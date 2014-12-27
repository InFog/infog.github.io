---
layout: post
title: Como consertei meu Kobo
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

Há cerca de três meses eu Kobo mini parou de funcionar. Eu estava lendo o quarto
livro das Crônicas de Gelo e Fogo e, como todo mundo morre < / spoiler >, meu
Kobo resolveu morrer junto.

Tá, ele não morreu, morreu, ele ficava na tela de carregamento inicial, com a
carinha (in)feliz. E não passava disso.

De primeira tentei os métodos de reset tradicionais, tipo segurar o botão de
ligar por 20 segundos ou usar o botão de reset na traseira do aparelho. Cheguei
a deixa a bateria acabar para ver se resolvia, mas nada dava certo.

Acabei deixando o problema de lado por conta de muitas mudanças que estavam
acontecendo na minha vida. De vez enquando até pegava o Kobo e tentava os
procedimentos de reset, mas nada funcionava.

Na semana passada eu resolvi abrir o aparelho para remover a bateria e colocar
novamente. Mas acabei descobrindo algo ainda melhor: Ele tem um SD card que
pode ser removido! Não pensei duas vezes. Removi o SD card e montei para ver
o que tinha dentro.

São basicamente três partições no SD card. Uma é chamada de root, e tem o sistema
operacional que roda no Kobo. Essa partição é ext3 ou 4.

A outra partição é tipo um backup do root e acredito que é usada para o "reset
de fábrica" ou algo assim. Essa também é ext3 ou 4.

A terceira partição é uma FAT e tem os arquivos dos livros e um diretório
**.kobo**. Aí é que estava a mágica e o problema.

Esse diretório guarda as atualizações do Kobo e outros dados de sistema. Tipo
o hitórico de leitura e essas coisas.

A minha primeira opção seria apagar esse diretório e ter meu reset de fábrica no
modo hard. Mas acabei optando por pesquisar um pouco para ver se achava sistemas
operacionais alternativos para o oficial do Kobo. A pesquisa não foi frutífera,
talvez por pressa minha, mas acabei achando uma [página](http://www.mobileread.com/forums/showthread.php?t=185660)
com downloads de versões mais recentes do software do Kobo.

Interessante que o tal do diretório **.kobo** guarda apenas o diff da versão
"de fábrica", da partição root.

Dai eu beixei a nova versão e coloquei no diretório **.kobo**, movendo o diretório
**.kobo** antigo para um backup fora do SD card.

Depois disso liguei o Kobo e ele percebeu o update e fez a instalação.

Depois disso foi reconfigurar o acesso à minha conta e pronto, tudo funcionando
novamente :)

Agora quero entender melhor esse Linux que roda no Kobo e, de repente, até
escrever algo que rode nele.

Happy hacking,

InFog
