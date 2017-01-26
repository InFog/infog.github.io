---
layout: post
title: Curso de Python - Aula 14 - Orientação à Objetos
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

O curso de Python está bem legal, eu aprendi muito ensinando durante esse meses aqui no blog. Para vocês terem uma ideia eu consegui migrar o [GeSpeak](http://gespeak.googlecode.com) para [PyGTK](http://pygtk.org), e eu garanto que foi bem simples, tudo o que eu tive que fazer foi ter um pouco de paciência e entender bem a referência da biblioteca no site dela. Se tem uma coisa que eu aprendi com Python é que o código não precisa ser uma coisa de maluco para que funcione bem, Python deixa tudo muito simples e tem vários módulos que adicionam muitas funcionalidades extras. Enfim, se você está lendo isso é por que já deve ter visto as outras aulas e se você está acompanhando o curso também já deve ter percebido essa simplicidade. Agora chega de papo e vamos à aula.

O conceito de classes, objetos e afins é bem chatinho de entender no começo, mas depois que se entende é difícil de querer trabalhar de outra forma. Este assunto é bem genérico e também é suportado por várias linguagens de programação, por isso não vou escrever sobre isso, em vez disso vou usar o arsenal de informações livres que temos na grande rede chamada internet. Comecem lendo a página sobre [Orientação a Objetos na Wikipedia](http://pt.wikipedia.org/wiki/Poo). Tentem entender os conceitos do que é uma classe, um atributo, um método... Durante as próximas aulas vamos tratar deste assunto, ok?

Mas, como fazer uma classe em Python?

Vamos ver um exemplo de uma classe muito usada no ensino de orientação à objetos, a classe Aluno:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
class Aluno:
    __doc__ = """
        Classe de estudo
    """

    Nome = ''
    Serie = 0
    Notas = [0,0,0,0]

    def __init__(self, Nome, Serie):
        __doc__ = """
            Instancia da classe Aluno
            Parâmetros
            Nome: String com o nome do aluno
            Serie: Integer com a classe do aluno (1 a 9)
        """
        self.Nome = Nome
        self.Serie = Serie

    def pega_nome(self):
        __doc__ = """
            Esta função retorna uma string com o nome do aluno
        """
        return self.Nome

    def define_nota(self, Semestre, Nota):
        __doc__ = """
            Esta função serve para definir uma nota para um aluno
            Parâmetros
            Semestre: Integer de 1 a 4
            Nota: Float de 0 a 10
        """
        self.Notas[Semestre] = Nota

    def fecha_media(self):
        __doc__ = """
            Esta função função tira a média do aluno
            e returna um float
        """
        Notas = 0
        Media = 0
        i = 0
        while (i < 4):
            Notas += self.Notas[i]
            i += 1
        Media = Notas / 4
        return Media


# Iniciando o programa
nome = str(raw_input("Nome do aluno: "))
serie = int(raw_input("Serie: "))
aluno = Aluno(Nome=nome, Serie=serie)

i = 0

while (i < 4):
    nota = float(raw_input("Digite a %sª nota: " % str(i+1)))
    aluno.define_nota(Semestre=i, Nota=nota)
    i += 1

print("O aluno %s terminou o ano com média %f" % (aluno.pega_nome(),aluno.fecha_media()))
{% endhighlight %}

Vamos à explicação da classe...

Esta classe **Aluno** possui três atributos: Nome, Serie e Notas, uma string, um inteiro e uma lista. O método construtor da classe **__init__()** recebe o nome do aluno e também a série que ele está. A classe também tem o método **define_nota()** que recebe o semestre e a nota, vejam que aqui o aluno tem apenas uma nota geral e não por matéria. As funções **fecha_media()** e **pega_nome** são funções que retornam algum valor. Depois da definição da classe criamos uma **instância** dela chamada **aluno**, reparem que eu usei o mesmo nome mas com letras minúsculas, isso não é obrigatório, viu? Você pode dar qualquer nome às instâncias de uma classe, que também são conhecidas como **objetos**.

Classes nos ajudam muito em muitas tarefas, nesse caso poderiamos ter, por exemplo, trinta objetos da classe Aluno, cada um com as informações de um aluno.

### Lição de Casa!

Mais uma aula curta essa, não? Mas vamos discutir esse assunto ainda por algum tempo, enquanto isso vamos à lição de casa!

Se preparem, essa vai ser pesadinha! Construam uma classe chamada Aluno (podem aproveitar o código dessa aula), mas ela deve conter as notas de português, matemática e ciências. Para cada matéria são quatro notas. Então o programa começa e pede o nome do aluno e a classe dele, depois pede as quatro notas de cada matéria, depois disso ele tira as médias e monta um boletim em HTML (uma tabela mesmo), mostrando as notas abaixo de 5 na cor vermelha, além das médias. Se o aluno tiver até duas médias vermelhas o programa diz que ele está de recuperação, se tiver três vermelhas ele está reprovado!

Boa sorte!
