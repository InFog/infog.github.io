---
layout: post
title: Os problemas do Código Duplicado
categories:
- Desenvolvimento
- Melhores Práticas
tags:
- PHP
- Código Limpo
- Desenvolvimento
status: publish
type: post
published: true
---

Olá, pessoal!

Você já teve aquela sensação de *Déjà* vu enquanto trabalhava em algum trecho
de código? Infelizmente este é um sentimento bastante comum na nossa área e o
problema é que em algumas vezes não estamos necessariamente lidando com
duplicação de código e em outras sim.

![Wild Duplicate Code Appeared](/assets/images/wild-duplicate-code-appeared.jpg)

A duplicação de código é o problema mais comum apontado pelos *Bad Smells*, que
é uma coleção de más práticas que acontecem em desenvolvimento de software.

### Problemas causados pela duplicação de código

Um dos problemas é o aumento da base de código. Isso pode não ser um problema
para armazenamento, mas é um problema para o entendimento da aplicação. Guardar
1mb de código é barato, guardar 5mb é tão barato quanto, mas com certeza é
muito diferente a quantidade de trabalho para entender 100 linhas de código do
trabalho para entender 500 linhas.

A manutenção é prejudicada também pois em geral é necessário alterar vários
trechos de forma semelhante e fatalmente um trecho ou outro será esquecido.
Imagine fazer uma correção em um local de uma aplicação e descobrir que esta
correção precisa ser feita em mais 5 telas que usam uma lógica semelhante. É
chato e é bastante comum que se esqueça de algo. Afinal de contas somos humanos
e humanos esquecem.

### O que gera a duplicação de código?

Vários fatores podem levar à duplicação de código. Um deles é ter mais de um
desenvolvedor no mesmo projeto, que é muito comum. O problema é que dois ou
mais desenvolvedores podem estar trabalhando em funcionalidades parecidas e com
isso acabam criando código parecido ou que faz a mesma coisa. Quem nunca viu em
um mesmo sistema duas funções/classes/pacotes que fazem exatamente a mesma
coisa? Certamente essas funcionalidades poderiam ser unificadas e reutilizadas.

É claro que o problema também pode acontecer em projetos de apenas um
desenvolvedor. As vezes aquela preguicinha de isolar algo para reutilizar pode
custar horas e mais horas de manutenção no futuro.

As vezes uma empresa possui alguns softwares diferentes e também acaba gerando
duplicação entre esses softwares, pois quando se precisa de uma funcionalidade
parecida de um software em outro acaba-se por copiar o código e mudar alguma
coisa aqui e ali em vez de criar alguma espécie de biblioteca que pode ser
usada pelos dois softwares.

### Um exemplo simples de duplicação: Página de login

Este é um exemplo comum de problema de duplicação de código. Imagine que você
está desenvolvendo um site que contenha uma página de login. O primeiro
pensamento é que isso é bem fácil de resolver, pois basta criar uma página com
um formulário, adicionar umas validações em javascript, adicionar um backend
com validação dos dados e o login em si.

Mas depois de um tempo surge uma nova necessidade: Agora todas as páginas terão
um bloco de login no menu superior para facilitar a vida do usuário, assim ele
não precisa necessariamente ir para a página de login, basta digitar as
credenciais no bloco de login em qualquer página e pronto, está autenticado.

O problema é que com a nova necessidade vem também a vontade de simplesmente
copiar tudo o que é relacionado à primeira página de login e simplesmente colar
no novo bloco mudando uns nomes aqui e ali. Essa cópia parece inocente em um
exemplo pequeno assim, mas imagine algo copiado e colado em vinte partes
diferentes.

A cada pequeno trecho copiado se cria um pequeno débito técnico que vai
acumulando e acumulando até explodir, ou alguém pagar por ele.

### Identificando a duplicação de código

Identificar a duplicação não é uma tarefa muito simples, mas existem algumas
forma de se fazer este trabalho.

