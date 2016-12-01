---
layout: post
title: Curso de Python - Aula 8 - Mais sobre operadores e conhecendo as listas e o
  "for"
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

O assunto dessa aula são os operadores AND, OR e NOT!

Assim como muitas outras linguagens de programação o Python também aceita os operadores especiais **AND**, **OR** e **NOT**. Vamos trocar isso em miúdos... O **IF** reconhece apenas valores **False** e **True**. **False** é representado pelo **0** (zero), **None** e **False**, enquanto o **True** é representado por **True**, **1** (um) ou qualquer outro valor (strings, int, floats que tenham algum valor, menos **False**). Quando, no **IF** ou em outras estruturas de controle, executamos, por exemplo, <span style="font-style: italic;">10 % 2 == 0</span>, na verdade, esse trecho de código irá retornar True ou False, e o **IF** executará o código correspondente.

Mas, chegando ao ponto importante, o Python reconhece também o **AND** e o **OR**. Ou seja, usando vários testes com os operadores, eles retornarão apenas um valor, **False** ou **True**. Melhor explicar com exemplos.

O exemplo da aula anterior que mostrava se um número é par e divisível por 5 também poderia ser escrito assim:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

n = 10
if n % 2 == 0 and n % 5 == 0:
    print("O número é par e divisível por 5")
```

Com isso economizamos uma linha e mostramos toda a nossa habilidade em programação =)

Mas deixa eu explicar... o **AND** é um operador "**E**", ele exige que ambas as expressões sejam verdadeiras, para facilitar ainda mais a visualização dessas tais "expressões" vamos coloca uns parenteses neste **IF**:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

n = 10
if (n % 2 == 0) and (n % 5 == 0):
    print("O número é par e divisível por 5")
```

Que tal agora? Ficou melhor para entender? Vejam a primeira expressão dentro dos parenteses **(n % 2 == 0)**, ela tem que retornar um valor verdadeiro (**True**) além disso a segunda expressão **(n % 5 == 0)** TAMBÉM precisa ser verdadeira, afinal de contas estamos usando o operador "**E**" (**AND**). Isso fica muito claro quando falamos este **IF** em português, **"Se o módulo da divisão por 2 for zero E o módulo da divisão por 5 for zero então:"**, pode ser que você se atrapalhe um pouco no começo, mas esses operadores são muito comuns em programação, então é melhor se acostumar com eles, ok?

O operador **OR** (operador or or, sanduíche íche íche :-P ) quer dizer **OU**, ou seja "**OU** um **OU** outro". Tá vamos ver um exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

cor_carro = "cinza"
if (cor_carro == "azul") or (cor_carro == "cinza"):
    print("Ok, eu gosto desta cor")
```

Traduzindo: A cor do carro pode ser azul **OU** cinza, eu gosto das duas.

É muito importante lembrar que esses operadores devem ser usados sempre em caixa baixa (and e or) e não em caixa alta (AND e OR).

Já o operador NOT é o do contra gosta de negar a tudo e todos, revoltado que só ele... Se uma expressão é verdadeira ele diz que é falsa e se é falsa ele diz que é verdadeira. Vamos ver um exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

cor_carro = "amarelo"
if (not cor_carro == "azul"):
    print("Ok, eu gosto desta cor")
else:
    print("Eca! não gosto de azul!")
```

Desta vez estou dizendo que a cor pode ser qualquer uma menos azul. O código diz isso **"Se o contrário da expressão for verdadeiro então..."**. Para ficar mais simples de ver que tal colocarmos o **NOT** fora dos parenteses?

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

cor_carro = "amarelo"
if not (cor_carro == "azul"):
    print("Ok, eu gosto desta cor")
else:
    print("Eca! não gosto de azul!")
```

Que tal? A expressão **(cor_carro == "azul")** será falsa já que a variável cor_carro contém o texto **"amarelo"** mas ali está o **NOT **para negar o resultado, lembrem-se que ele é do contra, então ele vai dizer que a expressão é verdadeira. Como o **IF** expressa sempre um resultado verdadeiro então ele irá usar o print que diz "Ok, eu gosto desta cor".

Bem, agora vamos às arrays, nosso último passo antes de conhecer a estrutura de controle **FOR**.

Bem, a primeira coisa a saber sobre as arrays no Python é que é muito mais comum utilizarmos listas, mas as arrays também existem e são bem poderosas. Mas vamos começar pelas listas. Vejam este exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

lista = ["pêra", "uva", "maçã"]
print(lista[0]) # mostra "pêra"
print(lista[2]) # mostra "maçã"
print(lista[-1]) # mostra "maçã"
print(lista[-2]) # mostra "uva"
```

Bem simples não? Em Python é bem fácil usar listas. Vejam que o primeiro elemento de uma lista será sempre o elemento zero. Algo bem legal também é que podemos contar do último para o primeiro, neste caso o elemento "-1" é o último da lista, o "-2" é o penúltimo e assim por diante. Ag0ra vejam como trocar um item e como adicionar mais itens:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

lista = ["pêra", "uva", "maçã"]

# trocando um item: pêra por banana
lista[0] = "banana"

#
# Para adicionar um elemento em uma lista
# é meio chatinho =(
# Reparem que eu preciso repetir o último item
# e só então adicionar mais um
lista[2:3] = ["maçã", "morango"]
print(lista[3]) # mostra "morango"

# mas eu poderia "automatizar" assim:
lista[len(lista):len(lista)+1] = [lista[-1],"pêssego"]
print(lista[-1]) # mostra "pêssego"
```

Bonito? É eu também acho que não... Essas formas de adicionar itens são bem chatinhas, mas quando conhecermos as arrays tudo ficará mais fácil.

Então vamos ver como remover um item:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

lista = ["pêra", "uva", "maçã"]

# remover um item: maçã
lista[2:3] = []
print(lista) # mostra ['pêra','uva']
```

Como vocês podem ver eu precisei dizer o ítem a ser removido +1, por isso que eu usei [2:3], mas o 3, não existe nesta lista, mesmo assim o 2 foi removido.

Bem esta é a forma básica de se trabalhar com listas, as Arrays são bem parecidas mas oferecem algumas funções a mais que quebram um galhão, nela temos, por exemplo, funções para adicionar novos itens e também para remover itens. Mas as Arrays vão ficar para a próxima aula, ahh também vamos falar de listas multidimensionais!. Agora vamos falar um pouco sobre a estrutura de controle "**FOR**".

Na verdade o **FOR** em Python é um pouco diferente de outras linguagens onde geralmente se define um valor inicial, um final e um contador para uma variável. No Python o **FOR** é usado junto com as listas, desta forma:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

lista = ["pêra", "uva", "maçã", "banana"]
for fruta in lista:
    print(fruta)
```

Pois é, o **FOR** é isso, simples não? Ainda vamos falar bastante sobre o FOR, mas antes temos que conhecer as arrays, que são o assunto da próxima aula =)

### Lição de Casa

A lição de casa desta semana é bem fácil eu quero duas listas, uma com 5 nomes de carros e a outra com 5 cores, só o que eu quero que vocês façam é associar cada carro a uma cor, tipo o carro 2 é da cor 2, assim:

- O Gol é azul
- O Celta é vermelho

Vocês podem usar qualquer coisa que já tenhamos aprendido e não somente o que está na aula de hoje. Aproveitem que este é, provavelmente, o último exercício no "modo easy". Ahh provavelmente não terá aula na semana que vem, então boas festas à todos! Divirtam-se e curtam o Natal e o Ano Novo =)

InFog
