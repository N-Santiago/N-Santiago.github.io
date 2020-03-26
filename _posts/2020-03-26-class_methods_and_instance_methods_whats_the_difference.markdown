---
layout: post
title:      "Class Methods and Instance Methods: What's the Difference? "
date:       2020-03-26 21:05:22 +0000
permalink:  class_methods_and_instance_methods_whats_the_difference
---


Today, I want to write about an important topic for Ruby beginners, the difference between class and instance methods. As beginners, we can be overwhelmed by so much terminology. What is a method? What "iterating" data means? What's an argument? And so on and so on. But, I'm here to help. Yes, help. Including myself by writing this for all of us. So let's take a deep breath and start step by step. 

First, let's start by defining method. A Ruby method can be simply defined by the word function. A function that will return a value. 

For example:

```
def print_data(value)
  puts value 
end
```

Within a method, you can organize your code into subroutines which can be easily invoked from other areas of their program. 

Let's see this other method. 

```
def add_one(number)
  number + 1
end

def add_two(number)
  number = add_one(number)
  add_one(number)
end
```

Here, I'm calling method ```add_one(number)``` on method ```add_two``` when declaring the ```number``` variable. That's the magic of Ruby. We'll be connecting those methods. Is as simple as starting with ```def``` and ending with ```end```. 

Now, if we declare those methods in a Class. What is a Class? A class is a blueprint from which objects are created. To put it in even more simpler words. Is the where the objects are created. 

The sintax is as simple as this little example right here:

```
class Name
 # some code describing the class behavior
end
```

So what's an instance? If I got a class and I'm creating a method, how can I get an instance variable? Let's take a look at the following code. 

```
class Person
  def initialize(name)
    @name = name
  end
end
```

We got the Class Person. Then we got the Method Initialize(name). **Important: Initializers are an essential part of your Ruby programs.**  The body of the initialize method now does nothing else but assign the value of the local variable name to an instance variable @name. In other words, name is a local variable (exist within the definition of a module, method, class) to an instance variable and is going to be confined to whatever object self refers to. Now we'll be calling the instance variable name with an ```@```.  Like this, ```@name```. 

Now that we know what's a Class, a Method and an Instance variable. Can we understand what's a Class Method and what's an Instance Method? 

Let's check what's a Class Method. A class method provides functionality to a class itself. For example:

```
  def self.from_the_class
    "Hello, from a class method"
  end
	```
	
	While an instance method provides functionality to one instance of a class. For example:
	
	```
	def from_an_instance
    "Hello, from an instance method"
  end
	```
	
See the difference? ```self``` is signifying that is signifying that it is a Class Method. We can also write Class Method like this:

```
class SayHello  
class << self  
def from_the_class 
puts "Hello, from a class method"  
end  
end 
```

Another important detail about class methods. We wanna call a class variable with ```@@```. One thing we'll do a lot when programming ruby are the following.

```
Class Person

attr_accessor :name

@@all = []

def initialize(name)
@name = name
@@all << self
```

In this program, we're starting by creating the Class Person, followed by setting instance variable name as setter and getter (basically, read and write access), inititalizing that name instance variable and also initializing the ```@@all``` class instance which will store every instance of the Song class. 

So there it is, the difference between the Class and Instance methods. Once we figure out what each of those terms are, it makes sense. Is like getting all the pieces of complicated jigsaw puzzle. And like every jigsaw puzzle, we gotta start with the borders. In this case, this is the border. Understanding what it is and how it works will help us create good Object Oriented programs. Now that we understand Ruby a little bit. Let's keep having fun as we dive in deeper! 
