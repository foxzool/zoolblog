---
layout: post
title: rails调试插件rails-footnotes使用说明
category: rails
tags: rails gem
---

#说明
rails-footnotes 是一个在development环境下调试rails用的插件， 可以在当前页面的页脚处显示当前的调试信息，如session、实例变量、数据库查询时间等等

#截图

![rails-footnotes](/assets/attachments/rails-footnotes.png)

#安装方式

{% highlight ruby %}
	
	#编辑Gemfile, rails3版本必须用rails-footnotes 3.7 版以上的版本
	gem 'rails-footnotes', '>= 3.7', :group => 'development' 
	
	bundle install
	
	#编辑config/initializers/footnotes.rb
	if defined?(Footnotes) && Rails.env.development?
	    Footnotes.run! # first of all

	    # ... other init code
	end
{% endhighlight %}

#注意

rails-footnotes默认使用textmate来编辑当前页面文件， 如果要自定义配置编辑器， 请看[rails-footnotes文档](http://rubydoc.info/gems/rails-footnotes/3.7.4/file/README.rdoc)