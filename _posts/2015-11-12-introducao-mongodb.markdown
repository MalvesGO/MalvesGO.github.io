---
layout: post
title: Introdução ao MongoDB
date: 2015-11-03 09:38:24
tags: [mongodb]
description: "MongoDB é um banco orientado a documentos open-source que permite alta performance, alta disponibilidade e escalabilidade automática. - 10gen."
image:
  feature: mongodb.png
---

Recentemente tive a oportunidade de conhecer e utilizar o Mongodb em um projeto pessoal de Internet das Coisas, e isso me motivou a relacionar os principais comandos básicos do Mongodb, tendo como principal finalidade ajudar quem está iniciando com esse novo banco de dados NoSQL.

#Instalação do MongoDB

A documentação do MongoDB é bem completa e detalhada, sendo assim, vamos listar abaixo alguns links diretos para você conseguir instalar em seu computador.

[Instalando MongoDB no Windows](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/)

[Instalando MongoDB no Linux](https://docs.mongodb.org/manual/administration/install-on-linux/) 

[Instalação do MongoDB no Mac](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/)

Se você seguiu os passos corretamente, meus parabens... Já temos o Mondodb instalado e pronto para executar nossos comandos.

#Tudo pronto para começarmos????

Abra o seu terminal e execute o seguinte comando:

{% highlight javascript %}
mongod
{% endhighlight %}

ou

{% highlight javascript %}
sudo service mongod start
{% endhighlight %}

<img src="/images/img-posts/iniciarServer.png" class="img-responsive center-block">

<h1 class="text-center">Observação importante:</h1>

Se vocẽ por acaso fechar o terminal, o serviço do Mongodb irá cair, então para que tudo ocorra perfeitamente abra outra janela do terminal para prosseguir com os proximos comandos. :)

#Como se conectar ao MongoDB?

Para conectar no MongoDB, basta executar o comando abaixo:

{% highlight javascript %}
mongo
{% endhighlight %}
    
Simples!!!!  Estamos conectado no MongoDB. :-)

#Como criar um db (database)?

Para criarmos uma nova base de dados o comando é:  <strong>use nomeDaSuaBase</strong>

Exemplo: 

{% highlight javascript %}
use meuBanco
{% endhighlight %}

<img src="/images/img-posts/criarDbs.png" class="img-responsive center-block">


#Como listar todas as databases?

Para listarmos todas as databases o comando é:  <strong> show dbs</strong>

<img src="/images/img-posts/showDbs.png" class="img-responsive center-block">

#Como acessar um determinado database?

Criei um database chamado meuBanco, para conectarmos a ele executamos o seguinte comando:

{% highlight javascript %}
use meuBanco
{% endhighlight %}

Perai??? Para conectarmos ao db usamos o mesmo comando para criar o database???

Sim amiguinhos... Porém se atentem para não acabar criando outros dbs e acabar se confundindo na hora de usa-los, por exemplo meuBancoo (letra duplicada "o").

#Como saber em qual db estou usando no momento?

Quando quisermos saber em qual db estamos conectados no momento usamos o comando: 

{% highlight javascript %}
db
{% endhighlight %}

#Como criar uma collection?

Antes de tudo verifique se esta conectado no db que criamos <strong>meuBanco</strong>, após isso para criarmos uma collections usamos o comando <strong>db.createCollection(nomeDaCollection)</strong>.


Vamos criar a collection usuarios.

{% highlight javascript %}
db.createCollection( "usuarios" )
{% endhighlight %}

Após a execução do médoto, você terá o seguinte retorno de sucesso:

{% highlight javascript %}
{ "ok" : 1 }
{% endhighlight %}

<img src="/images/img-posts/createCollections.png" class="img-responsive center-block">

Agora temos nossa estrutura de dados.

#Como listar todas collections criadas na base de dados?

Para realizar esse procedimento usamos o comando:

{% highlight javascript %}
show collections
{% endhighlight %}    

<img src="/images/img-posts/showCollections.png" class="img-responsive center-block">


#Como inserir (insert) dados em nossa (collection) no MongoDB?

Para inserir os dados em uma collection, utilizamos o método, db.nomeDaCollection.insert(jsonQueVoceQuerInserir).

Agora vamos inserir uma pessoa na coleção usuarios:

{% highlight javascript %}
db.usuarios.save( { nome:"Marcelo" , sobrenome:"Alves" } )
{% endhighlight %} 	

