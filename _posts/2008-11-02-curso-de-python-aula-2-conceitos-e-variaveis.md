---
layout: post
title: Curso de Python - Aula 2 - Conceitos e variáveis
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

Olá! Está na hora de começar o <a title="Aulas de Python - Aula 1 - A Proposta" href="http://evaldojunior.com.br/blog/?p=232" target="_blank">Curso de Python</a>!

É importante lembrar que todas as aulas serão feitas utilizando o sistema operacional GNU/Linux, o Python funciona em plataformas Unix (FreeBSD, Solaris), Windows e Mac OS X. Se você quiser fazer as aulas em outro ambiente fique à vontade, mas que fique claro que eu posso não resolver alguma dúvida sua referente ao seu sistema.

Como rodar os exemplos?

Utilize o editor de textos de sua preferência para fazer os exemplos (vim, kate, gedit, joe, nano). Lembre-se de utilizar um editor de textos puro e não um editor rich como o OpenOffice Writer ou o MS Word.

Depois de digitar os códigos basta salvar o arquivo e lhe dar permissão de execução (no Linux/OSX), assim:

```sh
$ chmod +x exemplo1.py
```

A extensão **.py** utilizada aqui é apenas por convenção, os arquivos no Linux não precisam necessariamente de uma extensão. Após dar a permissão de execução basta rodar o script assim:


```sh
$ ./exemplo1.py
Ola Mundo!
$
```

No exemplo acima o Python apenas imprimiu "Ola Mundo!" e saiu.

Uma outra forma de rodar os exemplos é usando o **IDLE**, que é o editor padrão que vem instalado com o Python. Neste caso, basta salvar o arquivo e usar a tecla &lt;F5&gt; para executar o programa.

Primeiro alguns conceitos básicos, sem muita enrolação, se você quiser saber com mais detalhes a história do Python a galera da Wikipedia tem um [artigo](http://pt.wikipedia.org/wiki/Python) bem legal.

O Python é uma linguagem de programação interpretada e orientada à objetos, o que significa que você não precisa compilar o fonte, basta executa-lo com o interpretador, a orientação à objetos veremos mais à frente neste curso.

### O Interpretador Interativo

Um recurso muito legal do Python é o seu interpretador interativo, nele você vai digitando os comandos e recebendo as respostas na hora, é muito legal para testar códigos e saber como a linguagem trabalha em alguns casos.

Para ligar o interpretador basta chama-lo no terminal, ou procurar o programa no menu do seu sistema.

```sh
$ python
Python 2.5.2 (r252:60911, Sep 29 2008, 21:15:13)
[GCC 4.3.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Ali no **prompt** (os sinais &gt;&gt;&gt;) é onde você começa a digitar seu código para ser interpretado instantaneamente. Exemplo:

```sh
>>> print("Olá Mundo!")
Olá Mundo!
>>>
```

Ele imprimiu "Olá Mundo!" na tela e voltou ao **prompt** para receber novos comandos, legal né?

Durante o curso não será utilizado o interpretador interativo do Python, sempre faremos arquivos de texto com o código, mas se você quiser usar o interpretador para tirar alguma fica à vontade =)

### Variáveis

Então vamos às nossas primeiras linhas de programação com o Python. Muitos textos sobre Python começam mostrando como é legal utilizar o interpretador dele como uma calculadora, mas aqui nós vamos começar com variáveis de texto.

Uma variável é um espaço em memória utilizado para guardar alguma informação, quer ver um exemplo?

```python
#!/usr/bin/env python

texto = "Oi, como vai você?"
print(texto)
```

Explicando o código: A primeira linha diz que o código deverá ser interpretado pelo Python, dessa forma podemos roda-lo como qualquer outro programa (sem chamar o interpretador na linha de comando).  Na segunda linha nós reservamos um espaço em memória e lhe damos o nome de **texto**, dentro deste espaço guardamos a informação **"Oi, como vai voce?"**, e a terceira linha utiliza uma função do Python chamada **print**, esta função imprime na saída padrão (em geral o monitor) o conteúdo de alguma variável. Simples né? Digite o código, salve, dê permissão de execução e execute (abaixo eu chamei o arquivo de aula2_texto.py, mas você pode dar o nome que quiser).

```sh
$ chmod +x aula2_texto.py
$ ./aula1.py
Oi, como vai voce?
$
```

Deu tudo certo aí? Creio que sim =)

Agora vamos exibir um texto com 3 linhas sendo que cada linha estará em uma variável:

```python
#!/usr/bin/env python
linha1 = "Aulas de Python do InFog"
linha2 = "Com dicas e exercícios!"
linha3 = "Entre nessa você também!"
print(linha1 + linha2 + linha3)
```

Agora, rodando esse código teremos:

```sh
$ ./aula2_texto3.py
Aulas de Python do InFogCom dicas e exercicios!Entre nessa voce tambem
$
```

Certo, aqui foi usado o operador + (mais) para "concatenar" (juntar, uma no final da outra) os valores das variáveis. O problema é que foi tudo exibido na mesma linha, e não era isso que queríamos certo? Para resolver essa questão vamos simplesmente adicionar um caractere especial no fim dos dois primeiros textos (variáveis **linha1** e **linha2**), um caractere de final de linha, no Linux esse caractere é o **\n**, então o código ficará assim:

```python
#!/usr/bin/env python
linha1 = "Aulas de Python do InFog\n"
linha2 = "Com dicas e exercícios!\n"
linha3 = "Entre nessa você também!"
print(linha1 + linha2 + linha3)
```

```sh
$ ./aula2_texto3.py
Aulas de Python do InFog
Com dicas e exercicios!
Entre nessa voce tambem
$
```

Agora sim! Uma variável por linha =)

O exemplo acima foi para mostrar como concatenar **strings** (strings são variáveis do tipo texto), agora vou mostrar duas formas muito mais simples de se obter o mesmo resultado, porém com apenas uma variável:

Primeiro usando o caractere especial **\n**:

```python
#!/usr/bin/env python
print("Oi eu sou um texto\ndividido em\n3 linhas!")
```

Neste exemplo o texto é dividido em 3 linhas usando o caractere especial **\n** em linha.

Agora usando um outro recurso muito legal que são as aspas tríplices:

```python
#!/usr/bin/env python
texto = """
Eu também sou um
texto dividido
em 3 linhas
"""
print(texto)
```

Neste exemplo foram utilizadas as aspas tríplices, elas funcionam assim: Você coloca as três aspas e começa a digitar seu texto, no final basta fechar com as três aspas novamente.

###Lição de Casa

A lição de casa de hoje é bem fácil, faça um script Python que me mostre a mensagem abaixo das três formas mostradas aqui, uma linha por variável, todas as linhas em uma variável e usando as aspas tríplices.

Mensagem que deve ser exibida:

```sh
Com grandes poderes vêm grandes responsabilidades.
O bem de um e o bem de todos.
Sou o que sou devido ao que todos somos.
```

As três formas devem estar em apenas um script Python.

InFog
