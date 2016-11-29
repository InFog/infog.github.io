---
layout: post
title: Curso de Python - Aula 6 - Um pouco mais sobre strings
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


E aqui vamos nós para mais uma aula de Python!

Mas antes da aula vamos aos recados e comentários...

Eu achei bem interessante o último exercício da [aula 5](/aulas/python/2008/11/23/curso-de-python-aula-5-matematica-recados-e-strings.html), aquele em que vocês deveriam transformar a frase "o menino é legal" em "a menina é legal". O que eu achei interessante é que somente alguns perceberam que bastava trocar as letras "o" pela letra "a". Mas percebam que não existe "certo" ou "errado", o que eu pedi foi para transformar uma frase em outra, então tivemos resultados assim:

```python
frase.replace("o menino", "a menina")
```

Que faz o que eu pedi, mas, como eu disse, dava para fazer assim:

```python
frase.replace("o","a")
```

Bem mais simples, não?

Então vamos à aula de hoje!

Hoje vamos falar um pouco mais sobre as strings... Sim, eu sei que já vimos bastante coisa sobre elas, mas hoje vamos ver um pouco mais :)

### Substrings

Uma coisa interessante sobre as strings é que você pode acessar pedaços delas de forma muito simples, vejam o exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = 'aulas de python'

# Pegando caractere por caractere
print(titulo[0])
print(titulo[4])

# Agora pegando intervalos de caracteres
print(titulo[0:5])
print(titulo[9:15])

# Outros modos:

# Do começo até X
print(titulo[:5])

# De X até o fim
print(titulo[9:])
```

O resultado:

```sh
$ ./substr.py
a
s
aulas
python
aulas
python
$
```

Agora as explicações:

- **Linha 4**: Defini uma variável chamada **titulo** e à ela dei o valor "**aulas de python**".
- **Linha 7**: Exibi o caractere **0** (zero) desda string, ou seja, a letra "**a**".
- **Linha 8**: Mesmo esquema da linha 7, só que desta vez exibindo o caractere número **4**, ou seja, a letra "**s**".

Agora vem a parte legal:

- **Linhas 11 e 12**: Exibi uma lista de caracteres, primeiro a lista de 0 até 5 para mostrar a palavra "aulas"...

### Pausa para compreender melhor

O Python faz a numeração dos caracteres de uma string desse jeito:

![Sequência de caracteres](http://evaldojunior.com.br/blog/wp-content/uploads/2008/11/seqcar.png)

Certo, simples né? Para pegar a letra "v" eu faria isso:

```python
texto[5]
```

E para pegar a palavra "**Como**" eu faria isso:

```python
texto[0:3]
```

Nãããoooo!!! Isso retornaria apenas a string "**Com**". Mas... Por que isso?

Ora, é bem simples, a lista [A:B] vai de A (inclusive) até B (exclusive). Muito complexo? Bem, ela vai de A até um antes de B, o nome disso é **Slice** (cortar em inglês).

### Fim da pausa!

Continuando... Então se eu pegar dos caracteres de 0 até 5 (na linha 11), então eu consigo pegar a palavra "aulas". O mesmo vale para a linha 12, onde eu pego a palavra "python".

**Linhas 17 e 20**: Nestas linhas eu usei um outro recurso interessante, quando você não fornece o primeiro elemento da lista de caracteres o Python entende que você quer o primeiro caractere da string, o caractere **0** (zero). Da mesma forma quando você não fornece o segundo elemento da lista o Python entende que você quer que seja o último caractere.

Sabendo disso tudo você se pergunta se é possível fazer algo como substituir uma letra dentro de uma string:

```python
texto[6] = "b"
```

Não! Não é possível alterar strings desta forma. Para isso utilize a função **str.replace()** que já vimos (aqui)[/aulas/python/2008/11/23/curso-de-python-aula-5-matematica-recados-e-strings.html).

Uma outra forma de pegar substrings é usando a função **str.__getslice__()**, desta forma:

```python
titulo = "aulas de python"
print(titulo.__getslice__(0,5))
```
É claro que é bem mais simples usar a primeira forma (texto[0:5]), mas é bom saber que existem outros meios :)

### Strip

Calma... não é o que alguns pensaram... Agora veremos mais uma função da biblioteca **str**, a função **str.strip()**. Os que já programam em alguma linguagem podem conhecer essa função pelo nome **trim**.

Vamos aos exemplos:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = '     aulas de python     '

print(titulo.strip())
print(titulo.lstrip())
print(titulo.rstrip())
```

Desta vez a string tem o valor de "**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aulas de python **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;", sim, com cinco espaços em branco antes e depois do texto. Aqui foi proposital, mas você pode se deparar com um texto assim por ai.

Na linha 6 eu removi os espaços no começo e no fim da string com a função **str.strip()**.
Na linha 7 eu removi apenas os espaços no começo da string usando a função **str.lstrip()** (Left Strip).
E na linha 8 eu removi apenas os espaços no fim da string usando a função **str.rstrip()** (Right Strip).

### Find

Agora um função legal para pesquisar textos:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

titulo = 'aulas de python'

print(titulo.find('de'))
print(titulo.find('we'))
```

O resultado:

```sh
$ ./find.py
6
-1
$
```

Na linha 6 eu pesquisei pelo texto "**de**" e fui informado que ele está começa no caractere 6. Isso é legal para não ficar contando "de olho" onde uma substring começa.
Já na linha 7 eu pesquisei pelo texto "**we**", mas como ele não existe na string eu recebi o resultado **-1**. Isso é interessante para fazer pesquisas em textos.

### Lição de casa!

Com isso vamos para a lição de casa de hoje, que ainda é bem leve e desta vez não requer código.

1. Se eu tenho o texto "Oi me chamo João! Como é o seu nome?", como eu faria para saber em que posição a palavra "nome" começa? E como eu retornaria essa palavra?
2. Ainda na mesma string da 1, como eu trocaria o nome João por José?
3. Como eu faço para remover os espaços no início de um texto? E no fim? E no início e no fim?

### E agora um desafio!

Calcule a área sob o gráfico da função **f = x + 3**, sendo que x vai de 2 à 4. Apenas com o que já aprendemos aqui já é possível fazer isso.

Bons estudos.

InFog
