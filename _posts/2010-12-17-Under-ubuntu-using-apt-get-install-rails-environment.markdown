---
layout: post
title: Ubuntu下用apt-get安装rails环境
category: rails
tags: ubuntu rails
---

首先使用apt-get安装ruby
{% highlight bash %}
    sudo apt-get install ruby
{% endhighlight %}
运行 ruby -v
{% highlight bash %}
    ruby 1.8.7 (2010-06-23 patchlevel 299) [i686-linux]
{% endhighlight %}
ruby安装完毕

安装rubygems，*注意,这里不要用apt-get来安装*

先从官网下载最新版rubygems,并解压
{% highlight bash %}
    cd /tmp;wget http://production.cf.rubygems.org/rubygems/rubygems-1.3.7.tgz

    tar zxf rubygems-1.3.7.tgz
{% endhighlight %}

运行安装程序
{% highlight bash %}
    sudo ruby setup.rb
{% endhighlight %}
会看到输出很多文字，最后一行是
{% highlight bash %}
    RubyGems installed the following executables:

    /usr/bin/gem1.8
{% endhighlight %}
然后做一个ln连接
{% highlight bash %}
    sudo ln -s /usr/bin/gem1.8 /usr/bin/gem
{% endhighlight %}
输入gem -v 显示 1.3.7 说明 rubygems安装完毕,开始安装rails
{% highlight bash %}
    sudo gem install rails
{% endhighlight %}
经过一段时间的等待和文字输出之后，运行 rails -v， 显示  Rails 3.0.3 说明安装正确

rails new newapp  开始享受rails的快乐吧！

