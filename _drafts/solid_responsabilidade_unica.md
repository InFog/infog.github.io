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
extender com o passar do tempo.

Este princípio diz que um módulo em uma aplicação deve ter apenas uma responsabilidade
e a maneira de identificar se um trecho de código tem apenas uma responsabilidade
é perguntando quais são os motivos para se alterar tal trecho. Se a resposta
contiver mais de um motivo isso é um sinal de que o trecho de código em foco
tem mais de uma responsabilidade.

Veja este exemplo em PHP:

{% highlight php %}
<?php
class Autenticador
{
    private $repositorioUsuarios;

    public function autenticarUsuario(string $email, string $senha): bool
    {
        $usuario = $this->repositorioUsuarios->buscarPorEmail($email);

        if (null == $usuario) {
            return false;
        }

        if (! password_verify($senha, $usuario->getHashSenha())) {
            return false;
        }

        $_SESSION["usuario"] = $usuario;
        $_SESSION["autenticacao"] = true;

        $this->repositorioUsuarios->registrarLogin($usuario);

        return true;
    }
}
{% endhighlight %}

Agora vamos analisar este trecho de código. Temos uma classe chamada
`Autenticador` com um método `autenticarUsuario()`. Tudo parece bastante simples
e o método parece ter apenas uma responsabilidade: Autenticar um usuário
através de uma combinação de email e senha.

Mas leia atentamente o que o método `autenticarUsuario()` está fazendo:

- Verifica se o usuário existe no banco de dados;
- Verifica se a senha é válida;
- Cria os dados de sessão;
- Registra um histórico de login.

Até é possível argumentar de que isso ainda é uma responsabilidade única
chamada "autenticar um usuário", mas quando tentamos fazer a pergunta "Quais
são os motivos para se alterar este trecho de código?" teremos mais de uma
resposta:

- Adicionamos um campo `ativo` no cadastro do usuário e apenas usuários ativos podem se autenticar;
- Por motivos de segurança o método de verificação da senha foi alterado;
- Os dados de sessão serão armazenados de uma maneira diferente;
- O método vai ser usado para autenticar usuários do aplicativo Android onde não há sessão.

Além disso os valores retornados por esse método podem significar diferentes
coisas, um retorno `false` pode significar que o usuário não existe ou que a
senha está incorreta.
