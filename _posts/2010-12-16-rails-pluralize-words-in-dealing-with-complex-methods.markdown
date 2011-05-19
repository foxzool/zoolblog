---
layout: post
title: rails中处理复数单词的pluralize方法
category: rails
tags: rails ruby
---


#缘由
在日常开发中，有时候会碰到要将一些单词按照它的数量来按单复数显示    


   
所幸rails已经考虑到了这一点，在ActionView中有一个方法

{% highlight ruby %}
    There are <%= pluralize @user.size, "user" %>.  
{% endhighlight %}

  例子

{% highlight ruby %}

    pluralize(1, 'person')
    # => 1 person

    pluralize(2, 'person')
    # => 2 people

    pluralize(3, 'person', 'users')
    # => 3 users

    pluralize(0, 'person')
    # => 0 people

{% endhighlight %}
  
  深入研究pluralize方法:  
{% highlight ruby %}
    def pluralize(count, singular, plural = nil)
      "#{count || 0} " + ((count == 1 || count =~ /^1(\.0+)?$/) ? singular : (plural || singular.pluralize))
    end
{% endhighlight %}
  可以看到英语单词的单复数是由String#pluralize方法提供，这个是由ActiveSupport::Inflector提供的一个扩展方法  

  在rails console里运行  

{% highlight ruby %}
    "post".pluralize             # => "posts"
    "octopus".pluralize          # => "octopi"
    "sheep".pluralize            # => "sheep"
    "words".pluralize            # => "words"
    "CamelOctopus".pluralize     # => "CamelOctopi"  
{% endhighlight %}

  继续研究ActiveSupport::Inflector.pluralize

{% highlight ruby %}
    def pluralize(word)
      result = word.to_s.dup

      if word.empty? || inflections.uncountables.include?(result.downcase)
        result
      else
        inflections.plurals.each { |(rule, replacement)| break if result.gsub!(rule, replacement) }
        result
      end
    end
{% endhighlight %}

可以看到单词的单复数的匹配设置是在inflection.pluarls里，那要如何修改呢？
rails已经有一个配置文件了，在/paht/to/site/config/initializers/inflections.rb  

{% highlight ruby %}
    ActiveSupport::Inflector.inflections do |inflect|
      inflect.plural /^(ox)$/i, '\1en'
      inflect.singular /^(ox)en/i, '\1'
      inflect.irregular 'person', 'people'
      inflect.uncountable %w( fish sheep )
    end  
{% endhighlight %}

plural和singual是匹配单复数的通用匹配规则，irregular是处理那些特殊单词变化，uncountbale就是那些单复数一样的单词