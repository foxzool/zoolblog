---
layout: post
title: 建立sproutcore应用
category: ruby
tags: sproutcore gem
---

sproutcore是通过rubygems来安装的
{% highlight bash %}
gem install sproutcore
{% endhighlight %}

建立应用
{% highlight bash %}
sc-init HelloWorld
{% endhighlight %}

启动应用
{% highlight bash %}
cd HelloWorld
sc-server
{% endhighlight %}

便会通过启动thin在locahost:4020提供应用服务