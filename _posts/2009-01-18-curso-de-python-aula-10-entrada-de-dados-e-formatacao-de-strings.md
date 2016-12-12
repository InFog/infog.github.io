---
layout: post
title: Curso de Python - Aula 10 - Entrada de dados e formatação de strings
categories:
- Aulas
- GeSpeak
- python
tags:
- Aulas
- GeSpeak
- python
status: publish
type: post
published: true
mainimage: "aulas_python.png"
---

A aula de hoje vai começar um pouco diferente, vou mostrar o resultado do exercício "mega sena" da [aula 9](/aulas/python/2009/01/11/curso-de-python-aula-9-mais-sobre-listas-e-um-pouco-de-aleatoriedade.html).

O exercício não retrata exatamente a Mega Sena real, já que o número de dezenas é menor e as dezenas sorteadas vão até 99, mas o que vale é a ideia, certo?
Resolvi colocar o exercício aqui por que alguns me mandaram e-mail dizendo que estavam com algumas dificuldades para encontrar a solução. Então aqui vai:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import random
num1 = ["0","1","2","3","4","5","6","7","8","9"]
num2 = ["0","1","2","3","4","5","6","7","8","9"]
#random.shuffle(num2)
sorteados = "Dezenas sorteadas: "
i = 0
while i < 5:
    dezena = "00"
    while dezena == "00":
        random.shuffle(num1)
        random.shuffle(num2)
        dezena = num1[0] + num2[0]
    sorteados += dezena + " "
    i += 1
print(sorteados)
{% endhighlight %}

Vejam que esta é apenas uma das maneiras de resolver o problema. Alguns alunos fizeram de formas diferentes que também dão certo, e alguns até utilizaram funções que eu nem mostrei na na aula, mas que serviram muito bem.

Na linha 3 é importado o módulo <strong>random</strong>, que é onde está a função <strong>shuffle()</strong> que é a responsável por "misturar as bolas com os números". Nas linhas 4 e 5 são definidas duas listas com os números em formato de texto, talvez seja melhor trabalhar com números mesmo, mas eu achei que assim ficou simples para juntar os números e fazer as dezenas.

Na linha 6 eu começo a escrever o texto das dezenas sorteadas e na linha 7 eu inicio um contador para o número de dezenas sorteadas. Já na linha 8 começa o primeiro laço do programa, que vai fazer o sorteio se repetir até termos 5 dezenas

Na linha 9 eu já defini a dezena como "00" (zero zero) e então vem mais um laço que deve se repetir enquanto a dezena for "00".

Então vem a função <strong>shuffle()</strong> que embaralha as listas com os números, e logo depois a variável "dezena" rebe o valor do primeiro elemento de cada lista. Aqui acaba o laço, caso a dezena seja "00" ele vai se repetir.

Acabando o laço na linha 14 adicionamos o valor sorteado à variável "sorteados" e adicionamos 1 ao contador. Isso vai se repetir até o contador alcançar o número 5. Quando o laço acaba é exibida a variável "sorteados" com as dezenas sorteadas.

Se vocês olharem bem para o código e até mesmo o executarem algumas vezes vão ver que podem cair dezenas iguais, o que não é bom, certo? Mas isso eu vou deixar para vocês resolverem =)

