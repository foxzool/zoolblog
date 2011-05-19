---
layout: post
title: 使用bullet来处理rails开发中的N + 1查询问题
category: rails
tags: rails
---

[github地址](https://github.com/flyerhzm/bullet)

在开发中，有时会碰到N + 1查询问题。

比如说，在本Blog显示文章时， 文章的作者是由关联查询得出

{% highlight ruby %}
#home_controller
@posts = Post.paginate :page => params[:page], :order => 'created_at DESC'

#views
@posts.each do |post|
..............
post.user.username
............
{% endhighlight %}

这样，每一篇文章都会有一个查询，怎么来改进代码呢？

首先，先安装bullet
{% highlight ruby %}
group :development do
 gem 'bullet'
end
{% endhighlight %}

然后在config/environments/development.rb加入下面代码

{% highlight ruby %}
  Bullet.enable = true
  Bullet.alert = true
  Bullet.bullet_logger = true
  Bullet.console = true
  Bullet.growl = false
  Bullet.rails_logger = true
  Bullet.disable_browser_cache = true
{% endhighlight %}

重启服务器

之后重新访问页面时就会弹出页面来提示你，当前页面有N+1问题，可以用:include => [:user]来解决

重新编辑home_controller
{% highlight ruby %}
@posts = Post.paginate :page => params[:page], :order => 'created_at DESC', :include => [:user]
{% endhighlight %}

问题解决