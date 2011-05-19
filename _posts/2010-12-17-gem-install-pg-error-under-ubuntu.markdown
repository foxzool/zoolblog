---
layout: post
title: ubuntu下gem安装pg出错
category: ruby
tags: ubuntu ruby
---

在安装pg时，系统报了如下的错误
{% highlight bash %}
    /home/zool/.rvm/rubies/ruby-1.8.7-p302/bin/ruby extconf.rb 
    checking for pg_config... no
    checking for libpq-fe.h... no
    Can't find the 'libpq-fe.h header
    *** extconf.rb failed ***
    Could not create Makefile due to some reason, probably lack of
    necessary libraries and/or headers.  Check the mkmf.log file for more
    details.  You may need configuration options.

    Provided configuration options:
    	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/home/zool/.rvm/rubies/ruby-1.8.7-p302/bin/ruby
	--with-pg
	--without-pg
	--with-pg-config
	--without-pg-config
	--with-pg-dir
	--without-pg-dir
	--with-pg-include
	--without-pg-include=${pg-dir}/include
	--with-pg-lib
	--without-pg-lib=${pg-dir}/lib
{% endhighlight %}
请教GOOGLE大神后，找到如下解决方案
{% highlight bash %}
    sudo apt-get install libpq-dev libpq5
{% endhighlight %}
安装更新后解决问题