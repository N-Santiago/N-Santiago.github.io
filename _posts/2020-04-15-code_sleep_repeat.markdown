---
layout: post
title:      "Code, Sleep, REPEAT"
date:       2020-04-15 20:40:07 +0000
permalink:  code_sleep_repeat
---


Is that time of the month, the day to do the that past due blog assignment. At this month, I would be talking about my experience with Sinatra. Which has been great. Things are getting more exciting and this past week has been smooth, like smooth jazz or like the legend himself. 

![](https://api.time.com/wp-content/uploads/2015/12/sinatra1.jpeg?w=800&quality=85)

A few weeks ago, I was making the best out of my Business Intelligence experience (or should I say familiarity with SQL) to work those lessons. However, I was running too fast and hit myself with a wall called ActiveRecord. It was something new to me. Though is straightforward, we do need to be comfortable with what we learned so far. And that's where the CRUD Create, Read, Update, Delete) actions come to play.  The CRUD lab consisted on exercises to instantiate and create data on Ruby. For example: 

```
def can_be_created_with_a_hash_of_attributes
  # Initialize movie and then and save it
  attributes = {
      title: "The Sting",
      release_date: 1973,
      director: "George Roy Hill",
      lead: "Paul Newman",
      in_theaters: false
  }
  movie = Movie.find_by(attributes)  
end
```

In order to solve the failures, we need to know what we learned in the previous Ruby courses. Assuming we have to developed a CLI program, this should be a simple one. Well, not for me. There was one challenging and difficult exercise. Create the Christmas classic Home Alone if its in the argument or create the cult classic The Room if there's no argument. 

Sometimes I tried and it was returning an error that was expecting The Room. Which had me shouting out of frustration like this: 

![](https://thumbor.forbes.com/thumbor/960x0/https%3A%2F%2Fblogs-images.forbes.com%2Frobcain%2Ffiles%2F2017%2F10%2FKevin-Home-Alone.jpg)

Then, I decided to try it another way. Maybe adding that Home Alone argument....

![](https://thumbs.gfycat.com/BrownWarlikeConch-size_restricted.gif)

Exactly, I was frustrating. Turns out I needed to do something, repeat. Before realizing the correct code, I needed to review hashes with pair values. The moral of this story is to repeat, then repeat and then repeat some more. Review the topics, code again, play with for a bit with those codes. This was the correct code that solved the issue:

```
def can_be_created_in_a_block(m = {title: "Home Alone", release_date: 1990})
    movie = Movie.create do |mov|
    mov.title = m[:title]  
    mov.release_date = m[:release_date]   
    mov.save 
  end	
end	
```

That would also create both Home Alone and the amazing bad movie The Room. Remember fellow newbie, learn the code and keep practicing. Repetition is the key to get the value out of what we're learning.  
