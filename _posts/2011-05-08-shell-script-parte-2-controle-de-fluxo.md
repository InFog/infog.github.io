---
layout: post
title: Shell Script - Parte 2 - Controle de Fluxo
categories:
- Aulas
- Blog
- Shell Script
tags:
- Aulas
- Bash
- shell script
status: publish
type: post
published: true
mainimage: "shell.jpg"
---

Esta é a segunda parte das aulas de **shell script**. [A primeira parte pode ser lida aqui](/aulas/blog/shell/shell script/2011/05/01/shell-script-parte-1-introducao.html). Essas aulas são focadas na sintaxe do **Bash**, então nem tudo pode funcionar da mesma maneira no sh, ksh...
E vamos ao que interessa, mais sobre **shell script**:

## Tomada de Decisões

Em toda linguagem de programação existe alguma estrutura para tomada de decisões. Essa estrutura em geral é feita através do comando "**if**". O comando "**if**" analisa de uma expressão é verdadeira e então executa um bloco de código, caso a expressão seja falsa pode ser executado, ou não, um outro bloco.

Em geral as linguagens de programação oferecem maneiras de verificar se um valor é igual, menor ou maior que outro. As formas mais comuns são:

- **==**: Igual à
- **!=** : Diferente de
- **&lt;** : Menor que
- **&gt;** : Maior que
- **&lt;=** : Menor ou igual à
- **&gt;=** : Maior ou igual à

Em shell script os mesmos testes são obtidos com:

- **-eq** : (equal) Igual à
- **-ne** : (not equal) Diferente de
- **-lt** : (less than) Menor que
- **-gt** : (greater than) Maior que
- **-le** : (less or egual) Menor ou igual à
- **-ge** : (greater or equal) Maior ou igual à

O uso do "**if**" em shell script é assim:

{% highlight sh %}
#!/bin/bash
if [ 2 -eq 4 ]
then
    echo "Esse echo nunca acontecerá"
fi
{% endhighlight %}

Repare que é necessário manter **espaços** entre os colchetes e os números, ou variáveis. O bloco após a palavra "**then**" será executado se a expressão dentro do "**if**" for verdadeira. O bloco "**if**" termina com a palavra "**fi**" que é "**if**" ao contrário. Essa é uma maneira simples de identificar o final de um "**if**" quando o encontramos.

As expressões acima são mais comuns para tratar números. Para fazer comparações com textos use:

- **=** : Igual à (isso mesmo apenas um sinal de igual)
- **!=** : Diferente de
- **-n** : String existe e não é vazia (apenas um operador)
- **-z **: String existe e é vazia (apenas um operador)

Veja um exemplo com Strings:

{% highlight sh %}
#!/bin/bash
echo "Digite seu nome: "
read nome
if [ -z $nome ]
then
    echo "Você não digitou seu nome!"
else
    echo "Olá, $nome"
fi
{% endhighlight %}

No script acima o "**if**" verifica se a variável **$nome** existe e está vazia, isso significa que o usuário não digitou o nome dele. A instrução "**read**" faz com que o shell leia alguma informação via teclado e retorne essa informação para a variável informada.

Também no script acima foi usada a palavra "**else**" que significa "**senão**". Esse bloco é executado quando o "**if**" retorna um valor falso.

## O Super IF do Shell

Mas o shell oferece mais opções para o "**if**" do que as linguagens de programação o fazem! Veja outras opções bem interessantes:

- **-s **: Arquivo existe, não vazio (apenas um operador)
- **-f **: Arquivo existe, não é um diretório (apenas um operador)
- **-d **: Diretório existe (apenas um operador)
- **-w **: Arquivo, com permissão de escrita (apenas um operador)
- **-r** : Arquivo, com permissão de leitura (apenas um operador)
- **-x **: Arquivo, com parmissão de execução  -x  (apenas um operador)

Veja um exemplo:

{% highlight sh %}
#!/bin/bash
arquivo="/tmp/meuLog.txt"
if [ -f "$arquivo" ]
then
    echo "Continuando log..." >> "$arquivo"
else
    echo "Criando log..." > "$arquivo"
fi
{% endhighlight %}

O script acima verifica se o arquivo "**/tmp/meuLog.txt**" existe. Caso exista ele continua o arquivo, colocando mais informações no final dele (redirecionador **&gt;&gt;**). Caso o arquivo não exista ele o inicia (com o redirecionador **&gt;**).

## IFs Aninhados

Chamamos de "**ifs aninhados**" as construções onde há um "**if**" dentro do bloco "**then**" ou "**else**" de outro "**if**":

{% highlight sh %}
#!/bin/bash
echo "Digite seu nome: "
read nome
echo "Digite sua idade: "
read idade
if [ -z $nome ]
then
    echo "Você não digitou seu nome."
else
    echo "Seu nome é $nome"
    if [ $idade -gt 10 ]
    then
        echo "Você tem mais que 10 anos."
    else
        echo "Você tem 10 anos ou menos."
    fi
fi
{% endhighlight %}

## IF Multilevel

Você pode fazer comparações em sequência, com o uso do "**elif**", desse jeito:

{% highlight sh %}
#!/bin/bash
echo "Digite um número"
read numero
if [ $numero -gt 0 ];
then
    echo "Número positivo"
elif [ $numero -lt 0 ]
then
    echo "Número negativo"
elif [ $numero -eq 0 ]
then
    echo "Número é zero"
else
    echo "O valor fornecido não é um número!"
fi
{% endhighlight %}

Além do comando "**if**", o shell oferece opções como "**case**" para controle de fluxo.

## O Comando Case

O comando "**case**" é usado para executar um bloco de código de acordo com o valor de uma variável. O comando "**case**" é interessante pois pode definir diversas opções diferentes sem usar uma estrutura com diversos comandos "**if**", "**elif**" e "**else**". Veja um exemplo:

{% highlight sh %}
#!/bin/bash
echo -n "O que deseja fazer? (A)lmoçar/(J)antar/(S)air? [A] "
read resposta
case "$resposta" in
    a|A|"")
        echo "Então tenha um bom almoço =)"
    ;;
    j|J)
        echo "Um jantar vai muito bem."
    ;;
    s|S)
        echo "Saindo..."
    ;;
    *)
        echo "Opção inválida"
    ;;
esac
{% endhighlight %}

O script acima exibe uma mensagem e então pede uma informação do usuário. O usuário vai digitar alguma letra e então o comando "case" entra em ação. Ele verifica qual valor foi digitado pelo usuário e executa os blocos de código relativos a cada opção. Primeira opção é a padrão, por isso ela é executada mesmo que o usuário não digite um valor.Cada bloco do case é iniciado por um valor que a variável analisada pode ter, ou vários valores, separados por um pipe. Os blocos são finalizados por uma sequência de dois caracteres 'ponto-e-vírgula' (;;).

## Conclusão

A estrutura de controle "**if**" do shell é bem interessante pois permite fazer diversas comparações entre valores e ainda oferece opções para lidar com o sistema de arquivos. O comando "**case**" pode tratar diversos valores de uma vez, o que acuda a manter o código mais limpo e organizado.

Até a próxima!
