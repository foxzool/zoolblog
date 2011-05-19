---
layout: post
title: 生产环境下rake db:migrate报错database is not configured
category: rails
tags: rails
---

我在服务器上运行了下面的命令
{% highlight bash %}
    RAILS_ENV=production rake db:migrate
{% endhighlight %}
结果报错
{% highlight bash %}
> ** Invoke db:migrate (first_time)

> ** Invoke environment (first_time)

> ** Execute environment

> rake aborted!

> proudction database is not configured
{% endhighlight %}
google后得到解决方法,将RAILS_ENV参数放到最后
{% highlight bash %}
    rake db:migrate RAILS_ENV=production
{% endhighlight %}