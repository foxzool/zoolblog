---
layout: post
title: Ubuntu上用apt安装sqlite
category: ubuntu
tags: ubuntu sqlite
---

很简单
{% highlight bash %}
    sudo apt-get install sqlite3 libsqlite3-dev
{% endhighlight %}
检查版本
{% highlight bash %}
    ~ > sqlite3 -version
    3.7.2
{% endhighlight %}
通过命令行进入数据库
{% highlight bash %}
    sqlite3 development_newsite.sqlite3

    SQLite version 3.7.2
    Enter ".help" for instructions
    Enter SQL statements terminated with a ";"
    sqlite>
{% endhighlight %}
输入.help查看帮助， .quit退出页面

如果需要图形界面可以安装sqlitebrowser
{% highlight bash %}
    sudo apt-get install sqlitebrowser
{% endhighlight %}