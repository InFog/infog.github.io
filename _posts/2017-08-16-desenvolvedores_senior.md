---
layout: post
title: O que desenvolvedores PHP sênior precisam saber em 2017
categories:
- php
- carreira
- desenvolvimento
tags:
- php
- carreira
- desenvolvimento
status: publish
type: post
published: true
mainimage: "developer_magic.png"
---

Tradução do original em inglês [aqui](http://blog.evaldojunior.com/php/developers/carrier/2017/07/11/senior-developers.html).

Este post é a minha opinião sobre o que eu acredito que desenvolvedores e
desenvolvedoras PHP sênior precisam saber em 2017. A principal razão para eu
escrever este post é ajudar profissionais a melhor entender seus próprios
conhecimentos e se lhes falta algo para dar o próximo passo em suas carreiras.

É importante lembrar que este post não é a verdade universal sobre o que
pessoas que trabalham com PHP precisam saber. Tenha isso em mente durante a
leitura.

É claro que o requisito número um é um bom conhecimento da linguagem PHP. Você
não precisa saber dos detalhes mais obscuros da linguagem, mas você deve conhecer
a linguagem bem o suficiente para se sentir confortável lendo código fonte seu e
de outras pessoas e você deve saber onde encontrar documentação e ajuda quando
precisar. Sim, desenvolvedores sênior também buscam por exemplos de código e
aprendem à partir destes exemplos, então não tenha medo de pesquisar por
respostas online, apenas certifique-se de diferenciar entre as boas fontes e as
fontes ruins. Na dúvida opte sempre pela [documentação oficial](http://php.net/docs.php)
e dê sempre uma passada no [PHP the Right Way](http://www.phptherightway.com/).

O PHP7 foi lançado faz tem tempinho e até mesmo a versão 7.1 já está
disponível como uma versão estável, então você deve saber o que há de novidades
na versão 7.x da linguagem. Velocidade é a primeira coisa que vem à cabeça e que
em geral todo mundo que desenvolve em PHP sabe, mas coisas como o
[null coalesce operator](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.null-coalesce-op),
a [tipagem de escalares para parâmetros](http://php.net/manual/de/migration70.new-features.php#migration70.new-features.scalar-type-declarations)
e o uso de exceções no lugar de erros são super úteis e podem te ajudar a deixar
o seu código mais seguro e confiável.

Usar o [composer](https://getcomposer.org/) para gerenciar as dependências de suas
aplicações deve ser a maneira padrão de gerenciar as dependências para você e
coisas simples como adicionar scripts personalizados no composer não devem ser
um mistério. Também é importante saber a diferença entre os comandos `install` e
`update` do composer e por que é tão importante adicionar o arquivo `composer.lock`
no seu controle de versão. Não vou dizer qual é a resposta aqui, então já fica o
primeiro item para pesquisar.

E, aliás, estamos em 2017, desenvolvedores devem ser capazes de usar ferramentas
de versionamento como [Git](https://git-scm.com/), [Mercurial](https://www.mercurial-scm.org/)
e outros. Branches, Merges e solução de conflitos devem ser ações simples e
naturais para sêniors.

Você também precisa conhecer os principais frameworks e as diferenças entre eles.
Será que eu devo usar o Symfony para construir uma landing page que será usada
por apenas algumas semanas? Ou será que o CakePHP é uma opção melhor? Talvez seja
o Yii ou o Laravel? O importante aqui é não ficar preso dentro das ferramentas e
capacidades de apenas um framework. A razão pela qual temos tantos frameworks
por aí é o fato de pessoas e projetos terem necessidades diferentes. Aqui podemos
aplicar o ditado: Se a única ferramenta que você tem é um martelo, você vai tratar
todos os problema como pregos.

Reconhecer e implementar Design Patterns também é necessário. Uma desenvolvedora
sênior sabe que não necessariamente se começa um projeto dizendo algo como "Vou
usar o padrão Strategy aqui", pois é necessário reconhecer que os padrões também
surgem do design da aplicação, por isso é bom saber como os padrões se comportam.
Claro que com o tempo é possível reconhecer tais padrões mais cedo no projeto,
mas como uma regra geral, em minha opinião, os padrões emergem do design, eles
não são forçados no design.

Desenvolvedores sênior devem ser capazes de escrever testes unitários para código
não testado e de refatorar tal código. Nossa indústria está em constante mudança
e ferramentas e bibliotecas estão em constante evolução. Ser capaz de remover
uma biblioteca não mantida de uma base de código e colocar uma outra no lugar é
uma ótima habilidade para se ter. Essa não é uma habilidade simples, pois requer
investigação e paciência, mas essa não é uma habilidade que muitos
desenvolvedores possuem, pois em geral temos vontade de jogar tudo fora e reescrever
o software como um todo usando as bibliotecas e ferramentas que são mais modernas
e legais (e um dia serão de novo as piores, velhas e abandonadas, mas no geral
ignoramos esta parte).

E por falar em testes, desenvolvedores sênior devem ser capazes de escrever testes
e também de praticar técnicas como Test Driven Development. Fazer "Mocks" de outros
sistemas e APIs não deve ser algo complicado ou não natural para sêniors.

Desenvolvimento é legal, mas você também deve ser capaz de entregar seu código
para ambientes de produção, assim as pessoas podem usar a sua aplicação. Mesmo
sabendo que é possível entregar aplicações usando FTP essa não deve ser a única
opção que você conhece. Ferramentas especializadas em "deploy" não são difíceis
de achar e você pode pegar um pouco de experiência com algumas ferramentas
SaaS. O [Capistrano](http://capistranorb.com/) é uma ferramenta Ruby bastante
usada para fazer o deploy de aplicações em [Ruby on Rails](http://rubyonrails.org/),
mas você também pode usá-la para aplicações PHP e existem até mesmo alguns plugins
para frameworks como o Symfony. O [Ant](http://ant.apache.org/) é uma ferramenta
que eu gosto bastante para automatizar tarefas, incluindo scripts para fazer deploys.
O [Fabric](http://www.fabfile.org/) é uma ferramenta Python para automatizar
tarefas e deploys e também existe o [Deployer](https://deployer.org/) para quem
quer manter tudo no mundo do PHP.

Depois de entregar o código em produção você deve ser capaz de entender como a
aplicação se comporta, para isso são necessárias ferramentas como [NewRelic](https://www.datadoghq.com/),
[Datadog](https://www.datadoghq.com/) e [Sentry](https://sentry.io/welcome/),
que são ferramentas SaaS que podem ser facilmente integradas à servidores e
aplicações. Também existem opções grátis como o [ELK](https://www.elastic.co/products).

Saber trabalhar com cache também é importante. Saber onde aplicar uma técnica de
caching pode ser a diferença entre ter uma experiência de usuário rápida ou uma
lenta com os servidores pegando fogo enquanto o cliente aguarda a página carregar.
E usuários não vão esperar a página carregar, eles vão procurar alguma outra
opção. Lembre-se de que é possível usar cache de diversas maneiras e é importante
saber onde e como aplicar técnicas de cache, do código à cdn.

**Importante**: Não dependa da empresa onde você trabalha para aprender coisas
novas. Se você não tem oportunidade de aprender testes unitários no seu cargo
atual, você pode fazer isso em casa construindo um projeto pessoal, por exemplo.
O mesmo se aplica para os demais itens deste texto. Hoje em dia é super simples
de se preparar um ambiente GNU/Linux virtual onde você pode testar diversas
técnicas e melhorar suas habilidades, inclusive para aprender algo novo que pode
ser usado em seu emprego atual ou mesmo para conseguir um novo. Sempre é possível
usar um cupom de [$10 na Digital Ocean](https://m.do.co/c/1059a87d7c47) para
fazer testes com um servidor privado e fazer o deploy de suas aplicações usando
até mesmo ferramentas para automatizar o processo como GitHub, BitBucket e
[Codeship](https://codeship.com/).

Desenvolvedoras sênior também devem ter boas habilidades em comunicação com
outras pessoas e devem ser capazes de entender o negócio das empresas para as
quais trabalham. Vamos falar a verdade, um número muito pequeno de pessoas
trabalha para empresas como Google, GitHub, Atlassian, Oracle e outras grandes
empresas focadas em software. A maioria de nós trabalha para lojas virtuais,
bancos, agências web e outros tantos tipos de empresas que estão fazendo negócios
online e dependem de uma plataforma sólida para sobreviver. Esse tipo de empresa
dificilmente vai jogar dinheiro no desenvolvimento de software e vai te dar
autorização para jogar tudo fora e reescrever todas as aplicações antigas que
você não aguenta mais dar suporte. Então, tente entender a empresa e tente
alinhar o lado técnico com o negócio para criar um ambiente onde todos podem
sair ganhando, pois sabemos que código ruim pode arruinar uma empresa.

Mais um detalhe importante: Você não precisa fazer tudo perfeitamente e saber
tudo o que eu listei aqui de cór, mas você precisa entender os conceitos e saber
procurar por ajuda nos lugares corretos quando necessário.

Você acha que eu deixei algo de fora deste post? A comunidade PHP é muito grande
e profissionais PHP existem em todos os formatos, cores e tamanhos e isso faz
essa comunidade ser muito especial. Deixe suas ideias nos comentários abaixo
e ajude a expandir o foco deste post.

InFog.
