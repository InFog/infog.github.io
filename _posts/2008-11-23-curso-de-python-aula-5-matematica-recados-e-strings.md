---
layout: post
title: Curso de Python - Aula 5 - Matemática, Recados e Strings
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

Olá pessoal, aqui estou para mais uma aula de Python!

Na [última aula](/aulas/python/2008/11/16/curso-de-python-aula-4-mais-numeros-e-a-biblioteca-math.html) eu deixei uns exercícios um pouco mais complexos do que os das primeiras aulas. Eu esqueci que nem todos que estão fazendo o curso já tiveram esse tipo de disciplina na escola/curso/faculdade, então acabou que apareceram coisas bem "diferentes" para o cálculo da área do círculo e do volume do cilindro.

Bem para aqueles que não sabiam as fórmulas, aqui estão:

- Área do círculo: **PI * Raio²**
- Volume do cilindro: **PI * Raio² * Altura**

Nas próximas vezes em que eu pedir algum tipo de cálculo eu passo as formulas e também os resultados, assim vocês mesmos já se corrigem.

### Um pouco mais sobre strings

Na [aula dois](/aulas/python/2008/11/02/curso-de-python-aula-2-conceitos-e-variaveis.html), para mostrar as variáveis eu usei sempre textos que são chamados na maioria das linguagens de programação de "**strings**". Lembra que nesta aula aprendemos como "concatenar" variáveis de texto? Também vimos as aspas tríplices e o caractere especial **\n**.

Pois bem, hoje vamos ver mais algumas operações interessantes com as strings.

**Multiplicação**: Sim, no Python podemos multiplicar algum texto, o que faz bastante sentido, vejam um exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

linha = '-' * 50
print(linha)
```

A saída deste exemplo é esta:

```sh
$ ./linha.py
--------------------------------------------------
$
```

Neste exemplo eu multipliquei a string **-** (um traço) por **50** e obtive uma linha. Esse recurso é bem interessante, principalmente para formatação da saída de texto.

**Um pequeno aviso**: Atenção, lembra que usamos algumas funções da [biblioteca math](/aulas/python/2008/11/16/curso-de-python-aula-4-mais-numeros-e-a-biblioteca-math.html)? Pois bem, agora vamos usar algumas funções da biblioteca **str**, mas, ao contrário da math, nós não precisamos de um "**import str**" no início do código, pois essa biblioteca já é incluída por padrão.

**Posicionamento**: Legal, agora eu sei exibir uma linha com 50 traços, então seria bom se desse para colocar algo como um título centralizado nela. Sim, faremos isso! E não apenas centralizado, vou mostrar **três** alinhamentos diferentes para vocês:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

linha = '-' * 50
titulo = 'Aulas de Python'

print(titulo.ljust(50))
print(linha)

print(titulo.center(50))
print(linha)

print(titulo.rjust(50))
print(linha)
```

E a saída disso (dessa vez mostrei o meu terminal já que no browser isso não fica bem alinhado):

![alin](http://evaldojunior.com.br/blog/wp-content/uploads/2008/11/alin.png)

neste exemplo usei três funções da biblioteca str: **str.ljust()**, **str.center()** e **str.rjust()**. A função **str.ljust()** alinha um texto à esquerda, de acordo com o tamanho passado para ela, que neste caso foi **50**. As funções **str.center()** e **str.rjust()** trabalham da mesma forma, mas uma centraliza o texto e a outra faz o alinhamento à direita.

Legal, mas a função **str.ljust()** é inútil já que um texto já "alinhado à esquerda", certo? Errado! E se eu disser que podemos preencher o espaços em branco com algo além de "espaços em branco"? Vejam só:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

linha = '-' * 50
titulo = 'Aulas de Python'

print(titulo.ljust(50, '-'))
print(titulo.center(50, '*'))
print(titulo.rjust(50, '+'))
```

E a saída:

![alinpre](http://evaldojunior.com.br/blog/wp-content/uploads/2008/11/alin_pre.png)

Como segundo parâmetro para as funções eu passei os valores "-", "*" e "+", com isso o Python preencheu os espaços em branco. Usando isso dá para fazer um relatório bem bonito para o seu chefe heim?

**Caixa:** A biblioteca **str** também nos oferece algumas funções para trabalharmos com as caixas alta e baixa (Maiúsculas e minúsculas) das strings. Com algumas funções simples podemos deixar um texto todo em maiúsculas, minúsculas ou algumas outras formas, vejam:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = 'aulas de python'

print('Resultado com str.upper()')
print(titulo.upper())

print('Resultado com str.lower()')
print(titulo.lower())

print('Resultado com str.title()')
print(titulo.title())

print('Resultado com str.capitalize()')
print(titulo.capitalize())

print('Resultado com str.title() e str.swapcase()')
print(str.swapcase(titulo.title()))
```

O resultado:

![cases1](http://evaldojunior.com.br/blog/wp-content/uploads/2008/11/cases1.png)

A última linha também poderia ter sido escrita assim:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = 'aulas de python'
print('Resultado com str.title() e str.swapcase()')
print(titulo.title().swapcase()) # Um jeito mais curto para o mesmo resultado

# Isso funciona pois no Python há funções que retornam um objeto
# neste caso um objeto do tipo string que pode ter seus
# métodos (funções) utilizados.
```

Agora as explicações...

- Na terceira linha eu defini a variável **titulo** com o valor "**aulas python**".
- Na quinta linha eu usei a função **str.upper()** que deixa toda a string maiúscula.
- Na sétima linha eu usei a função **str.lower()** que faz o contrário, deixando toda a string minúscula (tudo bem que ela já era minúscula).
- Na nona linha usei a função **str.title()** que deixa maiúscula apenas as primeiras letras de cada palavra.
- Na décima primeira linha foi utilizada a função **str.capitalize()** que deixa maiúscula apenas o primeiro caractere da string.
- Já na décima terceira linha eu usei duas funções, a **str.title()**, que agora vocês já conhecem e a **str.swapcase()**. Aqui é feito o seguinte, a função **str.title()** deixa a string assim: "Aulas De Python", aí vem a função **str.swapcase()** e **inverte** a caixa da string, o que é maiúscula vira minúscula e vice-versa, deixando a string assim: "aULAS dE pYTHON".

**Substituição**: Agora vamos substituir um pedaço de uma string:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = 'aulas de python'
print(titulo.replace('python', 'linux'))
```

O resultado disso? Tá ai:

```sh
$ ./subs.py
aulas de linux
$
```

Neste exemplo eu substituí a palavra "python" pela palavra "linux".

### Exercícios:

Ah, mas já? Estava tão legal...

Nesta aula aprenderemos mais sobre strings depois de aprendermos alguns conceitos como as instruções para controle do fluxo do programa.

Agora a lição de hoje:

Todas as linhas devem ter a largura de 60 caracteres. As linhas devem ser preenchidas com "-".

- seu nome alinhado à direita em minúsculo.
- seu nome centralizado com as primeiras letras em maiúsculo.
- seu nome à esquerda, a linha preenchida com _ (underline).
- troque o seu sobre nome por "python" e exiba centralizado.
- transforme a frase "o menino é legal" em "a menina é legal" e exiba.

Bons estudos

InFog.
