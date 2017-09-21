---
layout: post
title: Evite alterar a arquitetura do framework de desenvolvimento
categories:
- Frameworks
- Desenvolvimento
- Arquitetura
- Software
tags:
- Frameworks
- Desenvolvimento
- Arquitetura
- Software
status: publish
type: post
published: true
mainimage: "architecture.jpg"
---

No desenvolvimento de aplicações web, de sistemas de gestão à e-commerce e sites,
um framework é a base que vai ditar a arquitetura geral do projeto.

Um framework contém funcionalidades básicas e diretrizes que ajudam a equipe de
desenvolvimento à começar um projeto e mais para frente ajudam na manutenção e
também na adição de novos membros à equipe, pois uma nova pessoa na equipe que
já tenha conhecimento no framework pode se preocupar apenas em aprender as
regras do negócio, enquanto alguém sem experiência no framework pode contar com
documentação e até livros sobre o framework escolhido para o projeto.

Podemos dizer que um o framework correto para a aplicação sendo construída vai
suprir a maioria, se não todas, as necessidades do projeto. Mesmo assim ainda
podem surgir áreas onde um funcionamento um pouco diferente é necessário e como
temos acesso ao código fonte dos frameworks caímos na tentação de alterar partes
deste código para resolver o problema.

Uma possível solução para isso pode ser o uso de um pacote adicional que contém
a funcionalidade necessária e funciona em conjunto com o framework ou ainda o
desenvolvimento desse pacote separado que supra essa necessidade.

Outra forma é estendendo a classe que provê a funcionalidade e reimplementando
o que for necessário para a necessidade do projeto. Mas isso pode levar a problemas
para atualizar o framework futuramente, já que agora a sua aplicação contém uma
funcionalidade que depende não apenas do funcionamento, mas também da possível
implementação interna de uma classe do framework. Isso acaba quebrando o
encapsulamento pois a partir da extensão da classe o seu código passa a saber
muito sobre o funcionamento interno do framework.

Acredito que este problema seja menor atualmente (2017) do que era há alguns
anos, pois o uso do Composer incentiva a deixar a maioria do código do framework
e dos demais pacotes no diretório `vendor` e esse diretório deve ficar fora do
controle de versão e isso dificulta bastante fazer alterações permanentes no
funcionamento do framework.

Mesmo assim ainda é possível alterar arquivos como o `web/app.php` em aplicações
Symfony, pois mesmo sendo parte do framework este arquivo precisa ser versionado
e alterações no seu conteúdo são possíveis.

A minha dica aqui é: Não faça alterações no funcionamento interno do framework,
pois isso pode gerar mais problemas do que soluções no longo prazo.

Você ainda tem dúvidas de deve ou não usar um framework em seu projeto? Veja
o vídeo abaixo onde eu explico mais sobre o assunto:

<iframe width="100%" height="380" src="https://www.youtube.com/embed/GjBLxHANuy0" frameborder="0" allowfullscreen></iframe>

Happy coding!

Créditos da imagem de capa: [Flickr](https://www.flickr.com/photos/joeshlabotnik/3707230247/).
