---
layout: post
title: 完美解决rails中国时区时间设置
category: rails
tags: rails
---

##解释4个时区设置的不同

* config.active_record.default_timezone

* config.time_zone 

* Time.zone

* ENV['TZ']

分别解释如下:

1. ENV['TZ']

   这个变量指的是服务器系统变量，ubuntu下可以用cat /etc/timezone来查看

   当这个值为 Asia/Shanghai时， 显示就是中国时间。  

   对于ruby/rails来说，这个值决定 Time.now的显示时间

2. config.time_zone

   这个值是rails系统对显示时间的默认设置，可以通过 rake time:zones:all 列出所有可以设置的时区

   一般来说把这个设置为 'Beijing'

3. Time.zone

   这个是设置最终处理显示的时区，可以覆盖config.time_zone,参数和config.time_zone一样

   可以参考 railscasts的这篇 [Time Zones in Rails 2.1](http://railscasts.com/episodes/106-time-zones-in-rails-2-1)

4. config.active_record.default_timezone

   **这里就是全文的关键了！**

   这个default_timezone是决定active_record对数据库交互的时区设置，也就是影响created_at和updated_at在数据库的记录时间。

    只有两个参数:utc和:local, rails初始化时默认是utc，所以保存到数据库的时间是utc时间。

## 总结

要在界面和数据库都很好的显示处理中国时区时间，编辑/path/to/site/config/application.rb(rails2是environment.rb), 加入
{% highlight ruby %}
    config.active_record.default_timezone = :local
    config.time_zone = 'Beijing'
{% endhighlight %}

完美解决rails中国时区时间设置