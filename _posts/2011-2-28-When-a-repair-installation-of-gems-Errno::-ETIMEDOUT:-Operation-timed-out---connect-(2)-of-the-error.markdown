---
layout: post
title: "修复安装gems时Errno::ETIMEDOUT: Operation timed out - connect(2)的错误"
category: ruby
tags: ruby
---

这两天更新gems出现下面的错误
<code>
➜  ~  gem install rails      
ERROR:  Could not find a valid gem 'rails' (>= 0) in any repository
ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
    Errno::ETIMEDOUT: Connection timed out - connect(2) (http://rubygems.org/latest_specs.4.8.gz)
</code>

经检查和GFW无关，是rubygems的DNS
调整问题

#问题解决的最好方法方法
使用google的DNS
8.8.8.8 / 8.8.4.4

#另一种解决方式
修改rubygems的source源
<code>
#删除原有gem source
gem source -r http://rubygems.org/
gem source -r http://production.s3.rubygems.org/ 

#增加新source源
gem source -a  http://production.s3.rubygems.org.s3.amazonaws.com/
</code>

