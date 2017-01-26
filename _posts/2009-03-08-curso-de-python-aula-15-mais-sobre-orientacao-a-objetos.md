---
layout: post
title: Curso de Python - Aula 15 - Mais sobre Orientação à Objetos
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

Na [aula anterior](/aulas/python/2009/03/01/curso-de-python-aula-14-orientacao-a-objetos.html) vimos um básico sobre orientação à objetos e parece que o assunto foi um pouco mais complicado para vocês. Pessoal, vocês não podem ter medo de resolver os problemas, mesmo que pareça muito difícil tentem, só assim se aprende. E caso tenham dúvidas procurem o fóruns de discussão na internet. O importante é não desistir, se você quer mesmo aprender Python/programação.

Nesta aula veremos como "proteger" atributos de uma classe.

Este tipo de proteção é chamada de "atributos privados" e é algo muito comum na orientação à objetos. neste caso os atributos ou métodos privados de uma classe podem ser alterados ou chamados somente por funções da própria classe. O problema é que o Python não exatamente oferece essa "privacidade", mas existem convenções para isso, vejam no exemplo:


{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
class Aluno:
    __doc__ = """
        Classe de estudo
    """
    # Todos os atributos são privados...
    __Nome = ''
    __Serie = 0
    __Notas = [0,0,0,0]

    def __init__(self, Nome, Serie):
        __doc__ = """
            Instancia da classe Aluno
            Parâmetros
            Nome: String com o nome do aluno
            Serie: Integer com a classe do aluno (1 a 9)
        """
        self.__Nome = Nome
        self.__Serie = Serie

    def pega_nome(self):
        __doc__ = """
            Esta função retorna uma string com o nome do aluno
        """
        return self.__Nome

    def define_nota(self, Semestre, Nota):
        __doc__ = """
            Esta função serve para definir uma nota para um aluno
            Parâmetros
            Semestre: Integer de 1 a 4
            Nota: Float de 0 a 10
        """
        self.__Notas[Semestre] = Nota

    def define_nome(self, Nome):
        __doc__ = """
            Função para "renomear" o aluno
        """
        self.__Nome = Nome

    def fecha_media(self):
        __doc__ = """
            Esta função função tira a média do aluno
            e returna um float
        """
        Notas = 0
        Media = 0
        i = 0
        while (i < 4):
            Notas += self.__Notas[i]
            i += 1
        Media = Notas / 4
        return Media

# Iniciando o programa
nome = str(raw_input("Nome do aluno: "))
serie = int(raw_input("Serie: "))
aluno = Aluno(Nome=nome, Serie=serie)
# A linha abaixo não vai alterar mais o nome do aluno
aluno.__Nome = "José Nascimento"
# Mas a linha abaixo altera
aluno.define_nome("João da Silva")
i = 0
while (i < 4):
    nota = float(raw_input("Digite a %sª nota: " % str(i+1)))
    aluno.define_nota(Semestre=i, Nota=nota)
    i += 1
print("O aluno %s terminou o ano com média %f" % (aluno.pega_nome(),aluno.fecha_media()))
{% endhighlight %}

Como vocês podem ver agora o atributo "**Nome**" é chamado de "**__Nome**", com isso o Python evita que ele seja alterado fora da classe.

## Propriedades

Vamos ao exemplo!

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
class Aluno:
    __doc__ = """
        Classe de estudo
    """
    # Todos os atributos são privados...
    __Nome = ''
    __Serie = 0
    __Notas = [0,0,0,0]

    def __init__(self, Nome, Serie):
        __doc__ = """
            Instancia da classe Aluno
            Parâmetros
            Nome: String com o nome do aluno
            Serie: Integer com a classe do aluno (1 a 9)
        """
        self.__Nome = Nome
        self.__Serie = Serie

    def pega_nome(self):
        __doc__ = """
            Esta função retorna uma string com o nome do aluno
        """
        return self.__Nome

    def define_nota(self, Semestre, Nota):
        __doc__ = """
            Esta função serve para definir uma nota para um aluno
            Parâmetros
            Semestre: Integer de 1 a 4
            Nota: Float de 0 a 10
        """
        self.__Notas[Semestre] = Nota

    def define_nome(self, Nome):
        __doc__ = """
            Função para "renomear" o aluno
        """
        self.__Nome = Nome

    def fecha_media(self):
        __doc__ = """
            Esta função função tira a média do aluno
            e returna um float
        """
        Notas = 0
        Media = 0
        i = 0
        while (i < 4):
            Notas += self.__Notas[i]
            i += 1
        Media = Notas / 4
        return Media

    def pega_dados(self):
        __doc__ = """
            Esta função retorna os dados do aluno, nome e série
        """
        return "Aluno: %s\nSérie: %i" % (self.__Nome, self.__Serie)

    dados = property(pega_dados)

# Iniciando o programa
nome = str(raw_input("Nome do aluno: "))
serie = int(raw_input("Serie: "))
aluno = Aluno(Nome=nome, Serie=serie)
# Mostrando os dados do aluno...
print(aluno.dados)
i = 0
while (i < 4):
    nota = float(raw_input("Digite a %sª nota: " % str(i+1)))
    aluno.define_nota(Semestre=i, Nota=nota)
    i += 1
print("O aluno %s terminou o ano com média %f" % (aluno.pega_nome(),aluno.fecha_media())
{% endhighlight %}

Vejam que a propriedade "**dados**" (linha 63) chama uma função, isso é muito útil, pois, neste caso, nos poupa chamar uma função. Na verdade as propriedades tem mais usabilidade do que apenas isso, então fica a dica de estudo para vocês.

Acho que na próxima aula já podemos ver um pouco de GTK, o que conhecemos sobre classes até agora já é o suficiente.

### Lição de Casa!

O exercício de hoje vai fazer vocês pensarem bastante, lembram do exercício da última aula? Pois então, eu quero que vocês refaçam este exercício, mas desta vez com os atributos privados, vocês podem usar propriedades se quiserem, mas não são obrigados. Mas desta vez o programa deve ter um pequeno menu que pergunta o que o usuário quer fazer, as opções são: "opção 1: cadastrar aluno", "opção 2: definir notas", "opção 3: ver boletim", "opção 4: ver lista de alunos". Ou seja, vou poder cadastrar quantos alunos eu quiser com a opção 1. Na opção 2 o programa deve mostrar a lista de alunos e perguntar para qual que serão definidas as notas. Na opção 3 a mesma coisa, mas ao escolher um aluno o boletim dele deverá ser exibido. E a opção 4 só mostra uma lista simples, com todos os alunos.

Boa sorte! Este está bem divertido.
