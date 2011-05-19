---
layout: post
title: rails3新建项目模板
category: rails
tags: rails
---
rails 新建项目时可以使用-m 参数来使用模板生成新项目

#安装需求
*nix系统

git
 
sqlite3/mysql等环境已经安装完毕

rails 3.0.4(之前版本不能使用https的模板地址)


#样例
{% highlight ruby %}
  rails new my_app -T -J -m https://gist.github.com/777670.txt
{% endhighlight %}

就会自动生成新项目，安装一些gem,如
devise
haml
jquery
rspec
等等
同时自动迁移，删除index.html等等不必要文件。

https://gist.github.com/777670 是我自己配置文件，里面的配置可能不适合每个人， 可以自行fork修改。