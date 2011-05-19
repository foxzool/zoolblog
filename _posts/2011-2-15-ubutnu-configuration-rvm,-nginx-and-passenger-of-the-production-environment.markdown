---
layout: post
title: ubutnu配置rvm,nginx和passenger的生产环境
category: rails
tags: rails rvm nginx passenger
---

下述内容参考了[A Guide to a Nginx, Passenger and RVM Server](http://blog.ninjahideout.com/posts/a-guide-to-a-nginx-passenger-and-rvm-server)

首先， 使用 root 帐号登录， 

安装git和curl
{% highlight bash %}
apt-get install curl git-core
{% endhighlight %}

使用脚本安装rvm
{% highlight bash %}
bash < <(curl -L http://bit.ly/rvm-install-system-wide)
{% endhighlight %}
脚本会自动创建一个rvm组，并将root用户加入

编辑 /root/.bashrc和/etc/skel/.bashrc
将
{% highlight bash %}
[ -z "$PS!"]  && return 
{% endhighlight %}
替换为
{% highlight bash %}
if [[ -n "$PS1" ]]; then
{% endhighlight %}
在文件最后加入
{% highlight bash %}
fi
if groups | grep -q rvm ; then
  source "/usr/local/lib/rvm"
fi
{% endhighlight %}

配置用户
{% highlight bash %}
#增加zool用户
adduser zool
#将zool加入rvm组
adduser zool rvm
{% endhighlight %}

登录zool用户并测试
{% highlight bash %}
type rvm | head -n1
{% endhighlight %}
如果显示 rvm is a function 则表示安装正确

安装ree依赖组件
{% highlight bash %}
aptitude install build-essential bison openssl libreadline5 libreadline-dev \
curl git-core zlib1g zlib1g-dev libssl-dev vim libsqlite3-0 libsqlite3-dev \
sqlite3 libreadline-dev libxml2-dev git-core subversion autoconf
{% endhighlight %}

安装ree
{% highlight bash %}
rvm install ree
{% endhighlight %}

设为默认环境
{% highlight bash %}
rvm use ree --default
{% endhighlight %}

安装passenger和nginx
{% highlight bash %}
gem install passenger
rvmsudo passenger-install-nginx-module
{% endhighlight %}

配置nginx里的ruby环境
{% highlight bash %}
    passenger_root /usr/local/rvm/gems/ree-1.8.7-2010.02/gems/passenger-3.0.0;
    passenger_ruby /usr/local/rvm/wrappers/ree-1.8.7-2010.02/ruby;
{% endhighlight %}

设置nginx开机脚本
{% highlight bash %}
curl -L http://bit.ly/nginx-ubuntu-init-file > /etc/init.d/nginx
chmod +x /etc/init.d/nginx
update-rc.d nginx defaults
/etc/init.d/nginx start
{% endhighlight %}

原文中后面的step6,7关于Capistrano的环境配置以后再另文详述