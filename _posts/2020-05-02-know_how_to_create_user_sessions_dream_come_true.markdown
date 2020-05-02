---
layout: post
title:      "Know How to Create User Sessions. Dream Come True "
date:       2020-05-02 17:18:32 +0000
permalink:  know_how_to_create_user_sessions_dream_come_true
---


Is this time again. You guessed it, doing a blog assignment that's past due. Currently, I'm working the Sinatra Project. In my previous project post, I ranted about having too much to do additional to the project. Believe in coincidences or not, I'm starting training of that second job all over again (thanks COVID!) and I'm working on the onboarding process of a job offer I got months ago. Again, thanks COVID! So in between all those things, let's talk about something that got me electrified. User Sessions. I was excited about that!

![](https://scstylecaster.files.wordpress.com/2014/04/ron-swanson-is-excited.gif?w=500&h=282)

One of the reasons I came back to the coding world, is my fascination on how things work behind the scenes. How do I tweet? How do I watch that video on Youtube? How do I login to all these websites? What's behind that? Well, the time to learn about user session has come! I was exhilarated by learning this code: 

```
class ApplicationController < Sinatra::Base
  configure do
    set :views, Proc.new { File.join(root, "../views/") }
    enable :sessions unless test?
    set :session_secret, "secret"
  end

  get '/' do #yaaaay websites!!!
    erb :index
  end

  post '/login' do #Yeaaah, I'm learning how to make a user login
    @user = User.find_by(username: params[:username], password: params[:password])
    if @user.class == User 
      session[:user_id] = @user.id
      redirect to '/account'
    else
      erb :error
  end
end 

  get '/account' do #Yaaaas!!!!! Here's the accooooount!!!
    if session[:user_id] != nil && session[:user_id] != ""
      erb :account
    else
      erb :error 
  end
end 

  get '/logout' do #look at this, I even made him logout!! 
    session.clear
    redirect to '/'
  end
end
```

How cool is that? This is how we set the App Controller on Ruby. And is just the beginning. Yes, it is tough, it is frustrating and it is hard to keep up with a bootcamp cohort, but those rewards once you finish a lab or a project are  always rewarding. Before I go, here's the HTML code for the login page. 

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>title</title>
    <link rel="stylesheet" href="stylesheets/bootstrap.css" type="text/css">  
  </head>
  <body id="page-top">
    <h1>Welcome to FlatBank</h1>
    <h3>Log In Please</h3>
    <form action='/login' method="POST">
<label for "Username">Username: </label>
<input type="text" id="username" name="username">
<br />
<label for "password">Password: </label>
<input type="text" id="password" name="password">
<br />
<input type="submit" value="Log In" id="submit">
</form>

  </body>
</html>
```

It is for FlatBank, so I'll show this one if I get interviewed at a bank's headquarters. 

