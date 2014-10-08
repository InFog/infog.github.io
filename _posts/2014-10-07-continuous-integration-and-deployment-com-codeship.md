---
layout: post
title: Continuous Integration and Deployment com Codeship
categories:
- DevOps
tags:
- devops
- codeship
status: publish
type: post
published: true
---

Se você dormiu há dois anos e acordou agora, então você nao deve ter percebido
o movimento DevOps que vem acontecendo.

DevOps tenta aproximar os times de desenvolvimento e de operações, pois é bem
comum que esses times tenham visões diferentes do produto que juntos mantém no
ar.

Em geral a equipe de desenvolvimento quer manter tudo atualizado e quer entregar
mais e mais código. Já a equipe de operações quer estabilidade. O problema é que
o produto precisa evuluir e os times precisam andar juntos. Daí que surge o
movimento DevOps que tem muito a ver, pricipalmente, com a automação de
processos e padronização.

Em times que mantém esse cabo de guerra as coisas tendem a ser mais lentas. Fala
a verdade, quantos deploys você faz por mês? O quanto de problemas do tipo
"funciona na minha máquina" você já não passou? Ruim né?

Dentro do movimento DevOps existem duas siglas bastante conhecidas, o CI e o CD.

CI é Continuous Integration, ou Integração Contínua, onde em geral é rodado um
conjunto de testes a cada push realizado no repositório de código. Isso garante
que a qualidade do código irá se manter e os testes não devem quebrar.

Já o CD é o Continuous Deployment, ou Entrega Contínua, onde o código é empacotado
e entregue em produção também a partir de um push no repositório. Tudo automaticamente.

Mais uma vez, fala a verdade, qual é a dificuldade do seu time de entregar código
em produção? Quais são os passos? Se o seu passo a passo começa com "conectar no
servidor FTP", saiba que você está fazendo isso errado (ou não exatamente errado,
mas realmente atrasado e ineficiente).

Existem diversas formas de fazer CI e, mais para a frente, CD. Sim pois é necessário
começar pelo CI, pois não adianta entregar código quebrado.

Uma forma simples de fazer CI e CD seria executar scripts que rodam os testes e,
estando tudo ok, fazem a entrega em produção. Mas essa forma é complexa de manter,
principalmente se você tiver que administrar esses scripts em um servidor.

Uma outra forma muito conhecida é usando o [Jenkins](http://jenkins-ci.org/), que
é um automatizador de tarefas. Ele pode fazer praticamente qualquer coisa, mas
é bastante usado para CI e CD. O ruim é ter que configurar e hospedar o Jenkins.
A interface dele também não é das mais simpaticas. Tirando alguns detalhes o
Jenkins é uma ferramenta sensacional e deve estar na caixa de ferramentas de
praticamente todos que fazem automação de processos e DevOps.

Agora, uma outra ferramenta muito legal e bastante fácil de usar é o
[Codeship](https://www.codeship.io). Eu conheci o Codeship meio que sem querer
quando estava procurando por alguma opção de Jenkins hospedado. Então fiz uns
testes e acabei gostando bastante da ferramenta.

![Codeship Logo](/assets/images/codeship/logo.png)

No meu caso eu fiz a automação da entrega para um projeto em PHP. O meu cenário
era o seguinte:

- Projeto em PHP
- Dependências com Composer
- Testes com o PHPUnit (sem acesso à banco de dados)
- Empacotamento e deploy com Ant (via SSH)

O passo a passo para criar o projeto no Codeship foi muito fácil. A primeira
parte é a escolha do repositório:

![Escolha do repositório](/assets/images/codeship/1_source.png)

Na próxima página você escolhe a tecnologia utilizada para que ele já forneça
opções comuns para ela. Veja que escolhendo PHP ele já preenche o setup com a
instalação das dependências via Composer e o comando dos testes como **phpunit**:

![Setup e testes](/assets/images/codeship/2_tests.png)

Claro que você pode alterar esses campos para outras necessidades. Eles são
executados como um shell script, então são bem simples de alterar.

O próximo passo é adicionar o hook no Bitbucket (se o seu projeto estiver lá).
Depois é necessário fazer um commit e um push para que o primeiro teste seja
executado. Ele até sugere a adição da insígnia do Codeship no readme:

![Hook e insígnia](/assets/images/codeship/3_push.png)

Após executar os testes pela primeira vez (e fazer passar), configure como será
feito o deploy. O Codeship tem várias opções para deploy:

![Opções para deploy](/assets/images/codeship/4_deploy.png)

Mas a minha escolha foi **$script**, pois eu já tinha um script que empacota e
entrega usando o **Apache Ant**. Então minha a minha configuração para deploy
ficou assim:

```bash
ant deploy
```

Depois disso bastou fazer um novo push e ver a mágica acontecendo.

Teve uns passos adicionais como adicionar a chave SSH do usuário do Codeship no
meu servidor, com um usuário específico para deploy, mas no geral isso foi tudo.

Ah, algo que não posso deixar de dizer é que o atendimento do pessoal do Codeship
é sensacional! Se você precisar de algo é só chamar pelo twitter
[@codeship](https://twitter.com/codeship) que eles respondem rápido. Se você não
usa twitter, eles têm uma forma de atendimento pelo painel do site.

E o preço disso tudo? Para até 5 projetos e 100 builds por mês é grátis. Ou seja,
é uma ótima forma de começar a fazer CI e CD nos seus projetos pessoais e também
na empresa.

Você conhece alguma ferramenta legal para CI e CD? Deixa nos comentários ;)
