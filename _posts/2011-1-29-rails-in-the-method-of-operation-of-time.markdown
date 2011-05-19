---
layout: post
title: rails中对时间的操作方法
category: rails
tags: rails
---

做web应用，和时间打交道是不可免的。rails对ruby的时间模块做了扩展。
本文作于2011年1月29日, ruby版本为1.8.7, rails版本为3.0.3

#基本的时间转换
{% highlight ruby %}
>> now=Time.now
=> Sat Jan 29 21:47:07 0800 2011
#utc秒数互相转换
>> now.to_i
=> 1296308827
>> Time.at(1296308827)
=> Sat Jan 29 21:47:07 0800 2011
#当前时间的一些变量
>> now.sec
=> 7
>> now.min
=> 47
>> now.hour
=> 21
>> now.month
=> 1
>> now.year
=> 2011
#现在是星期几(注意!!!周日是返回 0 )
>> now.wday
=> 6
#现在是本月第几天
>> now.day
=> 29
#现在是今年第几天
>> now.yday
=> 29
#时间参数的数组
>> now.to_a
=> [7, 47, 21, 29, 1, 2011, 6, 29, false, "CST"]
{% endhighlight %}

#时间化输出
{% highlight ruby %}
>> now.strftime("%Y-%m-%d %H:%M:%S")
=> "2011-01-29 21:47:07"
{% endhighlight %}
参数解释如下
{% highlight bash %}
  %a - 星期几的英文简写 (``Sun'')
  %A - 星期几的英文全称 (``Sunday'')
  %b - 月份的英文简写 (``Jan'')
  %B - 月份的英文全称 (``January'')
  %c - 默认的首选本地时间输出格式
  %d - 本月第几天 (01..31)
  %H - 24小时制的小时 (00..23)
  %I - 12小时制的小时 (01..12)
  %j - 今年的第几天 (001..366)
  %m - 月份 (01..12)
  %M - 分钟 (00..59)
  %p - 上午还是下午 (``AM''  or  ``PM'')
  %S - 秒数 (00..60)
  %U - 从星期天算一周开始的本年第几周 (00..53)
  %W - 从星期一算一周开始的本年第几周 (00..53)
  %w - 现在是星期几 (周日是0 , 0..6)
  %x - 默认的日期输出格式 ("01/29/11")
  %X - 默认的时间输出格式 ("21:47:07")
  %y - 年份的后两位 (00..99)
  %Y - 年份
  %Z - 时区名
  %% - 输出%字符
{% endhighlight %}

以上是ruby的基本方法，rails对其做了更多的扩展
{% highlight ruby %}
#重写了to_s方法，能够接受参数
>> now.to_s
=> "Sat Jan 29 21:47:07 +0800 2011"
>> now.to_s(:db)
=> "2011-01-29 21:47:07"
>> now.to_s(:number)
=> "20110129214707"
>> now.to_s(:time)
=> "21:47"
>> now.to_s(:short)
=> "29 Jan 21:47"
>> now.to_s(:long)
=> "January 29, 2011 21:47"
>> now.to_s(:long_ordinal)
=> "January 29th, 2011 21:47"
>> now.to_s(:rfc822)
=> "Sat, 29 Jan 2011 21:47:07 +0800"
{% endhighlight %}

如果要自己设计时间输出格式，按下面方法来，新建一个配置文件
{% highlight ruby %}
  # config/initializers/time_formats.rb
  Time::DATE_FORMATS[:month_and_year] = "%B %Y"
  Time::DATE_FORMATS[:short_ordinal] = lambda { |time| time.strftime("%B #{time.day.ordinalize}") }
{% endhighlight %}

rails对日期的一些扩展
{% highlight ruby %}
#指定时间
>> now.change(:year=>2012, :month=>12, :day => 21, :hour => 0, :min => 0, :sec => 0, :usec => 0)
=> Fri Dec 21 00:00:00 0800 2012

#begginning家族
>> now.beginning_of_day
=> Sat Jan 29 00:00:00 0800 2011
>> now.midnight
=> Sat Jan 29 00:00:00 0800 2011
>> now.beginning_of_week
=> Mon Jan 24 00:00:00 0800 2011
>> now.beginning_of_month
=> Sat Jan 01 00:00:00 0800 2011
>> now.beginning_of_quarter
=> Sat Jan 01 00:00:00 0800 2011
>> now.beginning_of_year
=> Sat Jan 01 00:00:00 0800 2011
#end家族
>> now.end_of_day
=> Sat Jan 29 23:59:59 0800 2011
>> now.end_of_week
=> Sun Jan 30 23:59:59 0800 2011
>> now.end_of_month
=> Mon Jan 31 23:59:59 0800 2011
>> now.end_of_quarter
=> Thu Mar 31 23:59:59 0800 2011
>> now.end_of_year
=> Sat Dec 31 23:59:59 0800 2011
#时间的魔术方法
>> now.yesterday
=> Fri Jan 28 21:47:07 0800 2011
>> now.tomorrow
=> Sun Jan 30 21:47:07 0800 2011
>> now.next_week
=> Mon Jan 31 00:00:00 0800 2011
>> now.next_month
=> Mon Feb 28 21:47:07 0800 2011
>> now.next_year
#注意没有prev_week
>> now.prev_month
=> Wed Dec 29 21:47:07 0800 2010
>> now.prev_year
=> Fri Jan 29 21:47:07 0800 2010
#今日已过秒数
>> now.seconds_since_midnight
=> 78427.615017
#日期输出
>> now.to_date
=> Sat, 29 Jan 2011
>> now.to_datetime
=> Sat, 29 Jan 2011 21:47:07 0800
#按秒数计算
>> now.ago(3600)
=> Sat Jan 29 20:47:07 0800 2011
>> now.since(3600)
=> Sat Jan 29 22:47:07 0800 2011
{% endhighlight %}

实际上还有很多方法没有列出，具体使用还是参考rails的api手册为准。

另外有一个rails插件bystar对此做了更多的扩展, 后面会另外写一篇文章来说明