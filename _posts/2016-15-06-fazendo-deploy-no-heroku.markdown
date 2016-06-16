---
layout: post
title: Como fazer deploy de Apps para o Heroku
date: 2016-06-15 19:38:24
tags: [heroku]
description: Como fazer deploy de Apps para o Heroku.
tags: [heroku, nodejs]
image:
  feature: heroku.png
---

Como fazer deploy de Apps para o Heroku

Heroku é uma plataforma de serviço em nuvem (PaaS) suportando várias linguagens de programação. Heroku é de propriedade da Salesforce.com . Heroku, uma das primeiras plataformas de nuvem , já está em desenvolvimento desde junho de 2007, quando suportava apenas a linguagem de programação Ruby , mas, desde então, adicionou suporte para Java , Node.js , Scala , Clojure e Python e PHP. O sistema operacional de base é Debian ou, no mais recente, o Debian-based Ubuntu.

### Continuando com o tutorial, vou levar em consideração que você possui:

* O Git instalado.
* O Ruby instalado.
* O Node.js instalado.
* Já ter lido o Getting Started with Heroku.
* Uma conta no Heroku (mais que necessário).
* Ter o Heroku toolbelt ou a gem Heroku instalado.

Como sou adepto do software livre estou escrevendo esse tutorial utilizando o Ubuntu, porém você pode escolher o sistema operacional de sua escolha.

Para saber se o Heroku está funcionando Ok, abra um terminal e digite:

{% highlight html %}
heroku –version
{% endhighlight %}

O console nos exibirá uma mensagem

<img src="/images/heroku/heroku-version.png" class="img-responsive center-block">

Agora vamos criar o nosso app, não vou criar nada muito complexo aqui, somente um exemplo de leitura de HTML estático com o Node.js. Para agilizar o processo, coloquei o código no github, vá até o projeto e clone o mesmo para o seu PC.

Duas coisas que você deve se atentar é:

 * Obrigatório o arquivo package.json, onde eu listo a engine que será utilizada, dependências, esse tipo de coisa.

 * Arquivo Procfile, é ele que vai indicar o processo que deve rodar, sem ele não funciona.

Iniciando o deploy de nossa aplicação

Abra o seu terminal, e vá até a pasta onde você clonou o projeto, siga os passos a seguir:

Crie um repositório git com: git init

Ainda escrevendo o tutorial


{% highlight javascript %}
npm install emailjs
npm install rpi-gpio
{% endhighlight %}


Espero que tenham gostado e agregado conhecimento...

Até a próxima


