---
layout: post
title: Acelerando respostas com o Memcached
categories:
- PHP
- Memcached
tags:
- PHP
- Memcached
- soudev
- develop
status: publish
type: post
published: true
---

Quando uma aplicação começa a crescer, o banco fatalmente se torna uma fonte de
problemas de performance. Em aplicações PHP, onde é bastante comum usar o MySQL,
esse tipo de problema é mais comum, pois o MySQL grava seus dados em disco e a
cada requisição precisa recuperar de novo do disco (ou de um cache interno).

Para resolver este problema existem algumas soluções que usam cache tanto em
disco quanto em memória. Uma boa opção para acelerar o processamento no backend
é utilizar o [Memcached](http://memcached.org/) para manter o cache em memória
ram.

No vídeo eu explico como funciona o uso do Memcached.

<iframe width="560" height="315" src="//www.youtube.com/embed/Z3XyWFV6VRI" frameborder="0" allowfullscreen></iframe>

InFog
