---
layout: post
title: Curso de Python - Aula 17 - Mais sobre o PyGTK
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

hoje vamos continuar falando sobre [PyGTK](http://pygtk.org). Na [aula anterior](http://blog.evaldojunior.com.br/aulas/python/2009/03/15/curso-de-python-aula-16-iniciando-no-pygtk.html) vimos uma pequena introdução ao PyGTK, acredito que vocês não tenham encontrado muitas dificuldades com ele.

Pois bem, até agora fizemos uma janela com um botão, coisa simples, mas como eu faço para adicionar mais botões? Será que eu posso utilizar o mesmo método que usei para o primeiro botão? Usar a função **add()** da classe **gtk.Window**?

Hum, agora a coisa começa a complicar um pouquinho pois teremos que usar as "**Caixas**", mais precisamente as caixas verticais e horizontais, vejam o desenho abaixo, ele mostra o GeSpeak, mostrando as tais caixas:

![Uma representação do GeSpeak](http://evaldojunior.com.br/blog/wp-content/uploads/2009/03/gespeak_box.png)

Bem, o desenho acima não está completo, o GeSpeak ainda tem um menu, mais SpinButtons e mais uma Caixa Horizontal abaixo da primeira, mas serve como exemplo, vamos às explicações:

Em vermelho está a janela em sí, **gtk.Window**, este widget suporta apenas mais UM widget acoplado à ele. E é este o motivo que nos faz usar, neste caso, uma caixa vertical, **gtk.VBox**, em verde, este widget já suporta quantos widgets precisarmos, vejam que dentro dele temos, em roxo, duas caixas horizontais, **gtk.HBox**, e também um **gtk.TextView**. O mesmo acontece com as caixas horinzontais, elas suportam vários widgets.

No começo isso parece um pouco complicado, mas é bem simples. Vamos ver um código de exemplo:

{% highlight python %}
# -*- coding: utf-8 -*-
import pygtk
import gtk
def ola_mundo(widget):
    print "Hello World"
# criando a janela
janela = gtk.Window(gtk.WINDOW_TOPLEVEL)
# agora uma caixa vertical
caixa_v = gtk.VBox()
# agora um label e uma caixa de entrada
label1 = gtk.Label("Sou um label")
entrada = gtk.Entry()
# agora uma caixa horizontal, para o label e entry
caixa_h = gtk.HBox()
# adicionando o label e o entry à caixa horizontal
caixa_h.pack_start(label1, expand=False, fill=True)
caixa_h.pack_start(entrada, expand=False, fill=True)
# agora a caixa horizontal é adicionada à ciaxa vertical
caixa_v.pack_start(caixa_h, expand=False, fill=True)
# ufa, quase lá
# Agora um botão
botao = gtk.Button("Clique aqui")
botao.connect('clicked', ola_mundo)
# agora o botão é adicionado à caixa vertical
caixa_v.pack_start(botao, expand=False, fill=True)
# e finalmente adicionamos a caixa vertical à janela
janela.add(caixa_v)
janela.show_all()
gtk.main()
{% endhighlight %}

O código está bem comentado, vejam a janela que ele gerou:

![A janela GTK resultante do código anterior](http://evaldojunior.com.br/blog/wp-content/uploads/2009/03/captura_de_tela-widgetspy.png)

Simples, não? As opções expand e fill fazem referência ao preenchimento que o widget terá na janela, se ele irá se expandir junto com a janela ou não, etc.

E esta foi a nossa aula de hoje!

### Lição de Casa!

A lição de casa para hoje é: "Faça o código para montar a janela do GeSpeak mostrado na figura ali em cima, está bem colorido e fácil de acompanhar =) Bons estudos!
