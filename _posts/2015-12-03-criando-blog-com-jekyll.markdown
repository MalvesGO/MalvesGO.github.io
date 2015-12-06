---
layout: post
title:  "Como criei meu blog com Jekyll"
date:       2015-11-03 12:00:00
description: "Após passar algumas noites sem dormir para construir e configurar este blog com Jekyll, aqui está um tutorial de como você pode fazer o seu."
tags: [jekyll]
image:
  feature: jekyll.png
---


Hoje iremos aprender como criar um blog usando Jekill...
Mais por que Jekill???

Devido ser uma ferramenta open source de código livre e acessível a todos. Quer mais um motivo para usar????

<img class="center-block" src="http://images.tibiabr.com/hotnews/190402012_itsfree.jpg">

# Requisitos necessários:
* [Conta pessoal no Github](https://github.com/).
* 15 minutos do seu tempo
* Internet (é logico né...)

# Instalação

{% highlight javascript %}
sudo apt-get install git ruby jekyll
{% endhighlight %}

# Configurando

Antes de iniciar devemos configurar o git com nossos dados do Github

{% highlight javascript %}
git config --global user.name "nome-usuario"
git config --global user.email "email-usuario"
{% endhighlight %}

Agora criaremos um repositório git no qual iremos trabalhar localmente, o nome do repositório deve ser igual ao criado em sua conta no Github

{% highlight javascript %}
git init nome-usuario.github.io
{% endhighlight %}

Agora que vc já criou o diretório de seu blog, devemos encontrar um tema para Jekyll, recomendo esse repositório que possui vários templates prontos para uso.

{% highlight javascript %}
http://jekyllthemes.org/
{% endhighlight %}

Escolha um tema que lhe agrade e clone ele em seu repositório.

A estrutura ficará mais ou menos assim:

<pre><code> 
/_includes - Diretório do corpo das paginas
/_layouts - Diretório do corpo das paginas
/_posts - Diretório das postagens
/_css o /scss - Diretório dos arquivos CSS
/_img o /images - Diretório das imagens
/_config.yml - Arquivo de configuração
/404.md - Pagina de erro 404
/CNAME - Configurar um domínio
/about.md - Pagina about
/index.html Pagina inicial
</code></pre>

O arquivo _config.yml é um arquivo de configuração, informe os dados necessários.

Após realizar a configuração do arquivo, entre na pasta do seu projeto no terminal e escreva:

{% highlight javascript %}
jekyll serve
{% endhighlight %}

Abra seu navegador favorito e digite localhost:4000 ou 127.0.0.1:4000 e vai ver seu blog em funcionamento, agora ja pode começar a modificar o conteúdo de seu blog localmente através de seu editor favorito, no meu caso Sublime Text.

Quando decidir que seu blog esteja da forma desejada, podemos agora publica-lo no Github seguindo os seguintes comandos:

{% highlight javascript %}
git add --all
git commit -m "Blog criado"
git push -u origin master
{% endhighlight %}

Será necessário informar seu usuário e senha do github. 
Após seguir todos os passos ja podemos ver nosso blog publicado, acessando o endereço criado por você...

<pre><code> 
www.nome-usuario.github.io
</code></pre>

Espero que tenham gostado e agregado conhecimento...

Até a próxima


