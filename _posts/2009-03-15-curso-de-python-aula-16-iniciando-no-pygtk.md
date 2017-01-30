---
layout: post
title: Curso de Python - Aula 16 - Iniciando no PyGTK
categories:
- Aulas
- python
tags:
- Aulas
- pygtk
- python
status: publish
type: post
published: true
mainimage: "aulas_python.png"
---

Olá alunos!

O exercício da última aula foi bem pesadinho, o pessoal teve que suar para resolver, então acredito que aprenderam bastante sobre Python, teve até gente dizendo que passou a noite fazendo os exercícios e com isso aprendeu bestante. Eu fico muito feliz de ver esse tipo de coisa acontecendo, acredito que estou estimulando vocês, alunos e leitores, a aprender e crescer mais. Então vamos em frente!

Como alguns devem ter visto eu lancei o GeSpeak 0.3 nesta semana, ele é um bom exemplo do que veremos hoje, as aplicações em [PyGTK](http://www.pygtk.org/). O PyGTK usa o GTK+ para oferecer um conjunto de elementos gráficos para desenvolvimento de interfaces com o usuário. O PyGTK é multiplataforma (*nix e Windows) o que significa que seu código pode rodar sem alterações praticamente em qualquer canto. O que não é o caso do GeSpeak, já que ele utiliza comandos do Linux para algumas tarefas.

Então vamos começar com o básico, janelas e botões.

O código abaixo cria uma janela com um botão, não há, ainda qualquer tipo de ação para o botão:

{% highlight python %}
#!/usr/bin/env python
import pygtk
pygtk.require('2.0')
import gtk

janela = gtk.Window(gtk.WINDOW_TOPLEVEL)
botao = gtk.Button("Clique aqui...")

janela.add(botao)
janela.show_all()

gtk.main()
{% endhighlight %}

Pronto, um programinha bem simples. Ele só exibe o botão, mas vamos entender como isso funciona...

Na segunda linha estamos importando o módulo PyGTK.

Na terceira linha nós usamos a função require do PyGTK para ter certeza que estamos com um versão da família 2.x.

A quarta linha é responsável por importar o módulo GTK.

Na sexta linha é criado um objeto da classe **Window** do módulo **gtk**.

Na sétima linha é criado um botão usando a classe **Button**.

Na nona linha adicionamos o botão à janela usando a função **add()** da classe **Window**.

A décima linha serve para exibir a janela e tudo o que está dentro dela, com a função **show_all()**.

E na décima segunda linha chamamos o looping principal do GTK com a função **main()**.

Agora vou mostrar um exemplo em que o clique do botão dispara uma função que exibirá "Hello World" no terminal:

{% highlight python %}
#!/usr/bin/env python
import pygtk
pygtk.require('2.0')
import gtk

def ola_mundo(widget):
    print "Hello World"

janela = gtk.Window(gtk.WINDOW_TOPLEVEL)
botao = gtk.Button("Clique aqui...")
botao.connect('clicked', ola_mundo)
janela.add(botao)
janela.show_all()
gtk.main()
{% endhighlight %}

Vejam que agora a função **connect()** é usada para "conectar" o sinal "**clicked**" do botão à função **ola_mundo()**.

Bem por enquanto é isso. Na próxima aula teremos mais, recomendo que todos leia o artigo [Mantendo a Sanidade com o Glade](http://www.cin.ufpe.br/~cinlug/wiki/index.php/Mantendo_A_Sanidade_Com_O_Glade), pois no começo dele é explicado como o GTK trabalha, leiam sobre os sinais e também a parte "Explodindo Coisas".

### Lição de Casa

A lição de casa de hoje é muito simples, mas vocês vão precisar usar a [Referência do PyGTK](http://www.pygtk.org/docs/pygtk/index.html) para fazer. Eu só quero uma janela com um botão escrito "Clique aqui", e quando a pessoa clicar o texto do botão deve mudar para "Clicado".

Bons estudos.
