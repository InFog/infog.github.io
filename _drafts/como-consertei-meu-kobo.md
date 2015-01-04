---
layout: post
title: Como consertei meu Kobo Mini
categories:
- Kobo
- DIY
tags:
- Kobo
- DIY
status: publish
type: post
published: true
---

Há cerca de três meses eu Kobo Mini parou de funcionar. Eu estava lendo o quarto
livro das Crônicas de Gelo e Fogo e, como todo mundo morre < / spoiler >, meu
Kobo resolveu morrer junto.

Tá, ele não morreu, morreu, ele ficava na tela de carregamento inicial, com a
carinha (in)feliz. E não passava disso. Assim:

![A tela inicial do Kobo](/assets/images/kobo/kobo1.jpg)

Tentei usar o botão de bloquear a tela, que também serve para ligar e
desligar o aparelho, mas não funcionou.

Tentei os métodos de reset tradicionais, tipo segurar o botão de
ligar por 20 segundos ou usar o botão de reset na traseira do aparelho. Aliás,
é meio complicado chegar nesse botão, pois é necessário remover a placa
traseira do Kobo.

Cheguei a deixa a bateria do aparelho acabar para ver se resolvia, mesmo ela
demorando muito para acabar. Mas nada disso funcionou.

Acabei deixando o problema de lado por conta de muitas mudanças que estavam
acontecendo na minha vida. De vez enquando até pegava o Kobo e tentava os
procedimentos de reset, mas nada funcionava.

Na semana passada eu resolvi abrir o aparelho para remover a bateria e colocar
novamente, pois li em alguns fóruns que esse procedimento poderia funcionar.

Durante este processo acabei descobrindo algo ainda melhor: Ele tem um SD card que
pode ser removido:

![O Kobo sem a segunda tampa traseira](/assets/images/kobo/kobo2.jpg)

Não pensei duas vezes. Removi o SD card e acessei usando um leitor
para ver o que tinha dentro.

São basicamente três partições no SD card. Uma é chamada de root, e tem o sistema
operacional que roda no Kobo. Essa partição é ext3 ou 4.

A outra partição é tipo um backup do root e acredito que é usada para o "reset
de fábrica". Essa também é ext3 ou 4.

A terceira partição é uma FAT e tem os arquivos dos livros e um diretório
**.kobo**. Aí é que estava o problema.

Esse diretório guarda as atualizações do Kobo e outros dados de sistema. Como o seu
hitórico de leitura e outros dados.

A minha primeira opção seria apagar esse diretório e ter meu reset de fábrica no
modo difícil mesmo. Mas acabei optando por pesquisar um pouco para ver se achava sistemas
operacionais alternativos para rodar no Kobo. A pesquisa não foi frutífera,
talvez por um pouco de pressa minha, mas acabei achando uma
[página](http://www.mobileread.com/forums/showthread.php?t=185660)
com downloads de versões mais recentes do software do Kobo.

Algo muito interessante é que o diretório **.kobo** guarda apenas o diff da versão
"de fábrica", da partição root. Com isso as atualizações podem ser arquivos menores.
Muito inteligente isso.

Então eu baixei uma versão mais atual e coloquei no diretório **.kobo**,
movendo o diretório **.kobo** antigo para um backup fora do SD card.

Depois disso liguei o Kobo e o sistema detectou o update e fez a instalação.

O próximo passo foi reconfigurar o acesso à minha conta.

![A tela de seleção de idiomas do Kobo](/assets/images/kobo/kobo3.jpg)

E então pude acessar novamente meus livros:

![A tela de bloqueio do Kobo](/assets/images/kobo/kobo4.jpg)

Agora, com o aparelho funcionando e entendendo melhor como ele funciona,
eu quero entender melhor esse Linux que roda nele e, de repente, até
escrever algum software para ele.

Se você enfrentou problemas parecidos com o seu Kobo Mini, ou outras versões,
esses procedimentos podem ajudar.

Happy hacking,

InFog
