---
layout: post
title: 在has many through里实现计数
category: rails
tags: rails
---
由于has many  through 这种方式不支持counter_cache。

所以可以用下面的代码实现计数

本站代码

{% highlight ruby %}
class Categorization < ActiveRecord::Base
  belongs_to :post
  belongs_to :category

  after_create  :increment_counter_cache
  after_destroy :decrement_counter_cache

  private
  def decrement_counter_cache
    Category.decrement_counter("posts_count", category_id)
  end

  def increment_counter_cache
    Category.increment_counter("posts_count", category_id)
  end

end
{% endhighlight %}