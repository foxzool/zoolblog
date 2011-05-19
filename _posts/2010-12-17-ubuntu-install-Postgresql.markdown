---
layout: post
title: ubuntu安装Postgresql
category: ubuntu
tags: ubuntu postgresql
---

# 安装

{% highlight bash %}
    sudo apt-get install postgresql
{% endhighlight %}

输入密码，确认。下载安装完毕之后会创建一个postgres用户，默认密码为空。

#配置    

修改postgres用户密码

{% highlight bash %}
    sudo passwd postgres
{% endhighlight %}

切换到postgres用户

{% highlight bash %}
    sudo su postgres
{% endhighlight %}

登录到postgres数据库

{% highlight bash %}
    psql postgres
{% endhighlight %}

会看到一下文字

{% highlight bash %}
    psql (8.4.5)
    Type "help" for help.

    postgres=#
{% endhighlight %}

然后输入下面的命令,password为你要设置的密码

{% highlight bash %}
    ALTER USER postgres with PASSWORD 'password'
{% endhighlight %}


输入\q返回到终端  


#创建用户和数据库  


输入

{% highlight bash %}
    createuser -drSP blog  #创建一个blog用户，但不是超级管理员

    createdb -O blog blogdb  #创建一个属于blog用户的blogdb数据库
{% endhighlight %}

#安装pgadmin

输入

{% highlight bash %}
    sudo apt-get install pgadmin3
{% endhighlight %}

安装完毕，运行

{% highlight bash %}
    pgadmin3
{% endhighlight %}

#设置其他网络连接数据库

修改/etc/postgresql/8.4/main/pg_hba.conf:

{% highlight bash %}
    # Database administrative login by UNIX sockets
    # local   all         postgres                          ident

    # TYPE  DATABASE    USER        CIDR-ADDRESS          METHOD

    # "local" is for Unix domain socket connections only
    local   all         all                               md5 #ident
    # IPv4 local connections: 
    host    all         all         127.0.0.1/32          md5
    # IPv6 local connections:
    host    all         all         ::1/128               md5  
{% endhighlight %}

修改/etc/postgresql/8.4/main/postgresql.conf,

{% highlight bash %}
    listen_address = '*' #允许其他机器访问
{% endhighlight %}

重启数据库

{% highlight bash %}
    sudo /etc/init.d/postgresql-8.4 restart
{% endhighlight %}

安装完成