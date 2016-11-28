---
layout: post
title: Curso de Python - Aula 4 - Mais Números e a Biblioteca Math
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

Olá pessoal! E vamos à mais uma aula de Python.

Nesta aula vou falar um pouco mais sobre números e operações e para isso vou usar alguns recursos da biblioteca **math**.

Vamos começar pela:

### Exponenciação

Eita palavrinha feia... Bom, mas acho que aqui todos sabem que exponenciação é isso: 2³ = 8.

Ok, mas como fazer o Python fazer isso para nós?

Uma primeira forma seria esta, que é bem parecida com outras linguagens:

```python
a = 2 * 2 * 2
```

Tudo bem, mas se eu quero fazer 2²³? Vou fazer isso:

```python
a = 2 * 2 * 2 * 2 * 2 # ... em quanto estava mesmo?...
```

Bem chatinho né? Por isso é bem melhor utilizarmos os recursos que a linguagem nos oferece para isso (em qualquer linguagem!). No Python a exponenciação é feita usando duas vezes o asterisco, assim:

```python
a = 2 ** 23
```

Interessante não? Agora que você já conhece a exponenciação, vamos à:

### Radiciação

Nossa! Outra palavrinha feia... A radiciação é o contrário da exponenciação e também é conhecida nos círculos sociais como "raíz". A raíz pode ser quadrada, cúbica ou de índice **n**. Aqui vamos usar uma função da biblioteca **math** do Python que nos retorna a raiz quadrada de um número. Aqui também é o nosso ponto de partida para as bibliotecas do Python. Por enquanto apenas veja e teste o código abaixo, sem perguntas, em breve você vai saber bem o que cada linha faz:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import math

a = 9
b = math.sqrt(a)

print(b) # Imprime 3.0
```

Resumindo, a função **sqrt()** da biblioteca **math** nos diz a raiz quadrada do número 9. Por enquanto apenas aceite isso, no assunto abaixo você vai saber o que são as bibliotecas e o que elas podem nos oferecer.

### Bibliotecas

De forma simplificada as bibliotecas são componentes que oferecem funções e classes para nossos programas. "Hum, o que são funções e classes?" você deve estar se perguntando, e eu vou explicar.

As **Funções** são rotinas pré estabelecidas que fazem alguma coisa específica e podem ou não retornar algum resultado. Um exemplo que já estamos usando faz um tempinho é a função **print()**, que pega uma informação e exibe na tela. Outra função que acabamos de usar é a **sqrt()** (SQuared RooT, Raíz Quadrada) que nos retorna a raíz quadrada de um número.

As funções podem ou não receber parâmetros. Os parâmetros são informações que passamos para as funções, mais um vez o exemplo da **sqrt()** que recebe um valor numérico. Os parâmetros são passados dentro dos parenteses que seguem o nome da função. Quando há mais de um parâmetro nós usamos vírgulas para separá-los. Veja um exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# Chamando função sem parâmetros
funcao1()

# Chamando função com um parâmetro
funcao2(param)

# Chamando função com dois parâmetros
funcao3(param1, param2)

# Chamando função com N parâmentros
funcao4(param1, ..., paramN)
```

Bem, por enquanto aceitem essas informações sobre funções como verdade absoluta do universo, quando chegar a hora de desenvolvermos as nossas funções esses conceitos ficarão muito mais claros.

Por enquanto não vou falar sobre as classes, isso fica para uma [aula sobre orientação à objetos](/aulas/python/2009/03/01/curso-de-python-aula-14-orientacao-a-objetos.htm).

Bem vamos voltar à biblioteca **math**. Essa biblioteca nos oferece algumas funções além da **sqrt()**, vou mostrar uma listinha abaixo:

- **math.sqrt(numero)**: Retorna a raíz quadrada do número.
- **math.cos(numero)**: Retorna o cosseno do número em radiano.
- **math.sin(numero)**: Retorna o seno do número em radiano.
- **math.tan(numero)**: Retorna a tangente do número em radiano.
- **math.radians(numero)**: Converte o angulo 'numero' de graus para radiano.
- **math.pi**: Não é bem uma função, está mais para uma constante com o número pi (3.1415926535897931).
- **math.hypot(x, y)**: Retorna a hipotenusa dos números (catetos) fornecidos.

A biblioteca **math** é muito mais do que apenas essas funções, mas isso foi apenas para lhes mostrar algumas coisas dela.

Bom acho que com isso já conseguimos ir para uns exercícios, certo?

### Lista de exercícios

Hoje a lista de exercícios será um pouquinho mais complexa do que as outras que já fizemos, mas não desanime, refaça quantas vezes for necessário para assimilar bem o conteúdo.

1. Calcule e exiba na tela a área do círculo de raio 4cm.
2. Calcule e exiba na tela as raízes de 9, 16, 20, 25 e 42.
3. Calcule a hipotenusa de um triangulo cujos catetos são 9cm e 4cm. (sem usar a função **math.hypot()** heim!)
4. Calcule o volume do cilindro de raio 6cm e altura 5cm.

Treine bastante e se tiver alguma dúvida procure mais informações na internet.

InFog.
