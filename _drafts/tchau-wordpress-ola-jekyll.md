---
layout: post
title: Tchau, Wordpress. Olá, Jekyll
categories:
- blog
tags:
- wordpress
- jekyll
status: publish
type: post
published: true
---

Eu usei o Wordpress durante os primeiros anos de vida desde blog e ele serviu
muito bem para as necessidades que eu tinha. A minha opção sempre foi pelo
Wordpress instalado, ao invés do serviço oferecido pela Wordpress.com.

O problema de manter a sua própria instalação de Wordpress é que o treco é
pesado pacas. Se você parar para medir a quantidade chamadas ao banco de dados
a cada requisição, você toma um susto. Não que isso seja ruim, mas poderia ser
melhor.

A verdade é que atualmente eu não preciso mais (será que já precisei?) dos
recursos do Wordpress. Tudo o que eu quero é manter alguns textos no blog e
uma área de comentários. E quanto mais simples for para escrever, melhor.

Não é segredo para ninguém que eu sou um grande defensor das ferramentas de
linha de comando e para mim é bem chato ter que entrar na interface de
administração do Wordpress para escrever um texto e ainda ficar me preocupando
com a formatação enquanto escrevo. Por isso eu queria uma ferramenta mais
simples e que de preferência usasse markdown ou alguma outra tecnologia
semelhante para escrever.

Nessa busca acabei encontrando o Jekyll, um sistema pronto para blogs e com
uma ideia diferente do que em geral existe por aí: Páginas estáticas.

**O que? Páginas estáticas?**

Isso mesmo, usando o Jekyll você escreve seus textos em markdown e depois gera
as páginas estáticas. Simples assim.

Isso é algo que realmente muda bastante o conceito, pois não podemos adicionar
conteúdos que precisam ser dinâmicos. O blog passa a ser simplesmente um
grande conjunto de páginas HTML. Bastante leve, mas estático.

## Adicionando comentários

Um problema para sites estáticos é: como colocar comentários?

Existem alguns serviços que permitem adicionar um sistema de comentários a
qualquer página usando JavaScript, dessa forma mesmo páginas estáticas podem
ter comentários.

Após uma pesquisa rápida eu optei pelo
[Disqus](http://disqus.com/) que já filtra spams e tem uma aparência bem legal.

## Concluíndo


MEIO...

O legal é que agora eu consigo escrever usando o
[Vim](http://blog.evaldojunior.com.br/desenvolvimento/dicas/vim/2013/06/08/vim-o-editor.html)
praticamente de qualquer lugar, depois é só fazer o commit para o GitHub e lá
estará o post no blog.


FINAL...

Ah, este não é um texto para falar mal do Wordpress! Essa ferramenta tem seus
usos (muitas vezes equivicados...) e tem seu público. O fato de o Wordpress não
se encaixar nos meu propósitos não significa que ele também não irá encaixar
nos propósitos de outras pessoas. Cada um tem suas necessidades.