Uma das formas é a identificação manual, que pode acontecer sem querer quando
se esbarra em uma duplicação ou quando se procura por uma deliberadamente. O
problema é que quando se procura você tem que saber bem o que quer, pois você
já suspeita que existe algum tipo de duplicação.

Outra forma é usando ferramentas como *diff* e *meld*. O trabalho é mais
simples do que a busca totalmente manual, mas ainda é bastante trabalhosa e é
necessário saber bem o que se procura para poder comparar dois ou mais arquivos
diferentes em busca de possíveis duplicações.

E uma terceira forma é com o uso de ferramentas especializadas do tipo *CPD*
que são *Copy and Paste Detectors*.

No caso do PHP temos o [PHPCPD](https://github.com/sebastianbergmann/phpcp)
que consegue varrer todo um projeto e identificar sequências de linhas iguais.

Usar o PHPCPD é simples. Faça a instalação usando o PEAR ou o
[Composer](https://packagist.org/packages/sebastian/phpcpd) e navegue até o
diretório do projeto para executar o **phpcpd** passando como parâmetro o
diretório com a base da aplicação:

```bash
    $ phpcpd --progress application

    Processing files
    268 / 268 [++++++++++++++++++++++++++++++++++++++++++++++>] 100.00%

    Found 22 exact clones with 275 duplicated lines in 31 files:
    - application/models/Conta_receber.php:30-65
      application/models/Conta_pagar.php:30-65
```

Este é o resultado que eu obtive ao executar o PHPCPD em um projeto antigo meu.
Veja que ele encontrou 275 linhas duplicadas espalhadas por 31 arquivos
diferentes. Nada para se orgulhar...

O interessante é que ele está me mostrando que em algum momento do tempo foi
desenvolvida uma classe de **contas a receber** \(ou de contas a pagar\) e
depois alguém copiou toda a classe para **contas a pagar** e mudou uns nomes
aqui e ali e pronto, uma nova funcionalidade pronta, cheia de duplicação, mas
pronta. O ideal seria criar uma classe como **contas** com todo o código comum
entre as classes e então fazer a herança.

## Duplicações identificadas, e agora?

Após encontrar as duplicações é hora de aplicar os princípios do **DRY**, Don't
Repeat Yourself. DRY significa algo como *enxuto* em inglês.

O legal é que existe o contrário do DRY que é o **WET** que pode significar "We
Enjoy Typing" ou "Write Everything Twice". badum tssss.

Se você trabalha com programação procedural \(sem julgamentos aqui\) então você
pode utilizar técnicas como a criação de funções ajudantes que conseguem
extrair certas lógicas do software e centralizar. Um exemplo seria a formatação
de datas. Imagine que você exibe algumas datas formatas em sua aplicação:

```php
    <?php

    echo $data->format('d/m/Y');
    echo $data->format('d/m/Y');
    echo $data->format('d/m/Y');
    echo $data->format('d/m/Y');
    echo $data->format('d/m/Y');
```

Aqui eu coloquei uma linha abaixo da outra, mas imagine o uso desta linha em
vários locais. Parece inocente né? Mas de repente você precisa exibir a hora
junto ou tem alguma condicional. Neste caso seria necessário varrer todos os
usos para fazer a correção. Então poderia ser aplicado o uso de uma função que
faz a exibição e que poderia ter as lógicas adicionais embutidas:

```php
    <?php

    function formatarData(DateTime $data) {

        // Lógicas adicionais...

        return $data->format('d/m/Y');
    }

    // Depois o uso ficaria assim:

    echo formatarData($data);
    echo formatarData($data);
    echo formatarData($data);
    echo formatarData($data);
```

Quaisquer alterações feitas em `formatarData()` seriam automaticamente
espalhadas pela aplicação.

Ainda falando de programação procedural podem-se criar classes utilitárias que
teriam algum contexto além de funções, mas que seriam usadas de forma parecida.

Já para quem trabalha com orientação à objetos as possibilidades são bem
interessantes.

Uma destas possibilidades é a **Extract Method** que busca extrair
comportamentos semelhantes em métodos de uma classe para extraí-los para um
método separado que pode ser reutilizado. Veja este exemplo:

```php
    <?php

    public function someAction()
    {
        if (! $this->getUser()->canAccess('SomeSection', 'Admin')) {
            $this->redirect('/notauthorized');
        }
        if ($this->env->isDev()) {
            $this->enableProfiler();
        }
        // ...
    }

    public function anotherAction()
    {
        if (! $this->getUser()->canAccess('AnotherSection', 'Admin')) {
            $this->redirect('/notauthorized');
        }
        if ($this->env->isDev()) {
            $this->enableProfiler();
        }
        // ...
    }
```

O código acima é tipo um controller e tem as primeiras linhas de seus métodos
repetidas. Veja como ele poderia ficar com as repetições extraídas para métodos:

```php
    <?php

    private function checkPermissionAdmin($section)
    {
        if (! $this->getUser()->canAccess($section, 'Admin')) {
            $this->redirect('/notauthorized');
        }
    }

    private function enableProfiler()
    {
        if ($this->env->isDev()) {
            $this->enableProfiler();
        }
    }

    public function someAction()
    {
        $this->checkPermissionAdmin('SomeSection');
        $this->enableProfiler();
        // ...
    }

    public function anotherAction()
    {
        $this->checkPermissionAdmin('AnotherSection');
        $this->enableProfiler();
        // ...
    }
```

Bem melhor, não?

Outra técnica bem interessante é a **Extract Class** onde buscamos por
duplicações em mais de uma classe e extraímos o comportamento para uma nova
classe.

Vamos voltar ao exemplo anterior. Imagine que o seguinte trecho é repetido em
vários controllers:

```php
    <?php

    // Repetido em vários controllers
    private function checkPermissionAdmin($section)
    {
        if (! $this->getUser()->canAccess($section, 'Admin')) {
            $this->redirect('/notauthorized');
        }
    }

    // Repetido em vários controllers
    private function enableProfiler()
    {
        if ($this->env->isDev()) {
            $this->enableProfiler();
        }
    }
```

Agora vamos fazer a extração destes comportamentos para novas classes. Uma
delas será para controle de acesso:

```php
    <?php

    class Acl {
        public function checkPermission($section, $role)
        {
            $app = App::getInstance();
            if (! $app->getUser()->canAccess($section, $role)) {
                $app->redirect('/notauthorized');
            }
        }
    }
```

E a outra para o profiler:

```php
    <?php

    class Profiler {
        private function enableProfiler()
        {
            $app = App::getInstance();
            if ($app->env->isDev()) {
                $app->enableProfiler();
            }
        }
    }
```

E agora a utilização das novas classes nos controllers:

```php
    <?php

    public function __construct()
    {
        $p = new Profiler();
        $p->enableProfiler();
    }

    public function someAction()
    {
        $acl = new Acl();
        $acl->checkPermission('SomeSection', 'Admin');
        // ...
    }
```

E vou deixar mais uma técnica aqui: **Pull Up Field**.

Esta técnica consiste em encontrar atributos repetidos em diferentes classes e
fazer a extração para uma classe ancestral comum.

A figura abaixo mostra bem o exemplo, subindo o campo *name* das classes para
uma nova classe e então herdando:

![Pull Up Field](/assets/images/pull_up_field.gif)

Uma última dica: **Estude Design Patterns**. Padrões de projeto são bastante
focados em reutilização de código e evitar problemas como o da duplicação,
então vale a pena um estudo mais aprofundado.

Na última PHP Conference Brasil eu fiz uma palestra sobre esse assunto. Veja os
slides:

<iframe src="http://www.slideshare.net/slideshow/embed_code/28800185" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px 1px 0; margin-bottom:5px; max-width: 100%;" allowfullscreen></iframe>

Bons estudos!

InFog
