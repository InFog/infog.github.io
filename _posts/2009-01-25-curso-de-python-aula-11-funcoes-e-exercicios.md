---
layout: post
title: Curso de Python - Aula 11 - Funções e exercícios
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

Olá pessoal!

A aula de hoje está sendo escrita diretamente da Campus Party Brasil 2009 =) O Evento está no fim... Pois é, cheguei no final...

Então vamos ao Python!

Hoje vamos ver as funções, que são trechos de código que podem ser "invocados" em outras partes do programa. Nós já estamos usando as funções do Python desde a primeira aula, um exemplo é a função **print()** que exibe algo na saída padrão. As funções podem ou não receber parâmetros, ainda na função **print()** podemos citar como exemplo o argumento que ela recebe que é um texto.
No código abaixo dá para ver uns exemplo de funções, claro que estas funções são bem simples e nem precisariam existir, mas servem como um bom exemplo.

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Função simples e sem parâmetros:
def ola_mundo():
    print("Olá Mundo!")
# Agora uma função com um parâmetro
def ola_pessoa(nome):
    print("Olá " + nome + ", como vai você?")
# Agora uma função com dois parâmetros
def ola_pessoa_blog(nome, blog):
    print("O blog " + blog + " pertence à " + nome)
# Chamando as funções
ola_mundo()
meu_nome = "InFog"
ola_pessoa(meu_nome)
meu_blog = "http://evaldojunior.com.br/blog"
ola_pessoa_blog(meu_nome, meu_blog)
{% endhighlight %}

Vejam esta última função, ela tem dois parâmetros, mas eles não precisam ser colocados na ordem em que foram definidos na função, você pode fazer isso também:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Invertendo os parâmetros
def ola_pessoa_blog(nome, blog):
    print("O blog " + blog + " pertence à " + nome)
meu_nome = "InFog"
meu_blog = "http://evaldojunior.com.br/blog"
ola_pessoa_blog(blog=meu_blog, nome=meu_nome)
{% endhighlight %}

Como vocês podem ver basta passar o nome dos parâmetros seguido por seus valores. Esta é uma forma que eu costumo fazer mesmo quando não é para "inverter" os parâmetros, eu acho isso legal por que fica mais simples de ler o código, fica um pouco maior, mas qual das opções abaixo fica melhor para ler?

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Função simples e sem parâmetros:
# chamando a mesma função de formas diferentes
rolar_dados(8, 3, 2)
rolar_dados(faces=8, sorteio=3, excluir=2)
{% endhighlight %}

Vejam que as duas linhas chamam a mesma função, mas a de baixo esté bem melhor explicada.

Lembram que eu falei sobre as docstrings na primeira aula? Pois aqui elas se encaixam muito bem, vejam o exemplo:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Função simples e sem parâmetros:
# chamando a mesma função de formas diferentes
def rolar_dados(faces, sorteio, excluir)
    """
        Esta função rola um dado e retorna o
        número sorteado, você pode dizer quantos
        dados serão rolados e quantos resultados
        devem ser ignorados (os de menor valor)
        Exemplo:
        dado = rolar_dados(faces=4, sorteio=5, excluir=2)
        Isso retornaria os 3 melhores resultados jogando
        um dado de 4 faces na forma de uma lista
    """
    # ... código da função ...

rolar_dados(faces=8, sorteio=3, excluir=2)
{% endhighlight %}

Com alguns interpretadores, como ipython, é possível ver esta documentação. Isso facilita muito a vida dos desenvolvedores. Se você ainda não tem o costume de documentar o seu código eu sugiro que comece agora!

Bem, por hoje acho que já chega, vamos aos exercícios, é treinando que se aprende!

### Lição de casa

Faça a função **rolar_dados()** do exemplo acima, o programa deve perguntar para o usuário todos os dados (faces, sorteio e excluir), lembrando que "excluir" tem que ser, pelo menos, um número menor que "sorteio".

InFog
