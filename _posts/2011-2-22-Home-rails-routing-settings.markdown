---
layout: post
title: rails路由设置网站首页
category: rails
tags: rails
---

做一个应用必做的一步

首先删除 /public/index.html 这个文件

然后编辑 config/route.rb ，设置路由

{% highlight ruby %}
root :to => "home#index"
{% endhighlight %}

其中 "home#index" 是rails路由的简写， 指的是 homescontroller的index方法

设置首页后， 会自动生成两个helper方法 root_path和 root_url，  其中_path是相对路径，_url是绝对路径