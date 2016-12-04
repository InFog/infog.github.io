---
layout: post
title: Curso de Python - Aula 9 - Mais sobre listas e um pouco de "aleatoriedade"
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

Na aula passada falamos um pouco sobre as listas em Python, mas lendo os comentários e o fórum e revendo as aulas eu vi que deixei algumas coisas de fora e também falei algumas besteiras =( Bem, mas como eu disse no começo do curso eu também estou aprendendo, então nesta aula vou corrigir alguns "enganos" da aula anterior e mostrar mais alguns assuntos.

Ahh o João Paulo Farias, que eu não conheço, mas vi esta [notícia no BR-Linux](http://br-linux.org/2009/aprendendo-a-programar-com-python/), também está publicando aulas sobre Python, o blog dele é [aprendendocompython.blogspot.com](http://aprendendocompython.blogspot.com), e eu recomendo que vocês passem por lá. Pelo que eu vi no site ele tem bastante experiência com a linguagem, e as aulas são bem legais, ou seja acaba sendo uma nova fonte para vocês, além das minhas aulas =)

Então vamos às observações sobre a aula anterior... Só para deixar claro, não é que os exemplos da aula anterior estejam errados, o problema é que eles são o "hard level", então é melhor partirmos para o "easy level", não?

Primeiro vou falar mais sobre as listas, eu acredito que apenas com o código abaixo e seus comentários já é possível ver que as listas não são tão feias quanto eu havia falado:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# criando uma lista vazia
lista_vazia = []

# agora uma lista com itens
lista_itens = ["python", "php", "c++"]

# adicionando ítens à lista
lista_vazia.append("item1")
lista_vazia.append("item2")

# removendo um item de uma lista
lista_itens.remove("php")

# retorna e remove o último ítem da lista
ultimo = lista_itens.pop()

print(ultimo) # mostra "c++"

# inverte a ordem da lista
lista_vazia.reverse()
lista_vazia.append("item5")
lista_vazia.append("item3")
lista_vazia.append("item4")
lista_vazia.sort()
```

Viram como a operações das listas pode ser bem mais simples? Agora deixa eu explicar o código:

Nas linhas 5 e 8 são criadas duas listas, uma vazia e outra já com alguns elementos.

Nas linhas 11 e 12 são adicionados itens à lista vazia, o mesmo procedimento pode ser usado em listas com elementos.

Na linha 15 é removido o primeiro elemento que casa com "php", caso tivesse mais de um elemento "php" apenas o primeiro seria removido.

Na linha 18 temos uma função bem interessante já que ela retorna e remove o último item da lista, neste caso o último item é "c++", então a variável "ultimo" recebe este valor, e logo após ele é removido da lista.

Na linha 23 a ordem da lista é invertida.

Já na linha 27 a lista é ordenada com a função sort().

Agora vamos ver uma coisa bem legal: Como embaralhar listas em Python:

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# importando o módulo random
import random

# criando uma lista
lista = ["joão", "maria", "josé", "ana"]

# embaralhando a lista
random.shuffle(lista)
print(lista)
```

Como vocês podem ver eu usei o módulo "random" do Python, este módulo possui várias funções interessantes para gerar números aleatórios, mas vamos falar mais dele mais para frente, ok?

Na linha 5 é importado o módulo random, assim como fizemos com o [módulo math](/aulas/python/2008/11/16/curso-de-python-aula-4-mais-numeros-e-a-biblioteca-math.html).

Na linha 8 é criada uma lista com 4 elementos e na linha 11 usei a função "shuffle()" do módulo random para embaralhar a lista. A linha 9 exibe a lista embaralhada.

### Lição de casa

1. Sorteio - Crie uma lista com o nome de 10 pessoas, embaralhe esta lista e sorteie uma pessoa, depois embaralhe novamente e sorteie outra pessoa, lembrando que não poderá ser a mesma pessoa a ser sorteada.
2. Mega Sena - Crie duas listas com números de 0 a 9, embaralhe as listas e sorteie um número de cada uma para formar uma dezena, repita a operação 5 vezes para sortear 5 dezenas, assim como na mega sena. Caso a dezena caia como 00 (zero, zero) faça o sorteio dela novamente até sair outra combinação. Depois disso exiba as dezenas sorteadas.

Eu gostei bastante de fazer estes 2 exercícios :-)

InFog
