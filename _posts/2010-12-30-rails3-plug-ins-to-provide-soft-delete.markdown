---
layout: post
title: rails3中提供软删除的插件
category: rails
tags: rails
---
[github地址](https://github.com/teambox/immortal)

有时候，我们希望一条记录删除后仍旧保留在数据库里，这样我们可以在日后还有反悔查询的机会。

P.S. 在rails2时代， 这个功能由 acts_as_paranoid  这个插件实现.

代码胜千言
#安装
在Gemfile里加入插件配置
{% highlight bash %}
gem 'immortal'
{% endhighlight %}

在你要做软删除的model里引用插件
{% highlight bash %}
class User < ActiveRecord::Base
  include Immortal
end
{% endhighlight %}

在users表的字段上加上deleted这个字段
{% highlight bash %}
rails g migration AddDeletedToUser deleted:boolean


class AddDeletedToUser < ActiveRecord::Migration
  def self.up
    add_column :users, :deleted, :boolean
  end

  def self.down
    remove_column :users, :deleted
  end
end

{% endhighlight %}

在控制台里测试
{% highlight bash %}
>user = User.create(:username => 'zool')
 => #<User id: 1, username: "zool", created_at: "2010-12-30 12:09:42", updated_at: "2010-12-30 12:09:42", deleted: nil>
>user.destroy
>User.all => # []
>User.find_by_sql("select * from users;")
 => [#<User id: 1, username: "zool", created_at: "2010-12-30 12:09:42", updated_at: "2010-12-30 12:09:42", deleted: true>] 
>User.where("id = 1").to_sql
 => "SELECT \"users\".* FROM \"users\" WHERE ((\"users\".\"deleted\" IS NULL OR \"users\".\"deleted\" = 'f')) AND (id = 1)"
{% endhighlight %}