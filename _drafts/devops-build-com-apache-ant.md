---
layout: post
title: DevOps, Build com Apache Ant
categories:
- devops
- automacao
tags:
- devops
- ant
- automacao
status: publish
type: post
published: true
---

A partir deste post, vou começar a escrever aqui no blog sobre DevOps. Este é
um termo que está ficando cada vez mais popular e basicamente trata da melhor
integração entre desenvolvimento, infraestrutura e produção.

Falando um pouco mais sobre DevOps, é engraçado que eu sempre trilhei um
caminho DevOps antes de o termo existir/ser conhecido. Eu comecei no mundo de
TI trabalhando com redes e servidores GNU/Linux e depois fui migrando para o
desenvolvimento. Graças a isso eu consigo me dar bem com ambientes de produção
e servidores/serviços em geral.

Outra coisa que sempre busquei fazer foi a automação de tarefas repetitivas no
meu dia a dia. Sabe aquele deploy para produção onde é necessário copiar
arquivos, renomear diretórios, rodar migrations, etc? Esse tipo de coisa e
outras mais.

Para a automação eu sempre recorri ao bom e velho Shell Script. Então nos meus
projetos sempre tinha lá alguns scripts para preparar algo. O meu primeiro
script desta maneira foi chamado de **empacotar_lancamento.sh**. Isso lá em
2007 ou 2008.

Depois disso eu conheci o ótimo **GNU Make**, que ainda uso até hoje. Com o
Make eu ganhei a opção de rodar apenas uma parte do script de maneira bem
simples:

```bash
    make testes
    make empacotar
```

Sim, eu tenho projetos com o fonte em português :)

