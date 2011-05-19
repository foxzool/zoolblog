---
layout: post
title: 我的autotest配置
category: rails
tags: rails test
---

放在 ~/.autotest里， 起到统一配置

其中我没有用mac，所以注释掉了growl的相关配置

{% highlight ruby %}
#require "autotest/growl"
#require 'redgreen/autotest'
require "autotest/restart"
require 'autotest/timestamp'
require 'autotest_notification'
SPEAKING = false
DOOM_EDITION = false
BUUF = false
PENDING = false
STICKY = false
SUCCESS_SOUND = ''
FAILURE_SOUND = ''


Autotest.add_hook :initialize do |autotest|
  %w{.git .svn .hg .DS_Store ._* vendor tmp log doc}.each do |exception|
    autotest.add_exception(exception)
  end
end
#
#module Autotest::Growl
#
#  def self.growl title, msg, img, pri=0, stick="" 
#    system "growlnotify -n autotest --image #{img} -p #{pri} -m #{ msg.inspect} #{title} #{stick}" 
#  end
#  #
#  Autotest.add_hook :ran_command do |autotest|
#    results = [autotest.results].flatten.join("\n")
#    output = results.slice(/(\d+)\s+examples?,\s*(\d+)\s+failures?(,\s*(\d+)\s+pending)?/) 
#    if output  =~ /[1-9]\sfailures?/
#      growl "FAIL:", "#{output}", "~/Library/autotest/fail.png", 2, "-s" 
#    elsif output  =~ /[1-9]\spending?/
#      growl "PENDING:", "#{output}", "~/Library/autotest/pending.png", 2, "-s" 
#    else
#      growl "PASS:", "#{output}", "~/Library/autotest/pass.png" 
#    end
#  end
#
#end
{% endhighlight %}