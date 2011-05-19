---
layout: post
title: rails的定时任务插件whenever
category: rails
tags: rails gem
---

在做web应用时，有时会需要定时做一些操作，如发邮件，统计信息等。
这些都是需要放在后台来执行, whenever就是这样的一个插件，使用ruby强大的DSL， 高效的配置生成定时任务。
注意，whenever使用的是crontab定时器，所以这个gem在windows上无效。

[github地址](https://github.com/javan/whenever)

#安装
{% highlight bash %}
gem 'whenever', :require => false
{% endhighlight %}

#开始配置
{% highlight bash %}
cd /path/to/myapp/
wheneverize .
#会在config目录下生成一个schedule.rb文件
{% endhighlight %}

#配置文件说明
每个配置都是在一个叫every的block里面配置
运行频率 .minutes, .hours, .days, .months
可以运行任务 runner rake command 三种
#例子
{% highlight bash %}
#每隔10分钟运行一次
every 10.minutes do
  #等同于 rails runner MyModel.some_process
  runner "MyModel.some_process"
  #等同于 rake my:rake:task
  rake "my:rake:task"  
  #等同于在终端执行 /usr/bin/my_great_command
  command "/usr/bin/my_great_command" 
end
{% endhighlight %}

whenever默认使用production环境，可以在配置文件里另外定义
{% highlight bash %}
  set :environment, :autotest
  #或单独指定
  runner "MyModel.some_process", :environment => :autotest
{% endhighlight %}

#高级配置
#使用at参数来指定分钟
{% highlight bash %}
#每隔两个小时23分钟
every 2.hours, :at => 23 do
#每隔两天在上午4:30
every 2.days, :at => '4:30am' do
#每周五晚从05:00到23:45每隔15分钟
every :friday, :at => ('05'..'23').to_a.collect {|x| ["#{x}:00","#{x}:15","#{x}:30","#{x}:45"]}.flatten do
{% endhighlight %}

#与Capistrano结合
编辑Capistrano的配置文件config/deploy.rb, 加入
{% highlight bash %}
require "whenever/capistrano"
...
after "deploy:symlink", "deploy:update_crontab"
  namespace :deploy do
    desc "Update the crontab file"
    task :update_crontab, :roles => :db do
      run "cd #{release_path} && whenever --update-crontab #{application}"
    end
  end
{% endhighlight %}