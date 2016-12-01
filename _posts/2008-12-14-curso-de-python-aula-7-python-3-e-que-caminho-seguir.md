---
layout: post
title: Curso de Python - Aula 7 - Python 3 e "Que caminho seguir?"
categories:
- Aulas
- python
tags:
- Aulas
- python
status: publish
type: post
published: true
mainimage: "aulas_python.png"
---

Olá!

Na semana passada foi lançado o Python 3.0 (em 3 de Dezembro de 2008), também conhecido por aí como "Python 3000" ou "Py3k". Acontecerem algumas mudanças na linguagem, mas nada que vá prejudicar o que já aprendemos até aqui. Para saber tudo o que mudou você pode ler a notícia [http://docs.python.org/3.0/whatsnew/3.0.html](aqui).

Como este lançamento ainda é muito recente eu não vou usar a nova versão para as aulas, aqui eu vou continuar com o Python 2.5, que é o mais novo aqui no meu [http://debian.org](Debian) Lenny.

Ah, eu também quero agradecer a todos que estão acompanhando o curso, está sendo uma experiência muito boa para mim, espero que todos vocês estejam gostando tanto quanto eu \o/.

Ok, recados dados, é hora de estudar!

### Que caminho seguir?

Tudo o que fizemos até agora foram scripts com apenas um caminho a ser seguido, mas agora vamos começar a ver como dar mais opções aos programas, por isso vamos ver as estruturas de controle. Essas estruturas são bem simples tudo o que você tem que saber são três palavrinhas: "Se", "Enquanto" e "Para". Tudo bem que temos que saber estas palavras em inglês, mas não são complicadas, vamos treinar? "Se" = "If", "Enquanto" = "While" e "Para" = "For".

Mas antes disso precisamos conhecer os operadores que fazem as estruturas de controle funcionar:

- `==` : É o operador de igualdade, se x igual a y é assim: `se x == y`.
- `>=` : Maior ou igual, se x maior ou igual a y é assim: `se x >= y`.
- `<=` : Menor ou igual, se x menor ou igual a y é assim: `se x <= y`.
- `!=` : Diferente, se x diferente de y é assim: `se x != y`.

### A condicional "if"

Então vamos começar com o "Se", que é muito conhecido na maioria das linguagens de programação como "if". O "if" funciona assim: "Se certa condição for verdadeira então faça tal coisa, caso não seja faça essa outra coisa".

A construção do "if" em Python é bem simples, vejam estes exemplos:

```python
#!/usr/bin/env python

a = 10
if a < 20:
    print("menor que vinte")
else:
    print("maior ou igual a vinte")
```

Vejam este outro exemplo:

```python
#!/usr/bin/env python

sexo = 'f'
if sexo == 'm':
    print('masculino')
elif sexo == 'f':
    print('feminino')
else:
    print('outro')
```

Então? Simples? Algo que eu acho interessante no Python é que ele tenta parecer, às vezes, com uma linguagem humana, e não de máquina, sim, sim, vejam este último exemplo, o uso de "dois pontos" para indicar o que fazer é muito comum, vejam este exemplo:

*Viram só? Acabei de usar os "dois pontos" para indicar o que viria a seguir, legal né?*

Agora vou explicar o que casa om dos códigos fazem: (usei os "dois pontos" de novo hehe)

O primeiro é bem simples, a instrução "if" é uma pergunta "se", ele funciona assim, se a sentença a seguir for verdadeira ele executa o próximo bloco de código identado. Neste caso apenas a função print() está identada, então somente ela seria executada. A instrução "else" significa "senão" e é opcional, ela diz o seguinte, "senão, então faça o próximo bloco identado.

O segundo exemplo é bem parecido com o primeiro, a diferença é que ele tem uma instrução "elif", o "elif" é um "else" e um "if" ao mesmo tempo, se nós usarmos o português para falar este código ele seria mais ou menos assim: "Se a variável sexo for igual a 'm' então mostra 'masculino', senão se a variável sexo for igual a 'f' então mostra 'feminino', senão mostra 'indefinido'". Ok, talvez usar o "senão" e o "se" juntos fique meio confuso, mas mesmo assim acredito que não seja tão complicado de entender.

Mas você também pode fazer uma coisa que é conhecida por aó como "if aninhado", que é simplesmente um conjunto de "ifs" um dentro do outro. Para fazer este exemplo eu preciso falar primeiro sobre o módulo da divisão para vocês. (é um pequeno desvio na aula de hoje, mas leiam com atenção!)

### Módulo da Divisão

O módulo de uma divisão é o que sobra dela. Por exemplo, 2 / 2 o módulo é zero, já que não sobre nada, em 10 / 5 a mesma coisa, o resultado da divisão é 2 e não é "resto". Já em 10 / 3 o resultado inteiro é 3, e o módulo é 1. Com isso podemos concluir que sempre que o módulo de uma divisão é zero é por que o primeiro número era divisível pelo segundo. No Python o módulo é feito usando o caractere de porcentagem "%". Olhem o código abaixo (exemplo que não funciona no Python3):

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 7
modulo = a % 2

print("O resto da divisão é"),
print(modulo) # imprime: o resto da divisão é 1
```

Agora vamos voltar aos "ifs" aninhados.

### Ifs Aninhados

Tudo bem, eu poderia ter usado um exemplo sem módulos de divisão, mas pelo menos assim vocês já prendem o que é isso =) Vamos lá!

Neste exemplo eu quero saber se um número é par e é divisível por 5, ou seja temos duas condições para verificar, o que indica que usaremos duas vezes a instrução "if". Vamos lá?

Primeiro passo: Saber se o número é "par". Esta é uma tarefa bem simples, para sabermos se um número é par basta ver o resto da divisão por 2, se for zero então é par.

Segundo passo: Se o número for par então também verificamos se ele é divisível por 5. Isso também é simples, se o resto da divisão por 5 for zero então ele é divisivel por 5.

Mão na massa! Vamos fazer o código:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

n = 10
if n % 2 == 0 :
    if n % 5 == 0 :
        print(n),
        print("É par e divisível por 5")
```

Pronto, nós definimos a variável "n" com o valor 10, verificamos se o resto da divisão por 2 é zero (então é par), se for zero mesmo então verificamos se o resto da divisão por 5 é zero também, se esta segunda condição também for verdadeira então nós mostramos uma mensagem. E é assim que colocamos um "if" dentro do outro, percebam que a verificação da divisão por 5 só vai acontecer se a condição da divisão por 2 for verdadeira.

Agora vamos conhecer o próximo tópico:

### O laço "while"

Bom o while é o chamado "enquanto", ele é chamado de "laço" por que repete seu conteúdo enquanto uma condição for verdadeira. Vamos fazer um exemplo que mostra os números de 1 até 20:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

n = 1
while n <= 20 :
    print(n)
    n = n + 1
```

Acho que o exemplo fala por si mesmo, mas vamos verificar... Nele é definida a variável 'n' com o valor '1', então eu uso o "while" para dizer que o próximo bloco deve ser executando "enquanto 'n' for menor ou igual a 20", ai dentro do bloco é exibido o valor de 'n' e então é somado 1 ao seu valor atual. É muito importante somarmos 1 à 'n', se não fizermos isso o laço "while" será executado indeterminadamente, isso é um erro de programação também conhecido como "loop infinito" (loop pode ser considerado como laço em inglês). Estes loops infinitos são uma beleza para travar programas =)

Vamos usar um outro exemplo, dessa vez usando o "while" e o "if". Agora o programinha irá exibir somente os múltiplos de 5 entre 1 e 30:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

n = 1
while n <= 30 :
    if n % 5 == 0:
        print(n)
    n = n + 1
```

Vejamos o que o programa faz... 'n' é definida com o valor 1, então é criado um laço que será repetido enquanto 'n' for menor ou igual a 30, então é verificado se 'n' é divisível 5, se sim o valor de 'n' é exibido na tela, depois do bloco do "if" é somado 1 à 'n'. Simples né?

Bom pessoal o "para" ou "for" em Python é um pouco diferente das outras linguagens e exige que conheçamos as arrays, coisa que ainda não vimos, por isso a próxima aula será para falarmos de arrays e o controle "for".

### Lição de Casa!

Conhecendo estas estruturas de controle já conseguiremos fazer uns exercícios mais legais =) Então vamos à eles:

1. Mostre todos os pares de 1 a 100 que são divisíveis por 3.
2. Ainda de 1 a 100 mostre apenas os ímpares e divisíveis por 13.
3. De 1 a 50 mostre os pares e divisíveis por 7, quando não for par diga isso, quando for par mas não for divisível por 7 diga também, algo assim:
- 1 não é par
- 2 é par, mas não é divisível por 7
- ...
- 14 é par e é divisível por 7
- ...

Pronto, acho que só esses já dá para passar um tempo brincando =)

InFog
