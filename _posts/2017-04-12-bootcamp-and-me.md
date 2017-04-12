---
layout: post
title: Bootcamp and Me
---

So far I've been doing my programming bootcamp for .... *looks at day and thinks* 85 days now. That's almost a quarter of a year. At this point I'm comfortably familiar with the basics of setting up a webpage and can do some slightly fancy things.

Like what? In this day and age of pages that try and be near psychic in predicting your needs, I'm nowhere near that realm. Mostly I can do slick loading things that cause some portions of a page to slide in or slide out in a nice clean way. Cleanliness is a thing I've really come to value as I've gotten further into learning all the ins and outs. There is a lot of care and time that goes into crafting experiences that are pleasant to an end-user. I'm not an expert at writing it yet but when I see it, my appreciation for it is almost tangible.

My bootcamp so far has had three major sections with pretty different experiences between:
* Basics (CSS, HTML, JavaScript)
* First Project/Refactor (Build a website and then re-write it in jQuery)
* Project 2, 3, and 4/Refactor (Refactor first project *again* and two new ones)

Refactoring is both the worst thing and the best, because it really feels like it helps you grow as a programmer/developer, but it sure does suck trying to figure out exactly how to do something you've finished but better. An example of a refactor I did from CodeWars, the [Ubermeister Ball Challenge](http://www.codewars.com/kata/find-heavy-ball-level-ubermaster/train/javascript):

First Attempt
{% highlight js %}
function findBall(scales, ball_count) {
  var leftBalls = [];
  var midBalls = [];
  var rightBalls = [];
  var currentBalls = Array.from({length: ball_count},
  (v, i) => i); 

  var maxTries = Math.ceil(Math.log(ball_count)/Math.log(3)); 
  
  for(var i = 0; i < maxTries; i++) { 
    var numBalls = currentBalls.length; 
    var eachSection = Math.round(numBalls / 3);
    var weightCheck = 0;
    leftBalls = currentBalls.splice(0, eachSection);
    midBalls = currentBalls.splice(0, eachSection);
    rightBalls = currentBalls 
     
    weightCheck = scales.getWeight(leftBalls, midBalls);
    
    if (weightCheck === 0) {
      currentBalls = rightBalls; 
    } else if (weightCheck == -1) {
        currentBalls = leftBalls;
      } else { 
        currentBalls = midBalls;
        }      
  }
  
  return parseInt(currentBalls); 
}
{% endhighlight %}

After a long struggle to find a way to take in all the comments from my awesome mentor and some hints from a fellow student of mine, I ended up reading a bunch on recursion, and found some of my own logic errors. One example, I didn't need to find the number of times the scale could be used. If I wrote it correctly, it should stop before the scales 'broke'.

Final Attempt
{% highlight js %}
function findBall(scales, ball_count) {
  var currentBalls = Array.from({length: ball_count}, (v, i) => i);
  
  return weighBalls(scales, currentBalls);  
}

function weighBalls(scales, balls) { 
  var numBalls = balls.length;
  if(numBalls == 1) { 
    return balls[0];
  }
  
  var delineator = Math.round(numBalls / 3);   
  var leftBalls = balls.splice(0, delineator);
  var midBalls = balls.splice(0, delineator);   

  var weightCheck = scales.getWeight(leftBalls, midBalls); 
  if(weightCheck === 0) {
    return weighBalls(scales, balls);      
  } else if(weightCheck == -1) { 
      return weighBalls(scales, leftBalls);       
  } else {
      return weighBalls(scales, midBalls);       
    }   
}
{% endhighlight %}

Cleaner right? I love writing JavaScript, it's the language I understand best at the moment.

Overall my bootcamp has been a positive but stressful experience. I never get to rest on laurels since by the time I've really conquered an assignment, I'm ramming my head against the next one. I very much understand why a lot of bootcamps preface with needing a lot of self motivation, and I totally agree.