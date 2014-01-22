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

Este é um exemplo comum de problema de duplicação de código. Imagine que você
está desenvolvendo um site que contenha uma página de login. O primeiro
pensamento é que isso é bem fácil de resolver, pois basta criar uma página com
um formulário, adicionar umas validações em javascript, adicionar um backend
com validação dos dados e o login em si.

Mas depois de um tempo surge uma nova necessidade: Agora todas as páginas terão
um bloco de login no menu superior para facilitar a vida do usuário, assim ele
não precisa necessariamente ir para a página de login, basta digitar as
credenciais no bloco de login em qualquer página e pronto, está autenticado.

O problema é que com a nova necessidade vem também a vontade de simplesmente
copiar tudo o que é relacionado à primeira página de login e simplesmente colar
no novo bloco mudando uns nomes aqui e ali. Essa cópia parece inocente em um
exemplo pequeno assim, mas imagine algo copiado e colado em vinte partes
diferentes.

A cada pequeno trecho copiado se cria um pequeno débito técnico que vai
acumulando e acumulando até explodir, ou alguém pagar por ele.

### Identificando a duplicação de código

Identificar a duplicação não é uma tarefa muito simples, mas existem algumas
forma de se fazer este trabalho.

Uma das formas é a identificação manual, que pode acontecer sem querer quando
se esbarra em uma duplicação ou quando se procura por uma deliberadamente. O
problema é que quando se procura você tem que saber bem o que quer, pois você
já suspeita que existe algum tipo de duplicação.

Outra forma é usando ferramentas como *diff** e *meld*. O trabalho é mais
simples do que a busca totalmente manual, mas ainda é bastante trabalhosa e é
necessário saber bem o que se procura para poder comparar dois ou mais arquivos
diferentes em busca de possíveis duplicações.

E uma terceira forma é com o uso de ferramentas especializadas do tipo *CPD*
que são *Copy and Paste Detectors*.

No caso do PHP temos o (PHPCPD)[https://github.com/sebastianbergmann/phpcp]
que consegue varrer todo um projeto eidentificar sequências de linhas iguais.
