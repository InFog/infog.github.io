---
layout: post
title: Curso Python - Aula 3 - Comentários, Docstrings e Números
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

Vamos agora para a terceira aula do curso de programação com Python!

Esta aula tem os seguintes assuntos: Comentários, Docstrings e Números.

Vamos ver o que são cada um deles, para que servem e como usá-los.

### Comentários

Você sabe o que são comentários em um programa? Comentários são pequenos textos, em geral de algumas poucas linhas, que explicam alguma coisa no código, em geral para ajudar um possível leitor, ou você mesmo, um tempo depois, a entender o que está acontecendo. Vamos a um exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Isto é um comentário
print("oi")
print("Tudo bem?") #Outro comentário
```

A linha 3 tem apenas um comentário, já na linha 5 tem uma função print() e também um comentário.

O interpretador do Python vai simplesmente ignorar os comentários, assim como outras linguagens. Então ele está ali para ajudar um ser humano =D

Comentar o código chega a ser uma arte, você não pode exagerar comentando cada linha para dizer o que ela faz, mas é sempre bom dar uma ajudinha nas linhas mais obscuras ou complexas. Alias, se um determinado trecho de código está muito obscuro, talvez seja melhor facilitar um pouco o código, do que encher de comentários.

Outra coisa importante: Jamais esqueça um comentário que diz algo contrário ao que o software faz. Isso pode atrapalhar muito, MUITO, alguém (ou você mesmo), quando for necessário manter o código.

### Docstrings

Gostaram dos comentários? Sim, eles são legais, mas agora vem uma coisa muito legal também, que são as **Docstrings**!

A gente ainda não chegou nas funções e parâmetros, mas já vou explicar as docstrings, já que elas serão muito úteis no futuro.

Imagine que você quer documentar uma função, uma classe, um módulo, etc. Sim, código bem documentado facilita a integração com novos desenvolvedores e ainda te ajuda a entender melhor que você mesmo está fazendo. E o que fazer caso você precise de uma boa documentação? Abre um novo documento em um editor de textos como o Open Office Writer? Escreve em um caderno? Escreve em um saco de pão? Nãããooo, vamos utilizar um recurso do Python que são as Docstrings. Veja este exemplo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

def funcao(param1, param2):
  '''
    Descrição:
      Esta é uma função de exemplo que apenas
      exibe duas strings

    Utilização:
      funcao(param1, param2)

    Parâmetros:
      param1
        Um texto qualquer
      param2
        Outro texto qualquer
  '''
  print(param1)
  print(param2)


print funcao.__doc__
```

Você lembra das aspas tríplices? Pois olha elas aí, só que neste caso elas não estão como valor de alguma variável, elas estão como documentação do seu código. Quando um outro desenvolvedor for utilizar a sua função ele pode chamar o método __doc__ dela e ver esta documentação, olha só a saída do programa acima:

```sh
$ ./docs.py

    Descrição:
      Esta é uma função de exemplo que apenas
      exibe duas strings

    Utilização:
      funcao(param1, param2)

    Parâmetros:
      param1
        Um texto qualquer
      param2
        texto qualquer
$
```

Legal né? Ou seja quando você estiver com dúvida sobre a utilização de alguma função no Python tente chamar o método __doc__ dela. Esta é uma ótima forma de documentar seu código.

### Números

Agora vamos aos números, aqui faremos algumas operações, e é nisso que o exercício de hoje será baseado.

As variáveis podem conter números de uma forma muito fácil, basta usar o operador de atribuição (sinal de = ) para isso. As operações entre os números também é super simples, você pode usar os operadores + (adição), - (subtração), / (divisão) e * (multiplicação), veja abaixo:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 1
b = 10
c = 200

d = a + b # Resultado: 11
e = c / b # Resultado: 20
f = a - b # Resultado: -9
g = b * c # Resultado: 2000

h = 3
i = b / h # Resultado: 3 (Opa!!!)
```

Até a linha 10 estava tudo tranquilo, não? Aí o Python disse que 10 dividido por 3 é igual a três! Como assim? O correto não seria 3.33? É isso mesmo, o correto seria ele mostrar as casas decimais, mas neste ponto nós usamos apenas números inteiros e com isso o Python concluiu que estamos trabalhando apenas com inteiros, por isso que o resultado foi 3. Mas é por isso que existem os...

### Tipos de Números

Sim, existem tipos diferentes de números, existem os inteiros, os reais... E no exemplo acima nós fornecemos dois números inteiros para o Python (3 e 10) e ele nos retornou o resultado inteiro da divisão que é o 3.

Mas como fazer para ter o resultado real?

Calma, vamos ver os tipos de números. Os **integer** (inteiros) são os que usamos acima eles têm um limite que varia de acordo com o sistema operacional. Outros dois tipos de números interessantes no Python são os números **float** (reais) e os **long** (longos)...

Os números **float** são os famosos "números quebrados", com esse tipo de número nosso exemplo teria retornado 3.33. Já vou mostrar, calma aí.

Os números do tipo **long** são também números inteiros, a diferença é que eles são virtualmente ilimitados, só o que vai te impor um limite aqui é a quantidade de memória do computador, sim isso mesmo, se você quiser usar um número super mega blaster gigante você pode, desde que seu computador não exploda tentando lidar com ele :).

Bom, como dizemos que um número é **integer**, **float** ou **long**? Assim:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 1
b = long(a) # Usando a função long()
c = float(a) # usando a função float()
d = 1.0 # Declaração usando o ponto
e = 5.5
f = -33.7 # Serve para negativos também
```

Simples né? Assim conseguimos resolver o probleminha da divisão:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 3.0
b = 10
c = b / a # Resultado 3.333
```

Como vocês podem ver a operação envolveu um número integer e um número float, neste caso o Python fez a conversão do integer para float e então fez a operação. **Atenção**: aqui o Python converte o integer para float apenas para fazer a operação, no final das contas a variável **b** continuará como um 10 inteiro!

Os grupos de precedência das operações podem ser definidos com parênteses:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 2 + 4 - 3 + 6 # Resultado: 9
b = (2 + 4) - (3 + 6) # Resultado: -3
c = b / a # Resultado 3.333
```

Viram a diferença entre agrupar e não agrupar as operações?

### Lição de Casa

A lição de casa de hoje vai continuar bem light, pois as Docstrings nós usaremos mais pra frente, então hoje vocês podem completar este código:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

a = 2
b = 10
c = 15

# 1) divida b por a

# 2) multiplique b por c

# 3) some o resultado da 1 com c

# 4) divida c por b de forma inteira

# 5) divida c por b de forma real

# 6) subtraia o resultado da 4 de c

# 7) some a e b e multiplique pela soma de b e c

# 8) Só para lembrar, exiba seu nome na tela
```

Então é isso, esta foi a aula de hoje, façam os exercícios e vão treinando aí =)

InFog
