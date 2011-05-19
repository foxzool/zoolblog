---
layout: post
title: rails中文配置
category: rails
tags: rails
---

rails默认为英文，像一些model的验证提示都是英文。
按下面方法将其汉化

首先，在[https://github.com/svenfuchs/rails-i18n/tree/master/rails/locale](https://github.com/svenfuchs/rails-i18n/tree/master/rails/locale)下载相应的语言包

中文选择 zh-CN.yml   ,将其下载到config/locale下面

然后在config/application.rb里加入下面的配置

{% highlight bash %}
config.i18n.default_locale = :'zh-CN' 
{% endhighlight %}
这句话的意思是将rails的语言包默认为简体中文

然后重启服务器即可

效果
{% highlight bash %}
ruby-1.8.7-p302 > I18n.l Time.now
 => "2010年12月30日 星期四 10:11:21 CST" 
{% endhighlight %}