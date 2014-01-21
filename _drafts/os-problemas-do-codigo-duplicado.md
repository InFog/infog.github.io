---
layout: post
title: Os problemas do Código Duplicado
categories:
- Desenvolvimento
- Melhores Práticas
tags:
- PHP
- Código Limpo
- Desenvolvimento
status: publish
type: post
published: true
---

Olá, pessoal!

Você já teve aquela sensação de *Déjà* vu enquanto trabalhava em algum trecho
de código? Infelizmente este é um sentimento bastante comum na nossa área e o
problema é que em algumas vezes não estamos necessariamente lidando com
duplicação de código e em outras sim.

IMAGEM WILD DUPLICATE CODE

A duplicação de código é o problema mais comum apontado pelos *Bad Smells*, que
é uma coleção de más práticas que acontecem em desenvolvimento de software.

### Problemas causados pela duplicação de código

Um dos problemas é o aumento da base de código. Isso pode não ser um problema
para armazenamento, mas é um problema para o entendimento da aplicação. Guardar
1mb de código é barato, guardar 5mb é tão barato quanto, mas com certeza é
muito diferente a quantidade de trabalho para entender 100 linhas de código do
trabalho para entender 500 linhas.

A manutenção é prejudicada também pois em geral é necessário alterar vários
trechos de forma semelhante e fatalmente um trecho ou outro será esquecido.
Imagine fazer uma correção em um local de uma aplicação e descobrir que esta
correção precisa ser feita em mais 5 telas que usam uma lógica semelhante. É
chato e é bastante comum que se esqueça de algo. Afinal de contas somos humanos
e humanos esquecem.

### O que gera a duplicação de código?

Vários fatores podem levar à duplicação de código. Um deles é ter mais de um
desenvolvedor no mesmo projeto, que é muito comum. O problema é que dois ou
mais desenvolvedores podem estar trabalhando em funcionalidades parecidas e com
isso acabam criando código parecido ou que faz a mesma coisa. Quem nunca viu em
um mesmo sistema duas funções/classes/pacotes que fazem exatamente a mesma
coisa? Certamente essas funcionalidades poderiam ser unificadas e reutilizadas.

É claro que o problema também pode acontecer em projetos de apenas um
desenvolvedor. As vezes aquela preguicinha de isolar algo para reutilizar pode
custar horas e mais horas de manutenção no futuro.

As vezes uma empresa possui alguns softwares diferentes e também acaba gerando
duplicação entre esses softwares, pois quando se precisa de uma funcionalidade
parecida de um software em outro acaba-se por copiar o código e mudar alguma
coisa aqui e ali em vez de criar alguma espécie de biblioteca que pode ser
usada pelos dois softwares.

### Um exemplo simples de duplicação: Página de login
