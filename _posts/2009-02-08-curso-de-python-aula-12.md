---
layout: post
title: Curso de Python - Aula 12 - Manipulando Arquivos
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

Hoje vamos tratar sobre a manipulação básica de arquivos. Vamos aprender a abrir um arquivo, gravar informações nele e também à ler informações dele.

Primeiro vamos ver como adicionar algum texto à um arquivo:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
arq = open('/tmp/lista.txt', 'w')
texto = """
Lista de Alunos
---
João da Silva
José Lima
Maria das Dores
"""
arq.write(texto)
arq.close()
{% endhighlight %}

É bem simples, não? Na linha 3 é aberto o arquivo "/tmp/lista.txt" em modo de gravação, caso o arquivo não exista ele será criado. Na quarta linha é definida a variável "texto" que, na linha 11, é incluída ao arquivo "/tmp/lista.txt", que corresponde à variável "arq". Na linha 12 o arquivo é fechado e então o programa termina. Aqui eu fiz um cat no arquivo e ele apareceu com as informações que estavam na variável "texto".

Pessoal, entendam que esta é uma das maneiras mais simples de guardar informações, todos os programas que fizemos até agora perdem as informações assim que terminados.

Também é possível escrever em arquivos usando listas no lugar de variáveis apenas em texto:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
arq = open('/tmp/lista.txt', 'w')
texto = []
texto.append('Lista de Alunos\n')
texto.append('---\n')
texto.append('João da Silva\n')
texto.append('José Lima\n')
texto.append('Maria das Dores')
arq.writelines(texto)
arq.close()
{% endhighlight %}

Isto vai gerar o mesmo arquivo que o exemplo anterior, a diferença é que deu mais trabalho, mas dependendo da situação este modo pode ser melhor.

Certo, agora que já sabemos como adicionar informações vamos aprender a ler informações:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
arq = open('/tmp/lista.txt', 'r')
texto = arq.read()
print(texto)
arq.close()
{% endhighlight %}

A função **read()** lê o arquivo todo de uma vez para uma variável. Isso pode ser legal em casos como este, em que eu quero apenas exibir a variável. Mas vejam este outro exemplo:

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
arq = open('/tmp/lista.txt', 'r')
texto = arq.readlines()
for linha in texto :
    print(linha)
arq.close()
{% endhighlight %}

A função **readlines()** retorna cada linha do arquivo como um elemento de uma lista. Tudo o que já sabemos sobre a manipulação de listas pode ser usado aqui =)

### Lição de Casa

Usando apenas os modos de abertura de arquivos mostrados nesta aula ('w' e 'r') faça o seguinte:

1. Grave esta lista em um arquivo (Copie para o seu código para isso):

- Gol
- Uno
- Palio
- EcoSport
- Clio
- Strada
- Golf

2. Inverta a ordem da lista e grave em um segundo arquivo.
3. Ordene a lista alfabeticamente em um terceiro arquivo.
4. Com a lista organizada faça a sua numeração em um quarto arquivo, assim:

- 1 -  Clio
- 2 - EcoSport...

Bons estudos.
