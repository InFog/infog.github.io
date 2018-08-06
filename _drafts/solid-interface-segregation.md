---
layout: post
title: SOLID - O Princípio da Segregação de Interfaces
categories:
- desenvolvimento
- solid
- codigo limpo
tags:
- desenvolvimento
- solid
- codigo limpo
status: publish
type: post
published: true
mainimage: "image.png"
---

O Princípio da Segregação de Interfaces faz parte do SOLID, um conjunto de
princípios que têm como objetivo fazer com que um software seja mais simples de
manter e extender com o passar do tempo.

Este princípio diz que interfaces devem ser especializadas em vez de generalistas.
Isso é o mesmo que dizer que uma grande interface que tenta cobrir todas as
possibilidades de uma uma área é ruim e obriga as classes a implementarem métodos
que elas não precisam apenas para cumprir o contrato da interface.

Exemplo

Veja este exemplo de uma interface de conta em um banco:

```php
<?php

interface ContaInterface
{
    public function pegarSaldo(): float;

    public function depositar(float $valor, string $descricao): bool;

    public function sacar(float $valor, string $descricao): bool;

    public function deduzir(float $valor, string $descricao): bool;

    public function pegarExtrato(\DateTime $inicio, \DateTime $termino): MovimentacaoCollection;

    public function calcularRendimento(): float;

    public function calcularJuros(): float;
}
```

Esta interface tem o objetivo de cobrir o maior número de cenários possíveis
para contas de um banco. Pode-se implementar esta interface para os seguintes
tipos de contas:

- **conta simples**, que não permite ter saldo negativo e não tem rendimentos.
- **conta especial**, que permite ter saldo negativo e não tem rendimentos.
- **conta poupança**, que não permite ter saldo negativo e tem rendimentos.

Perceba que as classes implementando esta interface precisam implementar métodos
que elas não precisam ou nem podem ter.

Veja um exemplo de implementação de uma conta simples:

```php
<?php

class ContaSimples implements ContaInterface
{
    // ... Implemetação dos outros métodos

    public function calcularRendimento(): float
    {
        throw new \BadMethodCallException('A classe ContaSimples não tem rendimentos');
    }

    public function calcularJuros(): float
    {
        throw new \BadMethodCallException('A classe ContaSimples não tem juros');
    }
}
```

Neste exemplo a classe `ContaSimples` precisa obrigatoriamente implementar todos
os métodos da interface `ContaInterface`, mas estes métodos não fazem sentido
na regra de negócio deste tipo de conta, por isso exceções são usadas para
indicar que os métodos não devem ser chamados. Mesmo assim os métodos estão
presentes, ocupando espaço e causando confusão na cabeça de quem precisar fazer
a manutenção do código.

Veja mais um exemplo de uma classe que precisa de um dos métodos, a classe
`ContaEspecial`:

```php
<?php

class ContaEspecial implements ContaInterface
{
    private $taxaJuros = 0.01;

    // ... Implemetação dos outros métodos

    public function calcularRendimento(): float
    {
        throw new \BadMethodCallException('A classe ContaEspecial não tem rendimentos');
    }

    public function calcularJuros(): float
    {
        $juros = 0;

        if ($this->saldo < 0) {
            $juros = abs($this->saldo * $this->taxaJuros);
        };

        return $juros;
    }
}
```

Mas esta classe também não faz uso do método `calcularRendimento()`, que está
ali apenas para preencher o contrato da interface.

Escrever as classes que implementam a interface maior do que o necessário é
complicado, mas o uso dos objetos da classe pode ficar ainda mais complexo pois
serão necessários passos extras para entender se a classe é do tipo correto para
a operação sendo realizada. Um método que recebe um objeto do tipo `ContaInterface`
não pode confiar totalmente no tipo da classe e também fica confuso para as
pessoas que forem manter o código, pois um método que recebe `ContaInterface`
pode receber qualquer um dos três tipos de conta do nosso exemplo. Veja como
fica a implementação de um método que faz a aplicação dos juros em uma
`ContaEspecial`:

```php

class AplicadorJuros
{
    public function aplicarJuros(ContaInterface $conta): bool
    {
        $juros = 0;

        try {
            $juros = $conta->calcularJuros();
        } catch (\Throwable $e) {
            // O tipo de conta não tem juros
            // fazer o log do erro
            return false;
        }

        if ($juros > 0) {
            $conta->deduzir($juros, 'Juros aplicados em ' . date('d/m/Y'));
        }

        return true;
    }
}
```

Nada prático, certo?  Seguindo o princípio da segregação de interfaces devemos
criar as interfaces especializadas para cada tipo de conta, assim cada classe
concreta precisa implementar apenas as interfaces necessárias. Veja um exemplo
com as interfaces `ContaBaseInterface` e `ContaEspecialInterface`:

```php
<?php

interface ContaBaseInterface
{
    public function pegarSaldo(): float;

    public function depositar(float $valor, string $descricao): bool;

    public function sacar(float $valor, string $descricao): bool;

    public function deduzir(float $valor, string $descricao): bool;

    public function pegarExtrato(\DateTime $inicio, \DateTime $termino): MovimentacaoCollection;
}

interface ContaEspecialInterface extends ContaBaseInterface
{
    public function calcularJuros(): float;
}
```

Para deixar o exemplo mais simples eu coloquei as interfaces no mesmo "arquivo",
mas lembre-se de usar os namespaces do PHP e de ter apenas uma classe/interface
por arquivo.

Veja como agora temos duas interfaces, uma com o comportamento básico de uma
conta e uma com o que é necessário adicionar para a conta especial e que estende
a primeira interface. Mas como fica a classe `ContaEspecial` neste caso? Simples:

```php
<?php

class ContaEspecial implements ContaEspecialInterface
{
    private $taxaJuros = 0.01;

    // ... Implemetação dos outros métodos

    public function calcularJuros(): float
    {
        $juros = 0;

        if ($this->saldo < 0) {
            $juros = abs($this->saldo * $this->taxaJuros);
        };

        return $juros;
    }
}
```

Agora a classe conta especial implementa a interface `ContaEspecialInterface`
e não precisa mais implementar métodos que não fazem parte da sua regra de
negócio como o método `calcularRendimento()`.

Veja como fica então a implementação da classe `AplicadorJuros` dependendo da
interface especializada `ContaEspecialInterface`:


```php

class AplicadorJuros
{
    public function aplicarJuros(ContaEspecialInterface $conta): bool
    {
        $juros = $conta->calcularJuros();

        if ($juros > 0) {
            $conta->deduzir($juros, 'Juros aplicados em ' . date('d/m/Y'));
        }

        return true;
    }
}
```

Agora a classe cliente `AplicadorJuros` não precisa mais tratar casos especiais
onde o objeto recebido pode não ser uma `ContaEspecial`. Assim o código fica mais
limpo e fácil de entender, além de não quebrar as regras de negócio.

Para concluir podemos dizer que a segregação de interfaces é muito importante
pois nos permite focar em interfaces menores e mais especializadas e podemos
também passar a pensar mais em composição em vez de herança no design das classes,
que também é uma boa prática para o desenvolvimento de software.

Happy Coding!
