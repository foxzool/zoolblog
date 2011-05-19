---
layout: post
title: 使用disqus作为本站的留言系统
category: misc
tags: disqus
---

disqus是国外的一个强大的留言系统，不仅可以单对单进行留言，还可以使用facebook,twitter等帐号进行评论互动。

首先去他们官网进行注册  [disqus网址](http://disqus.com)
在注册后，你会得到你的网站的一个shortname，本站是zoolblog

然后在需要加入留言的地方加入下面的代码

{% highlight ruby %}
  <div id="disqus_thread"></div>
  <script type="text/javascript">
      /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
      var disqus_shortname = 'example'; // required: replace example with your forum shortname
  
      // The following are highly recommended additional parameters. Remove the slashes in front to use.
      // var disqus_identifier = 'unique_dynamic_id_1234';
      // var disqus_url = 'http://example.com/permalink-to-page.html';
  
      /* * * DON'T EDIT BELOW THIS LINE * * */
      (function() {
          var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
          dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
          (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
      })();
  </script>
  <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
  <a href="http://disqus.com" class="dsq-brlink">blog comments powered by <span class="logo-disqus">Disqus</span></a>
{% endhighlight %}

这里有三个值要注意
{% highlight bash %}
disqus_shortname #为你在网站上获得shortname,本站为zoolblog

disqus_identifier #为当前页面的唯一值，默认为当前网页url

disqus_url #为页面的显示url，默认为当前网页url
{% endhighlight %}

这里说明一下disqus_identifier和disqus_url的区别
disqus_url一般是网页的slug， 比如说post/1可以用slug方式显示的话，是post/creat-my-rails-app这样的格式，由于slug有时会变化，所以需要disqus_identifier来帮忙，这个是一个网页slug不管怎么变化都一致的值。
