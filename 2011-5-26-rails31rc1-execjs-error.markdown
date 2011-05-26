---
layout: post
title: rails3.1rc1在服务器上运行报Could not find a JavaScript runtime错误的解决方法
category: rails
tags: rails
---

rail3.1rc1在服务器上运行时报以下的错误信息：
{% highlight bash %}
  Could not find a JavaScript runtime. See https://github.com/sstephenson/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)
{% endhightlight %}

解决方式是在gemfile中加入
{% highlight ruby %}
  gem 'therubyracer-heroku', '0.8.1.pre3'
{% endhightlight %}