Agora vamos inserir uma pessoa com um telefone na mesma coleção:

{% highlight javascript %}
db.usuarios.save( { nome:"João" , sobrenome:"Silva" , telefone:"1234-5678" } )
{% endhighlight %}

ou também podemos inserir uma pessoa com vários telefones criando um array para o campo:

{% highlight javascript %}
db.usuarios.save( { nome:"Jean" , sobrenome:"Suissa" , telefone: [ "9898-9898" , "1234-5678" ] } )
{% endhighlight %}

Caso a collection usuarios não existir, ela será criada automaticamente.

#Agora vamos listar as pessoas

{% highlight javascript %}
db.usuarios.find()
{% endhighlight %}

Onde será listados todos os documentos armazenados na coleção.

<img src="/images/img-posts/find.png" class="img-responsive center-block">

Podemos observar que o campo "_id", foi criado automaticamente, ele é um identificador único de cada documento.

#Filtros

Podemos filtrar a busca fornecendo um objeto, no caso iremos buscar por todas as pessoas com o nome Marcelo

{% highlight javascript %}
db.usuarios.find( { nome:"Marcelo" } )
{% endhighlight %}	

Como todas as buscas existem várias opções de filtragem podemos começar com os clássicos:

{% highlight javascript %}
db.usuarios.find( { idade : { "$gt" : 18 } } ) //maior que 
db.usuarios.find( { idade : { "$lt" : 18 } } )//menor que 
db.usuarios.find( { idade : { "$gte" : 18 } } )//maior ou igual que
db.usuarios.find( { idade : { "$lte" : 18 } } )//menor ou igual que 
db.usuarios.find( { idade : { "$ne" : 18 } } )//diferente 
{% endhighlight %}

Um pouco diferente do que estamos acostumados. No objeto de pesquisa especificamos o campo que queremos fazer a comparação e atribuímos a ele um outro objeto que possui como campo a comparação queremos fazer e o valor.

Os operadores OU e E que são um pouco difícil de entender já que a posição parece mais estranha veja-os:

{% highlight javascript %}
db.usuarios.find( { "$or": [ { nome:"Marcelo" } , { nome:"Suissa" } ] } )
{% endhighlight %}	
	
Temos o objeto de pesquisa com o campo $or que recebe como valor um array e irá executar o operador OU para cara um destes valores. Também poderá ser utilizado juntamente com qualquer outra comparação como:

{% highlight javascript %}
db.usuarios.find( { telefone:"1234-5678" , "$or": [ { nome:"Marcelo" } , { nome:"Suissa" } ] } )
{% endhighlight %}

Neste caso buscará todas as pessoas que tiverem o telefone “1234-5678″ E o nome for Marcelo OU Suissa.

A operação AND pode ser feita de duas maneiras, se for com dois campos diferentes é bastante simples

{% highlight javascript %}
db.usuarios.find( { nome:"Marcelo" , sobrenome:"Alves"} )
{% endhighlight %}

Mas se tivermos utilizando o mesmo campo é necessário utilizar o formato abaixo(que apenas funciona na v2.0+):

{% highlight javascript %}
db.usuarios.find( { "$and": [ { nome : { "$ne" : "Marcelo" } } , { nome : { "$ne" : "Suissa" } } ] } )
{% endhighlight %}

Também no caso de se estar tentando estipular um intervalo de valores também pode ser feio assim:

{% highlight javascript %}
db.usurios.find( { idade : { $gte : 18 , $lte : 29 } } )
{% endhighlight %}


Também para pesquisa temos o exists que buscas apenas os documentos que tem ou não tem um determinado campo (semelhante ao not null)

{% highlight javascript %}
db.usuarios.find( { telefone : { $exists : true } } )
{% endhighlight %}

ou

{% highlight javascript %}
db.usuarios.find( { telefone :{ $exists : false } } )
{% endhighlight %}

E o <strong> in </strong> que busca todos os documentos em que o campo for igual a qualquer um dos valores contidos no array

{% highlight javascript %}
db.pessoas.find( { nome : { $in :[ "Marcelo" , "Alves" ] } } )
{% endhighlight %}


Bom acho que era isso, espero que tenha conseguido passar um pouco do meu conhecimento para vocês. Caso ainda tenha dúvidas, poderá consultara documentação do MongoDB .
