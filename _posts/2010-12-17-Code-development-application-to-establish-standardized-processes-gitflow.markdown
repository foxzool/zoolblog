---
layout: post
title: 应用gitflow建立代码开发标准化流程
category: git
tags: git
---


[github地址](https://github.com/nvie/gitflow)

简单的来说就是几步

1.安装
{% highlight bash %}
    wget -q -O - http://github.com/nvie/gitflow/raw/develop/contrib/gitflow-installer.sh | sh
{% endhighlight %}
    我在安装的时候从github下载文件时报证书错误，加了参数忽略错误后才成功
{% highlight bash %}
    wget -q -O - --no-check-certificate https://github.com/nvie/gitflow/raw/develop/contrib/gitflow-installer.sh | sudo sh

    sudo apt-get install opt
{% endhighlight %}
2.初始化
{% highlight bash %}
   git flow init
{% endhighlight %}

3.开发流程,就像文章里说的
{% highlight bash %}
>开发新特征

>git flow feature start <name> [<base>]
>git flow feature finish <name>
>列出新特征分支
>git flow feature
>准备发布版本

>git flow release start <name> [<base>]
>git flow release finish <name>
>列出发布分支
>git flow release
>< base >是位于develop分支的commit

>修正紧急Bug

>git flow hotfix start <name> [<base>]
>git flow hotfix finish <name>
>列出修正分支
>git flow hotfix
>支援其他成员工作

>git flow support start <name> <base>
>没有finish?(待实践)
>列出支援分支
>git flow support
>< base >是位于master分支的commit
{% endhighlight %}
