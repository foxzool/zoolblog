---
layout: post
title: ubuntu下mysql字符集设置错误
category: mysql
tags: ubuntu mysql
---
原来在rhel下设置了
{% highlight bash %}
    character-set-server = utf8
{% endhighlight %}
但在ubuntu下不起作用，报错:
{% highlight bash %}
    mysql: unknown variable 'character-set-server=utf8'
{% endhighlight %}
换为以下设置解决问题:
{% highlight bash %}
    default-character-set = utf8
{% endhighlight %}
