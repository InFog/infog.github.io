---
layout: post
title: Vim Dicas - Parte 1 - Movimentação
categories:
- Vim
- Editor
tags:
- vim
- editor
- cli
status: publish
type: post
published: true
---

Muita gente acha esquisito o fato de eu usar o [Vim](http://www.vim.org) como
meu editor de textos principal, mas também tem um número razoável de pessoas
que querem entender melhor meus motivos para usar vim e querem iniciar a usar
o editor também.

É para essas pessoas que eu resolvi escrever uma série de postos ensinando o
básico e o avançado do Vim e seus pequenos truques.

O tópico deste post é a movimentação dentro Vim. A movimentação é um topico
bastante básico, mas também bastante poderoso, pois o Vim consegue utilizar as
movimentações para turbinar a utilização de outros comandos.

Bem, para iniciar o assunto é bom falar sobre o teclado do ADM3A, que é essa
máquina aí:

IMG ADM3A

Olha só como é o layout de teclado dele:

IMG layout teclado

Esquisito né? Mas é isso que o pessoal tinha nos anos 70. Repare onde estão as
setas e onde está o ESC. A movimentação no Vim foi feita para tirar proveito
deste teclado e para fazer com que o usuário não precise movimentar muito as
mãos durante o uso.

Por isso a movimentação básica, que em outros editores seria usando as setas,
no Vim usa as teclas **hjkl**:

- h: Movimenta para a esquerda
- j: Movimenta para baixo
- k: Movimenta para cima
- l: Movimenta para a direita

Claro que tudo isso estando no **modo normal**, que permite a realização de
comandos no Vim, no **modo inserção** essas teclas inserem as respectivas
letras no arquivo sendo editado.
