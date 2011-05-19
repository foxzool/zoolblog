---
layout: post
title: 生成rails项目的实体关系图
category: rails
tags: rails gem
---

实体关系图 == Entity-Relationship Diagrams 

[插件官网](http://rails-erd.rubyforge.org/)

首先安装Graphviz

{% highlight bash %}
% brew install cairo pango graphviz    # Homebrew on Mac OS X
% sudo port install graphviz           # Macports on Mac OS X
% sudo aptitude install graphviz       # Debian and Ubuntu
{% endhighlight %}

然后在开发环境中使用

{% highlight bash %}
group :development do
  gem "rails-erd"
end
{% endhighlight %}

安装

{% highlight bash %}
% bundle install
{% endhighlight %}

生成PDF
{% highlight bash %}
% rake erd
{% endhighlight %}