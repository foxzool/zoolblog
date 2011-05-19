---
layout: post
title: ruby中去除字符串空格的方法
category: ruby
tags: ruby
---

使用 String#strip方法,去除所有空格
{% highlight ruby %}
"    hello    ".strip   #=> "hello"
"\tgoodbye\r\n".strip   #=> "goodbye"
{% endhighlight %}

另外lstrip和rstrip分别去除字符串左右两端的空格
{% highlight ruby %}
"  hello  ".lstrip   #=> "hello  "
"hello".lstrip       #=> "hello"
"  hello  ".rstrip   #=> "  hello"
"hello".rstrip       #=> "hello"
{% endhighlight %}

上述方法是返回字符串的copy,如要改变原字符串对象，使用 String#strip!, String#lstrip!, String#rstrip!。 如果对象没有改变则返回nil
{% highlight ruby %}
"hello".rstrip!      #=> nil
{% endhighlight %}