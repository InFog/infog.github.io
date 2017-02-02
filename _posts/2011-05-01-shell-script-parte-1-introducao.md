---
layout: post
title: Shell Script - Parte 1 - Introdução
categories:
- Aulas
- Blog
- shell
- Shell Script
tags:
- Aulas
- shell
- shell script
status: publish
type: post
published: true
mainimage: "shell.jpg"
---

Olá!
Hoje inicio uma nova séria aqui no blog. Serão poucas "aulas" de shell, mas que podem fazer uma boa diferença para quem está aprendendo.

## Shell

O shell é um interpretador de comandos. Sempre que digitamos algo ele interpreta o nos dá algum retorno.
Podemos escrever sequências de comandos que serão executados pelo shell. Essa sequência de comandos fica guardada em um arquivo e é chamada de 'script'. Como esse script será interpretado por um shell, ele é chamado de Shell Script.

## Sabores de Shell

Existem vários interpretadores Shell no mundo Unix, os mais conhecidos são:

- Bourne Shell (sh): Desenvolvido por Stephen Bourne no Bell Labs (da AT&amp;T) foi o shell padrão dos sistemas Unix por muitos anos. Hoje está presente em diversos sabores de Unix e em praticamente todas as distros GNU/Linux.
- Korn Shell (ksh): Desenvolvido por David Korn, também no Bell Labs, é um uma extensão do sh com várias melhorias. Por ter funções que o sh não tem, acaba sendo a opção de alguns programadores.
- Bourne Again Shell (bash): Este é o shell oficial do projeto GNU. Tem suporte total ao sh e acrescenta novos comandos. É o shell que mais cresce em número de usuários e é o padrão das distros GNU/Linux.

Existem diversos sabores de shell, mas coloquei aqui apenas os principais. No restante deste documento usarei apenas o bash, mas a palavra 'shell' poderá ser usada para referencia-lo.

## Como funciona um comando

Quando se digita um comando em shell, ele é interpretado e executado. Em shell existem os comandos do próprio shell (if, switch) e também os diversos programas/comandos do sistema operacional (ls, cd, mkdir).

## Atribuição de Variáveis

Em shell é possível criar variáveis (assim como nas linguagens de programação) para guardar valores. Para isso use a sintaxe:

{% highlight sh %}
$ IDENTIFICADOR=VALOR
{% endhighlight %}

Um exemplo:

{% highlight sh %}
$ curso="Análise e Desenvolvimento de Sistemas"
$ ano=2011
{% endhighlight %}

Repare que não há espaços ao redor do símbolo de igual.Para exibir o conteúdo de uma variável e necessário usar um cifrão ($) antes de seu identificador:

{% highlight sh %}
$ curso="Análise e Desenvolvimento de Sistemas"
$ echo "O curso é $curso"
{% endhighlight %}

## Redirecionamento de Saída
Em shell é possível direcionar a saída de um comando para um arquivo usando as instruções '&gt;' e '&gt;&gt;'. O comando 'ls' lista o conteúdo de um diretório na tela. Para direcionar a saída do comando ls para um arquivo use '&gt;':
$ ls &gt; resultado.txt
O redirecionador '&gt;' apaga o conteúdo do arquivo e grava a saída do comando. Para adicionar a saída de um comando ao final de um arquivo use '&gt;&gt;', dessa forma o conteúdo do arquivo será mantido:

{% highlight sh %}
$ echo "Iniciando script" > log.txt
$ ls /etc >> log.txt
$ echo "Finalizando script" >> log.txt
{% endhighlight %}

A primeira linha imprime o texto "Iniciando script" no arquivo log.txt, se o arquivo já existir, ele apaa o conteúdo. A segunda linha lista o conteúdo do diretório /etc, e joga a saída para o arquivo log.txt, dessa vez mantendo o conteúdo do arquivo. A terceira linha imprime o texto "Finalizando script" no arquivo log.txt, mantendo o conteúdo do arquivo.

## Redirecionamento entre comandos

Além de redirecionar a saída de um comando para um arquivo, também é possível redirecionar a saída para outro comando usando o pipe (|), barra vertical. O comando ls lista o conteúdo de um diretório, o comando wc conta linhas, palavras e caracteres de um arquivo. Unindo esses dois comandos eu posso saber facilmente a quantidade de arquivos e diretórios dentro de um diretórios:

{% highlight sh %}
$ ls /etc | wc -l
{% endhighlight %}

O ls vai listar cada arquivo em uma linha e o wc, com a opção '-l', vai contar a quantidade de linhas.

## Guardando a saída de comandos em variáveis
No exemplo anterior o script contava o número de arquivos e diretórios em um diretório. Para guardar esse número em uma variável é necessário colocar o comando entre acentos graves:

{% highlight sh %}
$ numero_de_arquivos=`ls /etc | wc -l`
$ echo "Há $numero_de_arquivos arquivos no diretório /etc"
{% endhighlight %}

## Manipulando Strings

