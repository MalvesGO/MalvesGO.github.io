---
layout: post
title: Testando sua aplicação no Heroku
date: 2016-06-15 19:38:24
tags: [heroku]
description: Teste simples de app sendo testada no Heroku.
tags: [heroku, nodejs]
image:
  feature: heroku.png
---

Hoje iremos aprender a testar nossas apps no Heroku

Post traduzido e adaptado do blog: [Christian Haschek](https://blog.haschek.at/post/fb64fa)

Uma das coisas que mais me fascina no tema Internet das Coisas, é o poder combinar e utilizar um software que controla um hardware. Nesta experiência utilizaremos um Raspberry para criar um sistema de alarme para monitorar a porta de sua casa ou quarto de uma forma bem interessante.

Bem sem mais delongas, vamos ao que interessa.

# Passo 1

Neste projeto iremos utilizar:

* 1 Raspberry
* 1 Sensor reed switch
* 1 Cabo usb
* 1 resistor 10kΩ

# Montagem do cirquito

<img class="center-block" src="https://www.pictshare.net/thumbs/800x600_95c6149e18.jpg">

# Passo 2: O sensor reed switch

O sensor reed switch é um componente essencial para nosso projeto, devido o mesmo mudar o seu campo magnético quando sofre uma interferência de um íma. Então caso a porta feche o sensor irá detectar o status e enviar para nosso servidor Nodejs rodando na Raspberry.

<img class="center-block" src="http://www.usefulbulk.com/navionmods/housedoor/images/09_reed_switch_deta.jpg">

# Passo 3: Desenvolvimento do software

Com apenas algumas linhas de código veremos que é bastante simples realizar este projeto. No desenvolvimento do software usaremos o Nodejs por que acho muito simples o seu funcionamento e como um desenvolvedor web, me sinto bem confortável com a linguagem JAVASCRIPT. Além do mais, o gerenciador de pacotes NPM é uma mão na roda para instalarmos todos os módulos que precisaremos.

Neste exemplo iremos fazer o Raspberry enviar um email quando o status da porta for alterado. Este projeto pode servir de base para você desenvolver seus proprios projetos... Solte a imaginação e mão na massa.

Iniciaremos com a instalação de dois pacotes via NPM. No terminal digite esses comandos:

{% highlight javascript %}
npm install emailjs
npm install rpi-gpio
{% endhighlight %}

Com este código você terá que fazer algumas mudanças para utiliza-lo:

* Caso utilizar um pino diferente do apresentado nesse tutorial, mude para o que vocẽ escolheu. Altere o valor do portaPino.

* Altere as credenciais de seu e-mail (usuario, senha e host, caso não esteja usando o Gmail)

{% highlight javascript %}

var gpio = require('rpi-gpio');
var email   = require("emailjs/email");
var pinoPorta = 7; 
var server  = email.server.connect({
    user:    "your.username",
    password:"YourPassword",
    host:    "smtp.gmail.com",
    ssl: true});

var ultimoStatus = 1;

gpio.setup(pinoPorta, gpio.DIR_IN,readInput);

function readInput()
{
    gpio.read(pinoPorta, function(err, value){
        if(ultimoStatus!=value)
        {
                console.log(alteraStatus(value));
                server.send({ //sending email
                   text:    alteraStatus(value),
                   from:    "Porta <youremail@gmail.com>",
                   to:      "Destinatário <youremail@gmail.com>",
                   subject: alteraStatus(value)
                }, function(err, message) { console.log(err || message); });
        }
        ultimoStatus = value;
    });

  setTimeout(readInput,1000); // verificando a porta de segundo e segundo
}

function alteraStatus(s){
  if(s==0) return 'A porta esta aberta! '+getTime();
  else return 'A porta esta fechada! '+getTime();
}

function getTime(){
        var h = new Date().getHours();
        var m = new Date().getMinutes();
        var s = new Date().getSeconds();
        if(h <10) h = '0'+h;
        if(m <10) m = '0'+m;
        if(s <10) s = '0'+s;
        return h+':'+m+':'+s;
}
{% endhighlight %}

Para executar o códgio você terá que salvar esse arquivo com o nome "statusporta.js", em seguida abrir o terminal e digitar o seguinte comando:

{% highlight javascript %}
node statusporta.js
{% endhighlight %}

Se tudo funcionar corretamente e você abrir , em seguida, fechar sua porta você deve receber um e-mail, verifique sua caixa de entrada.

Espero que tenham gostado e agregado conhecimento...

Até a próxima