Bem, tem um assunto que em breve vamos tratar, o desenvolvimento de programas com GUIs em Python, para isso vamos usar o [PyGTK](http://www.pygtk.org/). Isso ainda vai demorar um pouquinho, mas para quem quiser ver mais ou menos como funciona é só acompanhar o GeSpeak. O GeSpeak é um front end para o espeak, um sintetizador de voz para Linux. O GeSpeak já passou por algumas grandes mudanças de linguagem, mas acredito que o Python veio para ficar =) Então se você quiser conferir como é desenvolvido um programa em PyGTK é só fazer o checkout da versão de desenvolvimento do GeSpeak, como ele está no [GitHub](https://github.com/infog/gespeak) então isto é bem simples de ser feito, basta ter o git instalado e rodar este comando (em apenas uma linha):

```bash
git clone https://github.com/InFog/GeSpeak.git
```

Isto vai criar um diretório chamado gespeak, dentro dele estão os arquivos .py, para rodar o GeSpeak use o executável gespeak:

```bash
./bin/gespeak
```

Agora chega de enrolação e vamos à aula de hoje!

### Hora da aula!

A aula de hoje é uma base para a aula da semana que vem. Hoje veremos a entrada de dados do usuário e na semana que vem vamos fazer nossas primeiras funções, ou seja já estamos começando a deixar a fase do script, que é uma sequencia de instruções que é executada sem intervenção do usuário e vamos entrar na fase dos programas mais complexos que dependem do usuário para funcionar.

A função que vamos usar para receber os dados dos usuários é a <strong>raw_input()</strong>. Esta função lê dados na entrada padrão, que é o teclado na maioria das vezes, e depois retorna estes dados. A forma mais simples de armazenar os dados fornecidos pelo usuário é assim:

{% highlight python %}
#!/usr/bin/python
# -*- coding: utf-8 -*-
nome = raw_input("Digite o seu nome: ")
print(nome)
{% endhighlight %}

Neste caso a variável "nome" irá armazenar o que for digitado pelo usuário e depois será exibida na tela.

Você também pode usar funções de conversão para os dados fornecidos. Vamos dizer que você queira números inteiros ou reais:

{% highlight python %}
#!/usr/bin/python
# -*- coding: utf-8 -*-
inteiro = int(raw_input("Um número inteiro: "))
real = float(raw_input("Um número real: "))
{% endhighlight %}

Simples, não?

Agora vamos juntar o que vimos nas outras aulas com estas funções de entradas de dados. Vou fazer um pequeno exercício aqui, a ideia é fazer um programa para um colecionador de carros. Primeiro o sujeito vai dizer quantos carros ele tem, depois vai colocar o nome dos carros e por último a placa de cada um. Vamos ver como fica este código? Olha só:

{% highlight python %}
#!/usr/bin/python
# -*- coding: utf-8 -*-
print("Bem vindo ao Colecionador de Carros 10.000 Plus!")
nome = raw_input("Qual é o seu nome? ")
print("Olá " + nome + ", vamos à sua coleção?")
quantidade = int(raw_input("Quantos carros o senhor tem? "))
i = 1
carros = []
placas = []
while i <= quantidade:
    carros.append(raw_input("Carro %i: " % i))
    i += 1
print("Agora as placas...")
i = 0
while i < quantidade:
    placas.append(raw_input("Placa do %s: " % carros[i]))
    i += 1
print("Hora de mostrar a sua coleção!")
i = 0
while i < quantidade:
    print("O %s tem placas %s" %(carros[i], placas[i]))
    i += 1
print("Então é isso, tchau!")
{% endhighlight %}

A única novidade aqui é a forma como eu exibi os valores dentro das frases, usando o %. O nome disso é "formatar strings", e é um recurso muito útil. Ele funciona assim, string para formatar à esquerda, porcentagem, e valores à direita:

"Aqui %s incluído um texto" % "será"

Resultado: "Aqui será incluído um texto"

"Agora %s dois %s" % ("serão", "textos")

Resultado: "Agora serão dois textos"

Quando apenas um valor for inserido na string basta coloca-lo após o %, mas quando mais de um valor for adicionado é necessário coloca-los dentro de uma tupla, que é o caso do segundo exemplo.

Para inserir os valores você pode usar esta tabela simplificada:

<table border="1">
<tbody>
<tr>
<th>Expressão</th>
<th>Significado</th>
</tr>
<tr>
<td>%s</td>
<td>Uma string</td>
</tr>
<tr>
<td>%c</td>
<td>Caractere</td>
</tr>
<tr>
<td>%d</td>
<td>Decimal, inteiro</td>
</tr>
<tr>
<td>%f</td>
<td>Real (float)</td>
</tr>
<tr>
<td>%%</td>
<td>Um '%'</td>
</tr>
</tbody>
</table>

A última opção é interessante, é assim que se mostra um símbolo % em uma string em Python.

### Lição de casa

1. Sala de aula: Faça um programa que pergunte o número de alunos em uma sala de aula, depois pergunte o nome de cada um, após isso ele deve pedir 4 notas de cada aluno e fazer a média entre elas, se a média for maior que 6 o aluno está aprovado, senão reprova. No fim deve ser exibida uma tabela assim:
- Nome do aluno - nota1, nota2, nota3, nota4 - media - aprovado/reprovado

Hoje é só esse exercício =).

InFog
