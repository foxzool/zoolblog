---
layout: post
title: 在rails中使用jquery
category: rails
tags: rails
---

rails默认使用的是prototype这个库，如果要替换为jquery的话，按下面步骤做

首先替换public/javascript/rails.js为jquery的版本,
[从github下载](https://github.com/rails/jquery-ujs/blob/master/src/rails.js)

覆盖public/javascript/rails.js

然后[下载jquery](http://code.jquery.com/jquery-1.4.4.min.js)

放到pubic/javascript/jquery.js

在config/application.rb里，将下面的注释取消

{% highlight bash %}
config.action_view.javascript_expansions[:defaults] = %w(jquery rails)
{% endhighlight %}

重启服务器