Existem comandos bem interessantes para manipular textos em ambientes Unix. Um deles é o 'cut'. Este comando 'corta' um arquivo em colunas devolvendo apenas a informação requisitada. Veja um exemplo, o arquivo '/etc/passwd' guarda a lista de usuários do sistema e algumas outras informações:

{% highlight sh %}
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/shsys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
{% endhighlight %}

Esta lista tem muita informação, só o que eu quero é o nome dos usuários. Como este arquivo tem campos delimitados por ':', basta usado comando 'cut' para cortar o arquivo em colunas:

{% highlight sh %}
$ cat /etc/passwd | cut -d : -f 1
root
daemon
bin
sys
sync
games
{% endhighlight %}

Pronto, uma lista bem menor, apenas com os nomes dos usuários. No comando 'cut' a opção '-d' define o delimitador das colunas do arquivo, no caso ':', e a opção '-f' diz qual é a coluna que queremos, no caso a 1ª.Vamos alterar este comando para que ele retorne apenas os usuários que não possuem um shell no sistema. Esses usuários são identificados por terem um shell '/bin/false' na 7º coluna do arquivo '/etc/passwd'. Para pegar esses usuários podemos usar o comando 'grep' que filtra um texto e imprime apenas as linhas que contém o texto pesquisado:

{% highlight sh %}
$ cat /etc/passwd | grep /bin/false
Debian-exim:x:101:103::/var/spool/exim4:/bin/false
statd:x:102:65534::/var/lib/nfs:/bin/false
messagebus:x:104:107::/var/run/dbus:/bin/false
polkituser:x:105:111:PolicyKit,,,:/var/run/PolicyKit:/bin/false
{% endhighlight %}

Legal, consegui a lista de usuários, mas eu queria apenas os nomes... Então basta redirecionar a saída mais uma vez e usar o 'cut':

{% highlight sh %}
$ cat /etc/passwd | grep /bin/false | cut -d :  -f 1
Debian-exim
statd
messagebus
polkituser
{% endhighlight %}

Para inverter a pesquisa e mostrar apenas o usuários que tem sim algum tipo de shell, diferente de /bin/false, basta usar a opção '-v' do 'grep' para que ele inverta a pesquisa e mostre não as linhas que NÃO casam com o texto informado:

{% highlight sh %}
$ cat /etc/passwd | grep -v /bin/false | cut -d :  -f 1
root
daemon
bin
sys
sync
games
{% endhighlight %}

E para exibir a quantidade de usuários com algum tipo de shell basta usar o comando 'wc':

{% highlight sh %}
$ cat /etc/passwd | grep -v /bin/false | cut -d :  -f 1 | wc -l
24
{% endhighlight %}

## Criando Scripts
Até agora os comandos foram executados no prompt do bash. Desta vez vou criar um arquivo com uma sequência de comandos que serão executados. veja o conteúdo do arquivo:

{% highlight sh %}
#!/bin/bash
usuarios_shell=`cat /etc/passwd | grep -v /bin/false | cut -d :  -f 1 | wc -l`
usuarios_sem_shell=`cat /etc/passwd | grep /bin/false | cut -d :  -f 1 | wc -l`
echo "O sistema tem $usuarios_shell usuários com shell ativo"
echo "O sistema tem $usuarios_sem_shell usuários com shell desativado"
{% endhighlight %}

Salvei este arquivo com o nome '**usuarios_shell.sh**'. A extensão '**.sh**' não é obrigatória, mas facilita na hora de procurar seus scripts. Além disso alguns editores de texto (gedit) usam essa extensão para deixar o arquivo com sintaxe colorida, o que facilita bastante a edição.Para executar o arquivo use o comando 'bash usuarios_shell.sh', dessa forma o arquivo será interpretado e executado pelo 'bash'.No arquivo há ums instrução especial na primeira linha. Essa instrução diz que esse arquivo deve ser interpretado pelo bash e graças a ela podemos executar esse script sem usar o comando 'bash nome_do_arquivo.sh'. Para isso é necessário que o arquivo tenha permissão de execução:

{% highlight sh %}
$ chmod a+x usuarios_shell.sh
{% endhighlight %}

Agora basta executar o arquivo:

{% highlight sh %}
$ ./usuarios_shell.sh
{% endhighlight %}

O './' é o caminho atual do arquivo (diretório atual) e é necessário para que o bash saiba onde está o arquivo que se pretende executar caso ele não esteja em um diretório que faz parte da **$PATH**, que é uma veriável que contém os diretórios onde há programas para serem executados.

## Considerações

Graças ao poder dos redirecionadores, como o pipe (\|), é possível montar scripts aos poucos, unindo as funcionalidades de diversos comandos. No exemplo acima foram usados os comandos 'cat', 'grep', 'cut' e 'wc' para gerar apenas um resultado. Essa é a maneira shell script de se construir scripts, unindo pequenos pedaços, que sozinhos fazem pouco, mas juntos fazem muito.

InFog
