---
layout: post
title: Curso de Python - Aula 19 - PyGTK e sua documentação
categories:
- Aulas
- python
tags:
- Aulas
- python
- vakinha
status: publish
type: post
published: true
mainimage: "aulas_python.png"
---

Olá pessoal!

Aqui vamos nós para mais uma aula de Python!

Hoje veremos um pouco mais sobre os conectores e também vamos aprender a encontrar respostas na documentação do PyGTK.

É através dos conectores que nós conseguimos ligar as ações do usuário na interface às funções do programa. Na [aula 16](/aulas/python/2009/03/15/curso-de-python-aula-16-iniciando-no-pygtk.html), nosso primeiro contato com PyGTK, já existe uma demonstração de um conector ligando o evento "clique" de um botão à função "**ola_mundo**".

Primeiro precisamos saber que não existe apenas o sinal **'clicked'**, alguns widgets do PyGTK apresentam outros tipos de sinais, então nossa missão é descobrir que sinais são esses. Mas como faremos isso? Simples, basta ter alguns conhecimentos que você já deve possuir: Leitura e Navegação na Web. [Na página de referência do PyGTK](http://pygtk.org/docs/pygtk/), [também disponível aqui](https://developer.gnome.org/pygtk/stable/), você encontra a documentação de todos os componentes desta API.

Pois bem, vamos fazer o seguinte exemplo: Uma janela com um rótulo e um botão, quando o mouse passar sobre o botão o rótulo deve dizer "O mouse está sobre o botão!" e quando deixa-lo a mensagem muda para "O mouse saiu de cima do botão!". Aqui está um modelo para a janela:

![Modelo de como deve ser a aplicação](http://evaldojunior.com.br/blog/wp-content/uploads/2009/05/aula_19_1.png)

Janelinha bonitinha, né? Fiz no [Inkscape](http://www.inkscape.org/) =)

Bem, agora que já temos o modelo precisamos escrever o código para esta janela:

{% highlight python %}
#!/usr/bin/env python
# -*- coding=utf-8 -*-
import pygtk
import gtk
class CJanela():
    __doc__ = """
        Classe CJanela, desenha uma janela com um label e um botão em uma
        caixa vertical.
    """
    def __init__(self):
        self.janela = gtk.Window(gtk.WINDOW_TOPLEVEL)
        self.janela.set_title("Aula 19, Sinais")
        self.rotulo = gtk.Label()
        self.botao = gtk.Button("Passe o mouse")
        self.caixa = gtk.VBox()
        self.caixa.pack_start(self.rotulo)
        self.caixa.pack_start(self.botao)
        self.janela.add(self.caixa)
        self.janela.show_all()
janela = CJanela()
gtk.main()
{% endhighlight %}

Vejam que desta vez estou usando uma metodologia diferente, fiz uma classe **CJanela** que é a responsável por exibir a janela e seu conteúdo. Acredite em mim esta metodologia facilita muito o acesso aos widgets.

Agora já temos a janela com o rótulo e o botão, agora nos resta programar as ações para "mouse sobre" e "mouse sai".

Então vamos recorrer à documentação do PyGTK, como vamos usar os sinais do botão então é a [documentação desde](http://pygtk.org/docs/pygtk/class-gtkbutton.html) que devemos ver. Essa documentação também está disponível [aqui](https://developer.gnome.org/pygtk/stable/class-gtkbutton.html).

Vejam na área "**gtk.Button Signal Prototypes**", este widget nos oferece seis sinais: **activate**, **clicked**, **enter**, **leave**, **pressed** e **released**. Para o que queremos fazer os sinais **'enter'** e **'leave'** serão suficientes. Reparem que na referência diz que o sinal **'clicked'** é praticamente o único que uma aplicação precisa, em geral.

Então vamos criar as funções **'mouse_sobre'** e **'mouse_saiu'**, elas serão as responsáveis por alterar o texto do rótulo, e usaremos os conectores para ligar os sinais do botão à estas funções, vejam o código:

{% highlight python %}
#!/usr/bin/env python
# -*- coding=utf-8 -*-
import pygtk
import gtk
class CJanela():
    __doc__ = """
        Classe CJanela, desenha uma janela com um label e um botão em uma
        caixa vertical.
    """
    def __init__(self):
        self.janela = gtk.Window(gtk.WINDOW_TOPLEVEL)
        self.janela.set_title("Aula 19, Sinais")
        self.rotulo = gtk.Label()
        self.botao = gtk.Button("Passe o mouse")
        self.botao.connect('enter', self.mouse_sobre)
        self.botao.connect('leave', self.mouse_saiu)
        self.caixa = gtk.VBox()
        self.caixa.pack_start(self.rotulo)
        self.caixa.pack_start(self.botao)
        self.janela.add(self.caixa)
        self.janela.show_all()
    def mouse_sobre(self, widget):
        self.rotulo.set_text("O mouse está sobre o botão!")
    def mouse_saiu(self, widget):
        self.rotulo.set_text("O mouse saiu de cima do botão!")
janela = CJanela()
gtk.main()
{% endhighlight %}

Vejam o resultado:

![Mouse sobre o botão](http://evaldojunior.com.br/blog/wp-content/uploads/2009/05/captura_de_tela-aula-19-sinais.png)

![Mouse saiu de cima do botão](http://evaldojunior.com.br/blog/wp-content/uploads/2009/05/captura_de_tela-aula-19-sinais-1.png)

Bem simples né? O legal do PyGTK é que na maioria das vezes, para aplicações mais simples, a sua preocupação será com o negócio e não com o PyGTK com em sí, já que sua manipulação não é algo tão complexo.

E essa foi a nossa aula de hoje, espero que tenham gostado e aprendido bastante.

Lição de Casa!

Pensou que ia ficar só nisso? Agora é a hora de botar a cabeça para funcionar! A lição de hoje é simples, façam uma janela com um rótulo e quatro botões: "**maximizar**", "**desfazer maximização**", "**tela cheia**" e "**desfazer tela cheia**". Quando clicados os botões devem fazer as devidas ações e o rótulo deve mostrar o status da janela, exemplo: "**Janela Maximizada**", "**Janela em Tela Cheia**", etc.

Bons estudos!
