---
layout: post
title: "How to make a Javascript Countdown"
date: 2015-10-15 15:30:00
image: '/assets/img/'
description: 'How to make a nice looking counter in JS & CSS'
tags:
- javascript
- css
categories:
- javascript
twitter_text: 'How to make a nice looking counter in JS & CSS'
---
Hi, in this post we are going to make a [cool javascript countdown](https://chamoysvoice.github.io/birthday) that you could use as a countdown for a feature or webpage.

First we must talk about the Date object which according to [w3schools](http://www.w3schools.com/jsref/jsref_obj_date.asp) is a javascript object that receives a string or date representated in milliseconds to build a full Date object.

{% highlight javascript%}
var d = new Date(); // returns the current date

//returns the date according to the milliseconds between
//midnight of January 1, 1970 and the milliseconds provided.
var d = new Date(milliseconds);

// returns the date according to a formatted input.
// Example: Date("11/02/2015 00:00:00 AM");
var d = new Date(dateString);

// If you want to specify everything, you can!
var d = new Date(year, month, day, hours, minutes, seconds, milliseconds);
{% endhighlight %}

After defining what is a date in javascript we only need to get the remaning time to a date, for example, my birthday.

{% highlight javascript%}

var my_birthday = new Date("11/02/2015 00:00:00 AM");

// lets use .getTime(), to get a numeric value between the dates.
var now = new Date();
var remaining_time = my_birthday.getTime() - now.getTime();

// so if remaining_time > 60,
// that means that is at least 1 minute remaining is right?

{% endhighlight %}

So, all we have left is to calculate manually the days, hours, minutes, and seconds to a date to happen, and refresh that every second using an interval :)

lets set the basic unit convertions right:


- millisecond = 1
- second = millisecond * 1000
- minute = second * 60
- hour = minute * 60
- day = hour * 24

and we can use the modular operator to get the exact number of that remaining, like this:

{% highlight javascript%}
var second = 1000,
minute = 60 * second,
hour = 60 * minute,
day = 24 * hour;

var countdown = {
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
}

var remaning = 0;

var my_birthday = new Date("11/02/2015 00:00:00 AM");

// update values of the countdown
function calculate(remaining){
  countdown.days = Math.round(remaining / day);
  countdown.hours  = Math.round((remaning % day) / hour);
  countdown.minutes = Math.round((remaning % hour) / minute);
  countdown.seconds = Math.round((remaning % minute) / second);
}

// update the view of the html
// reemplace the id with your own
function updateView(){
  document.getElementById("seconds").innerHTML = countdown.seconds;
  document.getElementById("minutes").innerHTML = countdown.minutes;
  document.getElementById("hours").innerHTML = countdown.hours;
  document.getElementById("days").innerHTML = countdown.days;
}

// all we have left is to set an interval
setInterval(function(){
  now = new Date();
  remaning = my_birthday.getTime() - now.getTime();
  calculate(remaning);
  updateView();
}, second);
{% endhighlight %}

This is the end of the part 1 of this post, Tomorrow I'll be back with the html & css frontend

For the full code please visit the github repository.

[Github Repository](https://github.com/chamoysvoice/birthday)
