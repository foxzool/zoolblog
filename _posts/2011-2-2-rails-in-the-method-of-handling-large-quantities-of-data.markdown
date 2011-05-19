---
layout: post
title: rails中处理大批量数据的方法
category: rails
tags: rails
---

在实际运用中，我们要对每个用户发一封信的话。 一般的写法是 

{% highlight ruby %}
User.all.each {|user|
  NewsLetter.weekly_deliver(user)
}
{% endhighlight %}

当数据条目超过1000时， 这样的命令会占用大量的内存。 

rails里使用find_each方法来处理这样的情况

{% highlight ruby %}
User.all.each {|user|
  NewsLetter.weekly_deliver(user)
}
{% endhighlight %}

默认是1000条一批
可以用下面的参数指定一批的条数， 还可以指定开始的主键ID

{% highlight ruby %}
User.find_each(:batch_size => 5000, :start => 2000) {|user|
  NewsLetter.weekly_deliver(user)
}
{% endhighlight %}

find_each 是逐条处理对象， 有另外一个find_in_batches是按数组来处理

{% highlight ruby %}
Person.where("age > 21").find_in_batches do |group|
    sleep(50) # Make sure it doesn't get too crowded in there!
    group.each { |person| person.party_all_night! }
  end
{% endhighlight %}

看源码， find_each是对find_in_batches的包装

{% highlight ruby %}
# File activerecord/lib/active_record/relation/batches.rb, line 19
    def find_each(options = {})
      find_in_batches(options) do |records|
        records.each { |record| yield record }
      end

      self
    end
{% endhighlight %}