Não faz muito tempo eu resolvi evoluir e buscar novas ferramentas para
automatizar as tarefas repetitivas dos meus projetos. Uma dessas ferramentas
é o [Jenkins](http://jenkins-ci.org/). E enquanto estudava o Jenkins eu
percebi que a maioria da documentação, e literatura em geral, sobre o assunto
cita o [Apache Ant](http://ant.apache.org/) como ferramenta de automação.

Como eu já tive lá minhas diferenças com o Ant no passado (mais por
desconhecimento), eu acabei demorando um pouco para realmente estudar a
ferramenta e descobrir o que ela tem para oferecer.

Recentemente eu precisei automatizar o processo de deploy de um projeto e
resolvi dar uma chance para o Ant. O que segue é um resumo do que eu fiz e
as minhas impressões sobre o processo.

### Instalando o Ant

Instalar o Ant foi super fácil. A ferramenta é escrita em Java e está nos
repositórios oficiais do Debian, então bastou instalar usando o gerenciador
de pacotes:

```bash
    aptitude install ant
```

Depois disso a ferramenta já estava pronta para ser usada via terminal.

### Definindo o que será feito

Um passo importante foi definir o que seria feito pelo Ant.

- Rodar os testes unitários (PHPUnit);
- Copiar os arquivos do projeto para um diretório para empacotar;
- Durante a cópia ignorar arquivos de config e cache, ou apagar depois;
- Renomear o diretório de assets (evitar cache de css, js...);
- Alterar os arquivos de template para usarem o novo diretório de assets;
- Fazer o deploy na produção.

Pronto, apenas seis passos. Não são passos complicados para alguém executar e
eu levo cerca de 20 minutos para fazer o processo todo.

O problema é que 20 minutos é um tempo muito grande para fazer um deploy.
Graças a este tempo enorme eu ficava adiando as entregas, pois o processo pode
ser simples, mas é chato. Além de chato, consome tempo, imagina fazer 3 deploys
por dia. Já é 1 hora por dia! Acha pouco? Então vamos multiplicar isso... Se
você fizer 3 deploys por dia, 5 dias por semana, 25 dias por mês, já são 25
horas usadas para fazer um trabalho repetitivo que poderia ser automatizado.
E com 25 horas sobrando dá para desenvolver muita coisa nova no projeto ou
mesmo outros projetos.

E olha que eu nem falei da chance de erro humano durante a execução dos passos
para a entrega. Fatalmente um dos passos será esquecido ou feito de forma
incorreta em algum momento.

### O arquivo build.xml

Certo, não faça cara feia agora. O arquivo principal do Ant é **build.xml** e,
como se pode ser pela extensão, ele é um XML... Arquivos XML não são
necessariamente a coisa mais linda e/ou prática deste mundo, não para quem
conhece formatos como JSON e YAML. No meu caso, tive que encarar o fato de que
teria que trabalhar com XML e tentar tirar proveito disso. No final das contas
não o formato tem suas vantagens e, se você fizer um bom trabalho, o arquivo
fica bem legível e com fácil manutenção.

Bem, a primeira coisa no **build.xml** é definir o **project**:

```xml
    <project name="myProject" default="build" basedir=".">
        <description>
            My Project's Description
        </description>
    </project>
```

Com isso eu tenho um projeto e já estou dizendo que a **task** padrão é a
**build**. Calma que já vamos chegar nas **tasks**.

O próximo passo foi criar uma propriedade, qué tipo uma variável (ou talvez uma
constante). No caso eu queria definir o nome de um diretório onde a construção
do projeto seria realizada:

```xml
    <project name="myProject" default="build" basedir=".">
        <description>
            My Project's Description
        </description>

        <property name="build" location="build" />
    </project>
```

Certo, o nome da propriedade é **build** e a localização do diretório tem o
mesmo nome, **build**.

Depois eu já defini as duas primeiras **tasks**: **init** e **clean**:

```xml
    <project name="myProject" default="build" basedir=".">
        <description>
            My Project's Description
        </description>

        <property name="build" location="build" />

        <target name="init">
            <mkdir dir="${build}" />
        </target>

        <target name="clean">
            <delete dir="${build}" />
        </target>
    </project>
```

Nada muito complexo até agora. Claro que escrever desta maneira, com XML, é bem
mais trabalhoso que um um shell script, mas de qualquer forma a leitura não
não fica prejudicada. Uma coisa que eu percebi logo no começo foi que eu
precisava manter o diretório **build** vazio, ou inexistente, para que um
deploy não levasse arquivos de um deploy anterior. Então eu precisava executar
a **task** **clean** antes de executar a **init**, e para isso bastou adicionar
a propriedade **depends** na task **init**:

```xml
    <target name="init" depends="clean">
        <mkdir dir="${build}" />
    </target>
```

Com isso eu já conseguia chamar pelo terminal as tasks **init** e **clean**:

```bash
    ant init
    ant clean
```

Se chamar apenas **ant** um erro acontece pois em **project** foi definido que
a task padrão é a **build** e essa task ainda não existe.

Bem, o próximo passo foi rodar os testes unitários. O projeto é em PHP e estou
usando o PHPUnit. Como já tenho um **phpunit.xml** na raíz do projeto, basta
executar **phpunit** no terminal e os testes são executados. Pesquisei na
documentação do Ant e vi que para executar um comando é necessário usar o
**exec**, então criei uma task para isso:

```xml
    <target name="tests">
        <exec executable="phpunit" failonerror="true" />
    </target>
```

Eu instalei o PHPUnit via PEAR, então ele está na PATH do meu usuário. Eu
também poderia executar o PHPUnit instalado via composer. Uma opção bacana que
eu usei foi a **failonerror** que faz com que o Ant pare os processos caso o
PHPUnit dê algum erro. Isso é bom para o caso de eu colocar a task **tests**
como uma dependência de outra task, assim essa task não executaria por conta de
um erro nos testes unitários.

O próxima passo, enfim, foi construir a task **build**. Essa task é responsável
pela maior parte do trabalho (passos 2, 3, 4 e 5 da lista), então ela ficou um
pouco maior do que as outras tasks:

```xml
    <target name="build" depends="init,tests">
        <!-- Copying files -->
        <copy todir="${build}/deploy/application">
            <fileset dir="application">
                <exclude name="conf/config.php" />
                <exclude name="conf/database.php" />
                <exclude name="cache/" />
            </fileset>
        </copy>

        <!-- Copying JS's and CSS's to timestamped new dir -->
        <copy todir="${build}/deploy/assets_${DSTAMP}${TSTAMP}">
            <fileset dir="assets" />
        </copy>

        <!-- Renaming assets location in main template -->
        <replace file="${build}/deploy/application/views/template.php"
            token="/assets/" value="/assets_${DSTAMP}${TSTAMP}/" />
    </target>
```

Aí estão os 4 passos! A cópia dos arquivos, ignorando alguns arquivos e
diretórios, a cópia dos assets para um diretório com timestamp e a alteração
do arquivo de template para usar os novos assets.

Veja que eu coloquei a task **build** como dependente da **init** e da **tests**,
ou seja, se algum teste falhar, o build não será feito.

Neste ponto eu já conseguia fazer o build para gerar um novo entregável usando
o comando:

```bash
    ant build
```

Agora só faltava a task **deploy**:

```xml
    <target name="deploy" depends="build">
        <!-- Deploy to live! -->
        <scp todir="deployer@server:/path/to/application" keyfile="${user.home}/.ssh/id_rsa" trust="true">
            <fileset dir="${build}/deploy" />
        </scp>
    </target>
```

Agora usei o **scp**, que funciona como o comando **scp** mesmo. Repare que eu
coloquei a task **build** como uma dependência para **deploy**, pois o deploy
só pode ser feito tendo um entregável pronto.

Com o arquivo pronto passei a fazer deploys em menos de 3 minutos e sem
interação humana, basta fazer um **ant deploy** e ele roda tudo o que é
necessário para colocar a aplicação no ar. Claro que a construção do **build.xml**
foi baseada em estudos da documentação do Ant e em algumas tentativas e erros e
levou algumas horas para ser concluída, mas logo logo eu recupero esse tempo
graças a automação feita ;)

### Conclusão

O Apache Ant é uma ótima ferramenta para automação de tarefas e para fazer o
build automático de uma aplicação. Sua integração com o Jenkins é comum e até
incentivada, então um bom próximo passo seria a automação do build e do deploy
via Jenkins.

É claro que o Ant também tem seus problemas e existem outras ferramentas
similares, uma delas é o [Phing](http://www.phing.info/), que é derivado do
Ant, mas escrito em PHP.

Eu ainda tenho outras partes do deploy para automatizar, mas esse começo já
ajuda bastante. Por isso vou continuar estudando o Ant e o que mais ele pode
fazer, principalmente em conjunto com o Jenkins.

InFog
