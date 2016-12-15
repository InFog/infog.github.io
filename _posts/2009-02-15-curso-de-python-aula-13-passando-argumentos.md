---
layout: post
title: Curso de Python - Aula 13 - Passando Argumentos Via Terminal
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

Olá alunos!

Espero que todos estejam gostando tanto destas aulas quanto eu! Graças à vocês eu também estou aprendendo bastante sobre a linguagem, muitos comentários que vocês fazem me ajudam a perceber novos horizontes pythonescos. Então relaxem, peguem um café e curtam as aulas!

Outra coisinha... Nesta semana eu resolvi meu primeiro problema real com Python! Fiquei muito feliz por ter usado um pouco mais de 40 linhas, incluindo comentários, para fazer um script de conversão de arquivos de logs para arquivos html! Ficou muito legal. Bem chega de recados e vamos à aula de hoje!

Nós já falamos sobre como receber dados do usuário usando a função **raw_input()** e também já sabemos ler arquivos texto, mas agora vamos aprender a passar parâmetros para nossos programas via linha de comando! Para isso vamos usar o módulo "**sys**" do Python. Este módulo nos permite usar algumas informações do sistema, recomendo que vocês o estudem mais a fundo, vale a pena :-)

Bem o que eu quero fazer é o seguinte, eu quero, por exemplo, chamar um programa dessa forma, no terminal:

$ programa.py arquivo_entrada.txt arquivo_saida.txt

Neste exemplo estariamos passando dois parâmetros para o programa, um arquivo de entrada e um arquivo de saída, ambos arquivos de texto.

Para fazer nossos programas entenderem esses parâmetros vamos utilizar a lista **argv**, do módulo **sys**, assim:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import sys
for param in sys.argv :
    print(param)
{% endhighlight %}

Ou seja, cada item da lista **sys.argv** é um parâmetro passado para o programa, vejam este exemplo:

{% highlight bash %}
$ ./param.py oi este é um teste
./param.py
oi
este
é
um
teste
{% endhighlight %}

Como vocês podem ver o primeiro parâmetro é sempre o nome do programa que foi chamado na linha de comando, neste caso o programa **param.py**, para pegarmos apenas os parâmetros poderiamos fazer algo assim:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import sys
param = sys.argv[1:]
{% endhighlight %}

Neste caso a lista de parâmetros seria armazenada na variável **param**, ou seja, tudo coisa bem simples =)

Bem, por hoje é só. Como vocês podem reparar as aulas estão ficando mais curtas, mas vou exigir um pouco mais de vocês nos exercícios.

### Lição de Casa!

Hoje vou querer o seguinte, vocês precisam baixar [este arquivo](http://evaldojunior.com.br/blog/wp-content/uploads/2009/02/ls_etc.txt), que é apenas um ls do meu /etc, vocês vão fazer um programa que receba o nome de um arquivo via parâmetro na linha de comando, no caso este arquivo, e o transforme em html. Na verdade eu quero uma tabela com três colunas mostrando todos os nomes de arquivos e diretórios que estão neste arquivo, algo assim:


<table border="1" style="width: 100%;">
<tbody>
<tr>
<td>arquivo1</td>
<td>arquivo2</td>
<td>arquivo3</td>
</tr>
<tr>
<td>arquivo4</td>
<td>arquivo5</td>
<td>arquivo6</td>
</tr>
</tbody></table>

Só isso, o arquivo de saída deve ser ls_etc.html

Bons estudos.

InFog
