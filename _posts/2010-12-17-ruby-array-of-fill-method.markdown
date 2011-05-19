---
layout: post
title: ruby数组填充方法
category: ruby
tags: ruby
---

手册
{% highlight ruby %}
array.fill(obj) → array
array.fill(obj, start [, length]) → array
array.fill(obj, range ) → array
array.fill {|index| block } → array
array.fill(start [, length] ) {|index| block } → array
array.fill(range) {|index| block } → array
{% endhighlight %}

前三个方法都是将obj填充到array里， start 默认为0, length默认为self.length长度

后三个方法是将block里的返回值填充到array里。block接收到的是array的元素index值。

实例代码
{% highlight ruby %}
a = [ "a", "b", "c", "d" ]

a.fill("x")              #=> ["x", "x", "x", "x"]
#将数组里所有元素替换为"x"

a.fill("z", 2, 2)        #=> ["x", "x", "z", "z"]
#从数组第[2]位元素开始，替换 2 次 "z"

a.fill("y", 0..1)        #=> ["y", "y", "z", "z"]
#将数组[0]到[1]位的元素替换为"y"

a.fill {|i| i*i}         #=> [0, 1, 4, 9]
#提供block方法, i为数组下标

a.fill(-2) {|i| i*i*i}   #=> ['a', 'b', 8, 27]
#从数组第[-2]位开始运行block
#注意，ruby源码里的注释是错的
#a.fill(-2) {|i| i*i*i}   #=> [0, 1, 8, 27]
    
#实际应用， 我要生成一个数字从1到50的数组

 >>  Array.new(50).fill {|i| i+=1 }
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]

{% endhighlight %}