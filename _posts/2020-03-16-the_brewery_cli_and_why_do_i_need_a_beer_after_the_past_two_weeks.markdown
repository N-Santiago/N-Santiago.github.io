---
layout: post
title:      "The Brewery CLI and Why Do I Need a Beer After The Past Two Weeks"
date:       2020-03-16 17:52:24 +0000
permalink:  the_brewery_cli_and_why_do_i_need_a_beer_after_the_past_two_weeks
---


The date is 3/16/20, the hour, 9:00 AM Alaska Time and my anxiety levels are high up with the Northern Lights as my first project is past due. Maybe these are excuses of mine, but imagine having a new job, moving to a new apartment, finishing a 2019 audit in the current job and having this project. Stressful, right? 

Ironically, my CLI program is inspired in my less stressful moments in life. All of us want to do something, travel and have new life experiences. Probably due to house prices and inflation in general being high up with the Aurora Borealis, we rather spend our money in travels and vacations while sharing those life experiences on Instagram. One of the things many of us like to do in those life experiences or just anytime we visit any city or town is check out the local beers. How hoppy is their IPA, how malty is their stout and how creative they are with those crazy specialties. For example, I'm from a smalltown in Alaska and there's two breweries. My favorite one is a Gummi Bear Belgian Tripel. What are the odds of having a Gummi Bear belgian in......Soldotna, Alaska. In other words, the craft beer business is an industry that's being rising to the Artic Lights skies and still keep a DIY spirit with their small businesses, collaboration between companies, contributions to its communities and even their label aestethics and creative names. Yes, that's fascinating for me. So I decided it would be a good idea to ellaborate those lines of codes for my enjoyment. 

![](https://kenaipeninsula.org/sites/default/files/1548185_10153772240015607_1896437546_o.jpg)

But then, came the hardest part. How can I figure out all these issues in so little time? How can I take a deep breath and solve the errors I'm getting? Well, like the craft beer business, Flatiron School and the rest and coding nerds and professionals are indeed, a community. Not only did I looked for help in my cohort's Slack chat, Twitter and even Slack Overflow. I worked together with some of my class peers. Having a sense of community and collaboration that motivates to continue, no matter how hard it is to administer time or getting the correct code. We can do it together! And when we're in this together, we're going up as the......ok that's enough, I'm out of Aurora references. 

To share at least a line of code, I'm going to help you out with empty arrays. Whenever your API returns an empty array rather than an error message in ruby, we can handle it this way in our API file:

```
return if @breweries_hash.empty?
```

That will help you handle the error. Remember to type it above the object you'll create for itirating the API data. Then, in the CLI file, we're going to create the ```if``` statement. Let's what we can do:

```
if input.length < 1 || @objects.empty? #empty array handle 
      puts "Sorry, I didn't found any tap!!" 
```

As you can see, I'm stating that the program will tell you that didn't found any tap when either your input is wrong (and the array is empty) or there's no input at all. 

Shout out to everyone who helped and worked with me. Now, I'm gonna get a Gummi Bear. ¡Salud! 
