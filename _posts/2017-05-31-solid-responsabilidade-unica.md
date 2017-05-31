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
mainimage: "solid_srp.png"
---

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
senha está incorreta. E ainda temos mais um problema neste código: Qual é o motivo
para a classe `Autenticador` saber da existência de um banco de dados através do
uso do repositório?

Vamos agora aplicar algumas mudanças no código para que este método tenha apenas
a responsabilidade de autenticar um usuário:

{% highlight php %}
<?php
class Autenticador
{
    public function autenticarUsuario(Usuario $usuario, string $senha): bool
    {
        return password_verify($senha, $usuario->getHashSenha());
    }
}
{% endhighlight %}

Conseguimos reduzir o método para apenas uma linha e agora o único motivo para
alterarmos seu código é o caso de mudanças na forma como a senha é verificada.

Legal, mas para onde foi o restante do código? Vamos colocar a parte que cria
a sessão em uma nova classe responsável apenas por isso:

{% highlight php %}
<?php
class Sessao
{
    public function iniciarSessao(Usuario $usuario): bool
    {
        $_SESSION["usuario"] = $usuario;
        $_SESSION["autenticacao"] = true;
        
        return true;
    }
    
    // ...
}
{% endhighlight %}

E por último podemos mover o restante do código para a o cliente que estava
usando a classe `Autenticador` no começo, que pode ser por exemplo um
`Controller` em uma estrutura **MVC**:

{% highlight php %}
<?php

use Form; // Apenas um exemplo para gerenciar os dados de formulários
use Redirect; // Exemplo para redirecionar
use Sessao; // A classe que criamos acima
use Autenticador;

class LoginController extends BaseController
{
    private $repositorioUsuarios;
    private $sessao;

    public function actionLogin()
    {
        $form = new Form($_POST);
        
        $email = $form->pegarValor("usuario", "");
        $senha = $form->pegarValor("senha", "");
        
        $usuario = $this->repositorioUsuarios->buscarPorEmail($email);

        if (null == $usuario) {
            $this->sessao->adicionarFlash("erro_login", "Usuário ou senha inválidos");
            return new Redirect("/login");
        }
        
        $autenticador = new Autenticador();

        if (! $autenticador->autenticarUsuario($usuario, $senha)) {
            $this->sessao->adicionarFlash("erro_login", "Usuário ou senha inválidos");
            return new Redirect("/login");
        }

        $this->sessao->iniciarSessao($usuario);
        $this->repositorioUsuarios->registrarLogin($usuario);

        return Redirect("/perfil");
    }
}
{% endhighlight %}

Repare que agora o cliente, no caso o `Controller`, é o responsável por
usar os diferentes módulos da aplicação. Como este cliente é um controller
de uma aplicação web, ele vai tomar conta de iniciar a sessão e de redirecionar
o usuário para a página correta em caso de falha ou de sucesso no login.

Repare também que eu tomei algumas "liberdades poéticas" e não iniciei os
objetos `$sessao` e `$repositorioUsuarios`.

Ainda podemos exercitar um pouco mais e separar mais as responsabilidades do
`Controller`, mas o controller é o cliente que precisa unificar o uso das
demais classes, então neste caso está de bom tamanho.

Agora a classe `Autenticador` tem apenas uma responsabilidade e pode ser
usada em diversos contextos, não apenas em uma aplicação web que conhece o
banco de dados.

A classe `Sessao` também pode ser usada em contextos diferentes e possíveis
alterações na forma como uma sessão é gerenciada serão feitas em apenas
um local.

Este tipo de exercício nos ajuda a entender melhor o Princípio da
Responsabilidade Única e por que ele  tão importante para a qualidade
do código.

Eu também gravei um vídeo falando sobre SOLID e sobre o Príncípio da
Responsabilidade Única. Veja aqui:

<iframe width="100%" height="400" src="https://www.youtube.com/embed/-Gw7_RCUEGQ" frameborder="0" allowfullscreen></iframe>

Agora você já pode começar a exercitar o primeiro princípio do SOLID em
seus projetos.

InFog
