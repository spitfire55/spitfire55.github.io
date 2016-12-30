---
layout: post
title: Rotating Arrays in Python
description: Advent of Code helped me discover a cool way to shift arrays
---

So during my time trying to solve [Advent of Code]("https://www.adventofcode.com/2016") problems (specifically, Day 8), I came across a cool trick on the [AoC subreddit]("https://www.reddit.com/r/adventofcode/comments/5h52ro/2016_day_8_solutions/") that makes it very easy to wrap arrays. Lets say you have the arrays
<pre>
<center>1, 2, 3, 4, 5</center>
</pre>
and you want to shift the values to the left by three so that the end result is
<pre>
<center>3, 4, 5, 1, 2</center>
</pre>
Trying to do this with a for loop might look something like this:  
{% highlight python %}     
myArray = [1,2,3,4,5]  
shift = 3  
myArrayLen = len(myArray)  
tempArray = [0 for x in range(myArrayLen)]  
for x in range(myArrayLen):  
    tempArray[(x+shift) % myArrayLen] = myArray[x]  
myArray = tempArray  
return myArray  
{% endhighlight %}

A even simpler way would be list comprehension:  
{% highlight python %}    
myArray = [1,2,3,4,5]  
return [myArray[(x - shift) % len(myArray)] for x in range(len(myArray))]  
{% endhighlight %}  

However, there is even a simpler solution that uses negative indices. When I first did the problem, I did it using the for loop approach. However, as I read through solutions on Reddit, I saw the list comprehension approach. I was at first a bit puzzled how the _x - shift_ portion of the code worked, since it would result in a negative index at the start of the list. After thinking about it for a bit, I realized that the negative index would wrap around in the negative direction the same way the modulus would wrap around in the positive direction.

With this in mind, I kept reading some other solutions. I came across the following:

{% highlight python %}  
def rot(arr, dist): 
    return arr[-dist:] + arr[:-dist]  
{% endhighlight %}  

All of that code above was simplified down to a single line. What this code essentially does is take the final x values, where x is the shift distance (I assume in this case that the shift distance is less than the array length), and prepends those to the first y values, where y is differnce between the total length of the array and the shift distance. This simple, elegant solution will definitely be used in the future when I need to shift values in an array.

Merry Christmas, and happy coding!