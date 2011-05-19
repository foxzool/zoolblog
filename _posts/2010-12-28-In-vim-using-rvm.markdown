---
layout: post
title: 在vim中使用rvm
category: misc
tags: vim rvm
---


[github地址](https://github.com/csexton/rvm.vim)


将plugin下载到你的vim plugin里

{% highlight bash %}
curl http://github.com/csexton/rvm.vim/raw/master/plugin/rvm.vim > ~/.vim/plugin/rvm.vim
{% endhighlight %}

编辑vimrc，加入下面的代码

{% highlight bash %}
set statusline+=%{exists('g:loaded_rvm')?rvm#statusline():''} 
{% endhighlight %}