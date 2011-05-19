---
layout: post
title: 打造你的加强版irb控制台
category: ruby
tags: ruby irb
---

[github地址](https://github.com/logankoester/irbrc)

### 安装步骤

下载

{% highlight ruby %}
    git clone git://github.com/logankoester/irbrc.git
{% endhighlight %}

安装相关gems

{% highlight ruby %}
    (cd irbrc; rvm gemset import irbrc.gems)
{% endhighlight %}

如果没有装rvm，直接运行
{% highlight ruby %}
     sudo gem install awesome_print bond hirb looksee map_by_method net-http-spy sketches what_methods wirble 
{% endhighlight %}
做文件连接
{% highlight ruby %}
    ln -s ~/irbrc/irbrc ~/.irbrc
{% endhighlight %}
运行irb

### 功能介绍

1. 输出代码高亮

2. irb运行历史记录，下次打开仍保留

3. 将irb命令行提示缩短为 '>>'

4. 输入'c'或'clear'清屏

5. 可以通过tab实现代码补全

6. 使用 *fl(file_name)* 命令来快速打开文件， *rl* 命令来重新打开最近文件， *rt*命令来打开最近文件并重新执行上一条语句 

7. pm方法，可以很漂亮的列出Object的所有methods

8. 自动加载rubygems, 并加载下面几个gems


 * map_by_method
{% highlight ruby %}
    >a = ["1", "2", "3"]

    >a.map_by_to_i

    > => [1, 2, 3]

   实际上相当于 a.map &:to_i, 但更dsl点不是更好?
{% endhighlight %}

 * what_methods

   猜方法名专用
{% highlight ruby %}
>3.14.what? 3  #什么方法返回3？                                             
> 3.14.to_int == 3                                              
> 3.14.floor == 3                                               
> 3.14.round == 3                                               
> 3.14.to_i == 3                                                
> 3.14.prec_i == 3                                              
> 3.14.truncate == 3                                            
> => ["to_int", "floor", "round", "to_i", "prec_i", "truncate"] 
{% endhighlight %}
  * pp

   用法 ap Object， 把一个Object格式华高亮输出

  * Sketches

   可以在irb中使用文字编辑器， 可以参看 [ihower的这篇文章](http://ihower.tw/blog/archives/3633)

   经实际测试，在使用what_methods时不知什么原因会自动打开sketches，可以编辑~/.irbrc，将135-136的sketeches代码注释掉




