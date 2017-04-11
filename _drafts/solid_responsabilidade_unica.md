---
layout: post
title: SOLID - O Princípio da Responsabilidade Única
categories:
- Desenvolvimento
- SOLID
- Código Limpo
tags:
- Desenvolvimento
- SOLID
- Código Limpo
status: publish
type: post
published: true
---
mainimage: "solid.png"

O Princípio de Responsabilidade única faz parte do SOLID, um conjunto de princípios
que têm como objetivo fazer com que um software seja mais simples de manter e
estender com o passar do tempo.

Este princípio diz que um módulo em uma aplicação deve ter apenas uma responsabilidade
e a maneira de identificar se um trecho de código tem apenas uma responsabilidade
é perguntando quais são os motivos para se alterar tal trecho. Se a resposta
contiver mais de um motivo isso é um sinal de que o trecho de código em foco
tem mais de uma responsabilidade.

Veja este exemplo:


{% highlight php %}
<!DOCTYPE html>
<html>
    <head>
        <title>Lista de pedidos</title>
    </head>
    <body>
        <?php

        if (isset($_GET["status"])) {
            $status = $_GET["status"];
        } else {
            $status = "pendentes";
        }

        ?>

        <h1>Lista de pedidos <?php echo $status; ?></h1>

        <?php
        $conexao = PDO("mysql:host=localhost;dbname=loja", "usuario", "senha");

        $query = <<<SQL
            SELECT * FROM `pedidos` WHERE `status` = "{$status}"
SQL;

        $resultado = $conexao->query($sql, PDO::FETCH_ASSOC);
        ?>

        <?php if (count($resultado) == 0) : ?>
            <p>Não há pedidos <?php echo $status; ?> no momento</p>
        <?php else: ?>
            <table>
                <thead>
                    <tr>
                        <th>Código</th>
                        <th>Cliente</th>
                        <th>Data</th>
                        <th>Forma de pagamento</th>
                    </tr>
                </thead>
                <tbody>
                    <?php foreach ($resultado as $pedido) : ?>
                        <tr>
                            <td><a href="pedido.php?codigo=<?php echo $pedido["codigo"]; ?>">
                                <?php echo $pedido["codigo"]; ?></a>
                            </td>
                            <td>
                                <?php
                                    $query = <<<SQL
                                        SELECT * FROM `clientes` WHERE `id` = {$pedido["cliente_id"]}
SQL;

                                    $cliente = $conexao->query($query, PDO::FETCH_ASSOC);
                                    echo $cliente[0]["nome"];
                                ?>
                            </td>
                            <td><?php echo date_format(new DateTime($pedido["data"]), "d/m/Y"); ?></td>
                            <td><?php switch ($pedido["forma_pagamento"]) {
                                case "1":
                                    echo "Boleto";
                                break;
                                case "2":
                                    echo "Cartão de crédito";
                                break;
                                case "3":
                                    echo "Débito em conta corrente";
                                break;
                                default:
                                    echo "Não definido";
                                break;
                            }
                            ?></td>
                        </tr>
                    <?php endforeach; ?>
                </tbody>
            </table>
        <?php endif; ?>
    </body>
</html>
{% endhighlight %}

Mas mesmo sendo um exemplo bem pequeno, este código tem diversas responsabilidades,
como receber dados através da requisição, fazer a comunicação com o banco de dados
e formatar o resultado para exibir no navegador. Sim, de maneira geral até dá
para dizer que este trecho tem uma "responsabilidade única", que é a exibição
dos dados no navegador, mas perceba que várias coisas precisam acontecer para
que a exibição dos dados seja possível.
