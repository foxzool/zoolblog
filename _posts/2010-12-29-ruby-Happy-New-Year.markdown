---
layout: post
title: ruby-新年快乐
category: ruby
tags: ruby
---

根据网上的源码改编

{% highlight bash %}
 ruby -e "((1..20).to_a+[6]*4).each{|i|puts ('#'*i*2).center(80)};puts;puts 'Happy New Year'.center(80)"
{% endhighlight %}

关键是center方法
{% highlight bash %}
"Happy New Year".center(80)
{% endhighlight %}
就是将字符串在80个字符的长度内居中