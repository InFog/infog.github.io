---
layout: post
title: Uma semana com o Fedora
categories:
- Distros
- Linux
- Fedora
tags:
- fedora
- linux
- distros
status: publish
type: post
published: true
---

Há uma semana eu resolvi fazer uma experiência de mudar de distro no meu
desktop. Eu uso o [Debian](http://debian.org/) há vários anos e de vez em quando
é bom sair um pouco da zona de conforto e experimentar algo diferente.

A distro da experiência deveria ser diferente do que estou acostumado, então os
diversos sabores de Debian logicamente estavam excluídos (Ubuntu, Mint, etc).

![Fedora Project](/assets/images/fedora-logo.png)

Fiz uma pesquisa rápida e acabei optando pelo [Fedora](http://fedoraproject.org).
Na verdade seria o [CentOS](http://centos.org), mas o Fedora é basicamente o
mesmo sabor RedHat, mas com pacotes mais atuais.

Então vamos aos passos do teste.

### O processo

O processo de instalação do Fedora foi bastante simples e eu consegui manter a
minha partição home com os dados intactos. O instalador é fácil de usar e eu só
me perdi um pouco na parte de seleção de teclado (ABNT), mas não foi difícil de
se achar. O problema é que depois de instalado ele voltou para o teclado padrão
americano (Eu instalei o sistema de inglês, deve ser por isso).

### Primeiro boot

Eu escolhi o Fedora com o ambiente gráfico [XFCE](http://xfce.org) e logo no
primeiro boot tive problemas. Por algum motivo as permissões da minha home
foram alteradas, então meu usuário não conseguia fazer login. O problema maior
é que no gerenciador de login isso não apareceu, então eu fazia login e em
seguida voltava para área de login sem nenhuma explicação.

Usei o root para investigar e descobri o problema de permissões. Fiz a correção
e o login funcionou normalmente.

### Softwares

A instalação de pacotes foi muito fácil usando o **yum**. O sistema é simples
de usar via terminal e nisso eu não tive muitos problemas, pois estou acostumado
ao **aptitude**.

Claro, não tive problemas com os pacotes padrão. Na hora de instalar pacotes
que não fazem parte dos repositórios oficiais a coisa não foi tão simples.

Um exemplo foi o Chromium, que não tem nos repositórios oficiais. Acabei
instalando de um repositório extra e sempre que eu digitava uma arroba ele
travava. O mesmo aconteceu com o Chrome. O Firefox funcionou muito bem.

Um software que foi fácil de instalar foi o Skype. Eu peguei a versão para
Fedora 16 em 32 bits e funcionou magicamente a instalação por uma interface
gráfica. Sem nem precisar resolver os problemas de dependências em 32 bits.

O ambiente de desenvolvimento foi simples de instalar, só tive que me achar nos
diretórios de configuração diferentes do Debian e tudo bem. Basicamente um
ambiente LEMP. Instalei um por um mesmo, sem algo tipo o Ansible para ajudar.

O Flash não funcionou e pronto. Fiquei sem vontade de experimentar mais formas
de fazer funcionar.

### Conclusão

No geral achei o Fedora bastante bom para usar no Desktop e também para
desenvolver. Tive lá meus probleminhas com um software ou outro mas gostei do
geral.

Ainda não foi o suficiente para me manter em outra distro, por isso mantive o
plano original de usar por apenas uma semana mesmo. Agora estou de volta ao
Debian :)

A experiência foi bem legal e eu recomendo à todos que usam GNU/Linux à tentar
também.

Você já fez algo assim? Quer deixar dicas para quem está pensando em usar outra
distro? Deixe sua opinião nos comentários.
