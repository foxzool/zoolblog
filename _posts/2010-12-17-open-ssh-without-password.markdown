---
layout: post
title: 开启ssh无密码登录
category: ubuntu
---

首先生成公钥
{% highlight bash %}
    ssh-keygen -t rsa
{% endhighlight %}
一路回车，会在~/.ssh目录下生成公钥和私钥.

将公钥复制到需要登录的服务器
{% highlight bash %}
    ssh-copy-id user@host
{% endhighlight %}
OK，完成了设置。

P.S. 如果服务器没有开启公钥登录，请编辑 /etc/ssh/sshd_config, 确保
{% highlight bash %}
    PubkeyAuthentication yes
{% endhighlight %}    
并重启ssh服务
{% highlight bash %}
    sudo /etc/init.d/ssh restart
{% endhighlight %}

