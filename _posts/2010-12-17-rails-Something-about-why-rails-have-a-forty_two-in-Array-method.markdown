---
layout: post
title: rails趣谈'为什么rails在Array中有个forty_two方法'
category: rails
tags: rails
---
有次，群里有人问，为什么在rails的Array中有个forty_two方法

先看代码

{% highlight ruby %}

> irb
>> require 'activesupport'
=> true
>> a = Array.new(50).fill {|i| i+=1 }
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
>> a.forty_two
=> 42
{% endhighlight %}
经过网上一番探索，在这个网页得到了答案 [网址](http://www.kerrybuckley.org/2008/11/24/my-very-small-part-in-the-arrayforty_two-controversy/)

在rails2.2时代， 有些人扩展了Array方法，从Array#second写到了Array#tenth。

这太混乱了，于是DHH发话，只保留 second, third, fourth and fifth 但增加一个forty_two， 为什么呢？

因为这是 [生命、宇宙以及任何事情的终极答案](http://zh.wikipedia.org/zh-cn/%E7%94%9F%E5%91%BD%E3%80%81%E5%AE%87%E5%AE%99%E4%BB%A5%E5%8F%8A%E4%BB%BB%E4%BD%95%E4%BA%8B%E6%83%85%E7%9A%84%E7%B5%82%E6%A5%B5%E7%AD%94%E6%A1%88)