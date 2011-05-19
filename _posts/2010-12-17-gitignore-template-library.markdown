---
layout: post
title: gitignore模板库
category: git
tags: git
---

[github地址](https://github.com/github/gitignore)

rails3项目新建时，会在项目根目录下生成.gitignore文件，这个文件是用来忽略那些不需要提交的文件。

你可以直接将项目里的Rails.gitignore里面的内容替换原来项目里的gitignore

这个模板库里还有其他许多模板，你可以在git global里加载，不用每个项目去修改了。
{% highlight bash %}
    git config --global core.excludesfile ~/.global_ignore
{% endhighlight %}
可以通过git config看到设置起效
{% highlight bash %}
    git config --list
{% endhighlight %}