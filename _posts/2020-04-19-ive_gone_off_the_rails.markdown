---
layout: post
title:      "I've gone off the Rails . . ."
date:       2020-04-19 12:00:14 -0400
permalink:  ive_gone_off_the_rails
---


I'm pretty sure that saying has everything to do with programming and nothing whatsoever to do with trains.

After completing my Sinatra project, I moved on to Sinatra's bigger and slightly buffer cousin known as Rails. A gem designed to create framework for web applications. I was told things such as "Rails is easy to work with" and other encouraging statements as the time came to one again learn something brand new, as well as master it in just four weeks. Sounds fun, right?

Rails is a very advanced game of Connect-The-Dots. Everything as to smoothly connect to everything else. Your Models need to have their "has_many" and "belongs_to" traits so you can connect them in your methods. Your methods need to clearly defined in your controllers so that you can properly render your views, making sure your variables are defined so the right methods can be called. If you make just one tiny mistake like using a period instead of a comma the entire thing will break. Then when you fix that it might just not work anyway; leaving you stuck in an endless cycle.

"Rails is easy to work with" Am I right?

The key to having everything working as best as it can is to make sure all of your routes are clearly difined. You do this in your **config/routes.rb** file. This file can be your best friend or it will be your worst enemy. It directs the URL requests as passed it to the needed controllers. When building your application start with defining your routes, or you'll get held up everytime you try to render a form.

The first route I'd reccommend you define is your 'root route' this is the default route that will render the view for the homepage of your applcacion. The google.com homepage is the root route for google. My root route is <root 'sessions#welcome'> which translate to "Use the sessions controller and call the welcome method, which will render the welcome form". That form can be found in the 'sessions' folder in 'views'. See? Dots connected.

The more routes you define, the more dots you can connect, if you want full RESTful power for one of your objects, you can use the keyword "resources" to give you model object unlimited RESTful power!

<resources: users>

![](https://media.giphy.com/media/3o84sq21TxDH6PyYms/giphy.gif)



Just like that, Rails has created routes for INDEX, NEW, CREATE, EDIT, UPDATE, SHOW, and DESTROY.
If you want to limit what routes your models have i.e. a little bit of RESTful kryptonite, you can use ":only" in conjuction with "resources:" to limit routes.

<resources: users, only: [:index, :create, :new]>

With that, we can say to the DESTROY route:

![](https://media.giphy.com/media/RX3vhj311HKLe/giphy.gif)

But wait, there's more!

Rails also allwos you to refer to routes by name instead of referencing the URLs the entire time. If we defined a route as:

<get “sessions/destroy”, as: :logout> that creats the name "logout_path" which can be easily written in your Controller methods as well as a button in your View forms. It also means that the DESTROY route can come back to play.

Routes are essential to any application, learn how to define them and navigating form to form will be smooth sailing.

