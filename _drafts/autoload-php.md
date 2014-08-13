---
layout: post
title: Como funciona o autoload do PHP
categories:
- PHP
- Desenvolvimento
tags:
- php
- desenvolvimento
- soudev
status: publish
type: post
published: true
---

Esse é um assunto um pouco batido, mas acho que vale a pena falar mais um pouco,
principalmente para quem está dando seus primeiros passos no PHP.

Os arquivos de código fonte em PHP são apenas arquivos de texto puro usando a
extensão php, ou nem isso se você não quiser, mas usar a extensão ajuda a
identificar o tipo de arquivo e ajuda os editores de textos e IDEs a saberem
que tipo de destaque de sintaxe devem usar.

Dito isso, é sabido que em PHP podemos usar algumas funções para incluir
código de outros arquivos em um arquivo que estamos criando. Essas funções são:

- *include*
- *include_once*
- *require*
- *require_once*

Imagine que temos uma estrutura assim:

- classes/
  - User.php
- index.php

No arquivo *classes/User.php* temos a classe *User* e o arquivo *index.php*
é utilizado como ponto de entrada da aplicação.

Agora, se quisermos usar a classe *User* dentro de index, faríamos algo assim:

```php
<?php

include "classes/User.php";

$u = new User();
```

Até aqui, sem muitos problemas, afinal é apenas uma classe. Agora, se temos,
por exemplo, 4 classes para carregar:

```php
<?php

include "classes/User.php";
include "classes/Customer.php";
include "classes/Order.php";
include "classes/Invoice.php";

$u = new User();
//...
```

Ok, começou a ficar chato. Esse é um trabalho para o *autoloader*. Esse recurso
faz exatamente o que o nome diz, carrega automaticamente uma classe quando ela
for requisitada.

Fazer um autoload é bastante simples. Crie uma função que receba um nome de
classe a ser carregado e então faça a inclusão do arquivo que a contém. Olha
como fica o exemplo:

```php
<?php

function my_loader($class)
{
    $file = __DIR__ . "/classes/{$class}.php";

    if (is_file($file)) {
        include $file;
    }
}

spl_autoload_register("my_loader");

$u = new User(); // Aqui o arquivo será carregado automaticamente
```

Simples, não? Neste caso criei a função *my_loader()* que recebe o nome de uma
classe que deve ser incluída. Dentro da função criei uma variável com o
caminho completo para o arquivo da classe. Depois apenas verifico se o arquivo
existe e então faço a inclusão.

Depois disso usei a função *spl_autoload_register()* para informar para o PHP
que quando ele não encontrar uma classe ele pode tentar achar essa classe
usando a minha função *my_loader()*.

Bem legal, né? E bem simples também.

Claro que essa é uma forma bem simplista de usar um autoloader e hoje em dia
os frameworks vêm com seus autoloaders e você precisa apenas manter os arquivos
com as classes nos lugares corretos para que tudo funcione.

Outra forma bastante usada hoje em dia, inclusive pelos frameworks, é com o
autoloader do [composer](http://getcomposer.org "Site do Composer").

Existem também alguns padrões da comunidade PHP para autoloaders. Dois famosos
são a [PSR-0](), que não é mais aconselhável, e a [PSR-4]() que é o padrão mais
atual e aceito para novos projetos. Então, se você quer saber mais sobre como
carregar, por exemplo, a classe *Awesome\\Service\\Twitter*, estude a *PSR-4*.

Você tem alguma dica legal sobre os autoloader? Deixe nos comentários :)

InFog
