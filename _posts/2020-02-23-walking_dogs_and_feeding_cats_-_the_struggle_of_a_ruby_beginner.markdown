---
layout: post
title:      "Walking Dogs and Feeding Cats - The Struggle of a Ruby Beginner. "
date:       2020-02-23 21:30:07 +0000
permalink:  walking_dogs_and_feeding_cats_-_the_struggle_of_a_ruby_beginner
---


Today, I woke up with something in mind, write a new blog post at Flatiron. A sunny February Sunday morning in Alaska, the snow is white, the pine trees are getting greener and the coffee smells good. A perfect day to catch up with all my assignments. When I think about a new blog post about my journey as a so called coder newbie and Flatiron School student. There's something that comes to mind, my frustration with the 'OO My Pets' lab. 

![](https://www.rover.com/blog/wp-content/uploads/2019/06/cat-4223305_1920-300x200.jpghttp://)

The lab is about getting some cats and dogs, changing their mood by feeding and walking them and eventually selling them before moving to a tiny NYC apartment. Kinda like Tamagotchi for a millenial who wants to move from the suburbs to the big city. Sounds like fun and it was, the objetive was to have a deeper understanding about Object relations in Ruby. First, there's the Cat and Dog classes. 

```
class Cat
  
  attr_accessor :mood, :owner
  attr_reader :name
  
  @@all = []
  
   def initialize(name, owner)
    @name = name
    @owner = owner
    @mood = "nervous"
    @@all << self 
  end
  
  def self.all
    @@all
  end
  
end
```
```
class Dog
  
  attr_accessor :mood, :owner
  attr_reader :name
  
  @@all = []
  
   def initialize(name, owner)
    @name = name
    @owner = owner
    @mood = "nervous"
    @@all << self 
  end 
  
  def self.all
    @@all
  end 
  
end
```
Look how we initialize their name, the owner and the pet mood. Additionally, we're also declaring the class variable. The thing about Ruby, it that doesn't look hard at all. Declare the class, use ` attr_accessor` and `attr_reader` if the variable is read only and initialize those variables. Of course, we also the class method to know all the cats and dogs. This Owner probably had dozens of pets. 

![](https://www.gannett-cdn.com/-mm-/44e7b49d73e88b1d981c9cd5164e3c6541350e20/c=0-278-3000-1973/local/-/media/2015/02/04/USATODAY/USATODAY/635586718209374247-XXX-101-DALMATIANS-MOV-JY-1627-70560192.JPG?width=580&height=326&fit=crophttp://)

Now, we need to create the `Owner` class. Like the past two classes, it is pretty straighforward to create the class and initialize the variables. 

```
class Owner
  attr_accessor :pets
  attr_reader :species, :name 
  
  @@all = []
  
  def initialize(name)  
    @name = name
    @species = "human"
    @pets = {:dog => [], :cat => []}
    @@all << self
  end 
```
Ruby is fairly easy to understand, once you know how the classes, methods and variables work, you'll do it autimatically. The challenge is how we're gonna work on this objects, how are we gonna relate them. That's when we realize we need to be commited to this new journey. The trick is to start with Ruby and create the variable, declare the setters and getters, initialize the variables, complete the program requirements, repeat and repeat and repeat. I'll keep the rest of the code secret, or not so secret at all. Don't hesitate contacting me and other for help. That's what I did and contributed a lot to my success selling those poor nervious pets.

![](https://www.our-happy-cat.com/images/scared-cat-hiding.jpghttp://)

Save your codes on Github, review them, study them, watch videos, meet new people like you. Must importantly, enjoy the ride. It is an exciting and hopeful one. 
