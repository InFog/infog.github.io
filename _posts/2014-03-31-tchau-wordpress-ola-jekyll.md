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
Wordpress instalado, ao invés do serviço oferecido pela Wordpress.com, pois
assim eu tinha mais liberdade para a instalação de temas, plugins e outras
edições "na unha".

O problema de manter a sua própria instalação de Wordpress é que o treco é
pesado pacas. Se você parar para medir a quantidade chamadas ao banco de dados
a cada requisição, você toma um susto. Não que isso seja totalmente ruim,
mas poderia ser melhor.

A verdade é que atualmente eu não preciso mais (será que já precisei?) dos
recursos do Wordpress. Tudo o que eu quero é manter alguns textos no blog e
uma área de comentários. E quanto mais simples for para escrever, melhor.

Não é segredo para ninguém que eu sou um grande defensor das ferramentas de
linha de comando e para mim é bem chato ter que entrar na interface de
administração do Wordpress para escrever um texto e ainda ficar me preocupando
com a formatação enquanto escrevo. Por isso eu queria uma ferramenta mais
simples e que de preferência usasse markdown ou alguma outra tecnologia
de marcação de textos semelhante para escrever.

Nessa busca acabei encontrando o Jekyll, um sistema pronto para blogs e com
uma ideia diferente do que em geral existe por aí: Páginas estáticas.

**O que? Páginas estáticas?**

Isso mesmo, usando o Jekyll você escreve seus textos em markdown e depois gera
as páginas estáticas. Simples assim.

Isso é algo que realmente muda bastante o conceito, pois não podemos adicionar
conteúdos que precisam ser dinâmicos. O blog passa a ser simplesmente um
grande conjunto de páginas HTML. Bastante leve, mas estático.

Outra coisa interessante é que dá paraq usar o seu controlador de versões
favorito para manter as versões dos textos. No meu caso a opção foi pelo
Git e hospedagem no GitHub. Alias, a hospedagem no GitHub trouxe outra
vantagem, poder usar as páginas estáticas do serviço! Com isso nem mesmo
a hospedagem do blog eu preciso fazer mais =)

## Adicionando comentários

Agora, um problema para sites estáticos é: como colocar comentários? Afinal
não é possível se conectar a um banco de dados e gravar e adicionar comentários
usando páginas estáticas.

Mas, para isso, existem alguns serviços que permitem adicionar um sistema de
comentários a qualquer página usando JavaScript, dessa forma mesmo páginas
estáticas podem ter comentários.

Após uma pesquisa rápida eu optei pelo
[Disqus](http://disqus.com/) que já filtra spams e tem uma aparência bem legal.

## Edição de textos

Como eu disse, os textos no Jekyll são em formato markdown, então basta ter um
editor de textos para escrever.

O legal é que agora eu consigo escrever usando o
[Vim](http://blog.evaldojunior.com.br/desenvolvimento/dicas/vim/2013/06/08/vim-o-editor.html)
e em praticamente de qualquer lugar, depois é só fazer o commit para o GitHub e lá
estará o post no blog.

## Conclusão

Este não é um texto para falar mal do Wordpress! Essa ferramenta tem seus
usos (muitas vezes equivicados...) e tem seu público. O fato de o Wordpress não
se encaixar nos meu propósitos não significa que ele também não irá encaixar
nos propósitos de outras pessoas. Cada um tem suas necessidades.

O propósito aqui foi apresentar o Jekyll como uma ótima opção para manter um
blog, ainda mais para os nerds :)

Ah, que ver um exemplo de como fica um projeto Jekyll? Então acesse o
[projeto deste blog](https://github.com/InFog/infog.github.io) no GitHub.

InFog
