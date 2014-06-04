---
layout: post
title: Programação na Estrada
categories:
- dev
- produtividade
tags:
- dev
- soudev
- php
- python
- flask
status: publish
type: post
published: true
---

Há pouco mais de um ano eu entrei em uma aventura compartilhada diariamente por
vários profissionais da minha região. Nós precisamos subir e descer a Serra do
Mar para ir e voltar de São Paulo para trabalhar.

No meu caso o tempo de viagem é de cerca de 2h para ir e pode chegar à 3h para
voltar. Ou seja, é um bom tempo que eu passo sentado no banco de um ônibus.

Logo no começo eu planejei usar esse tempo para trabalhar em projetos pessoais,
freelas, posts do blog e, pouco depois, na escrita do
(meu primeiro livro)[http://www.casadocodigo.com.br/products/livro-php-mysql].
O problema é que nops primeiros dia/semanas eu enjoava muito na viagem e
precisava tomar dramin praticamente todos os dias. Mas, com a ajuda da
(Cássia Luz)[http://twiller.com/cassialuz] eu fui largando o remédio aos poucos
até conseguir abandonar de vez. Parece que minha cabeça e meu estômago foram
se acostumando com a ideia de viajar de ônibus todos os dias.

Mesmo com a melhora, eu ainda enjoava um pouco com leitura e uso do smartphone.
Com o passar do tempo eu comecei a me sentir mais confiante para ler livros,
meu (e-reader)[http://blog.evaldojunior.com.br/leitura/2014/02/06/kobo-uma-resenha.html]
e para usar o smartphone. O problema era quando eu tantava usar um notebook ou
netbook... O enjoo sempre voltava.

Mas agora, depois de mais de um ano nesse sobe e desce na Serra, minha cabeça
resolveu colaborar de vez e estou, finalmente, conseguindo usar um netbook
durante a viagem. Um pequeno problema, ou não, é não tem conexão com a internet
durante a viagem, mas já falo sobre isso.

### Aproveitando o tempo

Eu tentei voltar a usar o netbook na viagem com alguns propósitos em mente:
Finalizar um freela, trabalhar em projetos pessoais e escrever mais aqui no
blog e na verdade este post é sobre isso :)

Um dos projetos em que estou trabalhando consiste na melhoria e padronização do
código de um site. O código anterior era em PHP, bastante bagunçado e contia
algumas gafes bem comuns de iniciantes. A linguagem neste caso realmente não
influenciava na bagunça, pois o que eu fiz para melhorar usando Python poderia
ter sido feito tranquilamente com PHP.

A minha ideia para o site, sendo um projeto pequeno e ótimo para reescrever e
praticar coisas novas, foi migrar para Python usando
(Flask)[http://flask.pocoo.org]. Como eu ainda não sou muito ágil com o Flask,
eu preciso consultar referências o tempo todo e não ter conexão com a internet
se mostrou um problema sério que eu resolvi assim:

- Instalação das dependências ainda em casa, enquanto com conexão.
- Não usar CDNs para Javascript e CSS para desenvolvimento local.
- Manter uma cópia dos manuais das ferramentas.

No caso das dependências, o (Virtualenv)[https://pypi.python.org/pypi/virtualenv/]
junto com o (PIP)[https://pypi.python.org/pypi/pip/]
resolvem todos os problemas deixando tudo instalado apenas para o projeto.

Os Javascripts e CSSs também foram fáceis de resolver mantendo cópias locais
de quaisquer bibliotecas necessárias.

Eu achava que o problema mesmo seria com os manuais, mas nem foi! Descobri que
grande parte dos projetos Python (ligados ao Flask, neste caso) disponibilizam
versões em PDF das documentações! Muito legal, não? E tem em ePub e Mobi também!

No caso do PHP, alguns projetos também disponibilizam versões em PDF e ePub das
documentações, como é o caso do (Silex)[http://silex.sensiolabs.org/].

Uma parte muito boa disso foi me forçar a entender ainda melhor o uso das
ferramentas e a saber ler com calma os manuais. Sem conexão não adiante correr
para a sua ferramenta de busca preferida para colocar o erro gerado pela
aplicação. Você precisa mesmo ler o erro e se entender com a documentação. Ah,
claro que isso também está me ajudando a entender melhor as mensagens de erro
e saber como resolver.

O interpretador interativo do Python também tem me ajudado muito! Com ele eu
consigo simular os cenários e tenho acesso à documentação das classes/funções
usando o doc e também a função **dir()** que me mostra os métodos de uma classe
ou objeto.

Outro ponto muito legal é a facilidade para se concentrar. Sem internet não há
chance de dar aquela olhadinha no e-mail, ou conferir o twitter rapidinho.
Usando um netbook, nem mesmo games dá para usar muito, então o que sobra é se
concentrar e produzir :D (Ei, sem ficar bitolado com produtividade aqui! Tem
dias que eu apenas leio ou jogo algo no smartphone, descanso é fundamental!)

A produção de textos para o blog também é fácil usando o (Jekyll)[http://jekyllrb.com/],
pois não preciso de paineis administrativos e coisas assim. É só escrever usando
markdown e, quando tiver conexão, mandar um push no Github.

Acredito que isso pode ser um exercício para você que quer se concentrar em
seus projetos mas tem a internet sempre te chamando para ver só mais aquela
coisinhaRapidinhoQueNãoVaiAtrapalhar. Tente pegar os manuais das ferramentas
que você usa e ficar sem conexão por alguns minutos, depois algumas horas, só
para ver o que pode aconter. Para mim está sendo ótimo!

Alias, estou escrevendo este texto de dentro do ônibus e estou quase chegando
em casa, então até mais!

InFog
