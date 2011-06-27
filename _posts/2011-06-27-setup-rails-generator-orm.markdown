---
layout: post
title: 设置rails中generator使用的orm类型
category: rails
tags: rails
---

在最近的一个项目里, 同时使用了postgresql和mongoid, 

结果在rails g model xxxx时, 默认调用的是mongoid,

虽然能通过--orm=actvie_record参数指定orm, 但还是很麻烦.

通过查询手册, 可以用下面的设置方式解决.

{% highlight ruby %}
#config/application.rb
config.generators do |g|  
   g.orm             :active_record  
end

{% endhighlight %}