---
layout: post
title: 使用to_lang翻译ruby字符串
category: ruby
tags: ruby gem
---


[github地址](https://github.com/jimmycuadra/to_lang)

我的博客就是用这个gem来翻译文章标题的

#安装

{% highlight bash %}
gem install to_lang
{% endhighlight %}

#使用

ToLang必须初始配置一个google api key  

[api key 获取地址](https://code.google.com/apis/console)



{% highlight ruby %}
require ‘to_lang’
ToLang.start(‘YOUR_GOOGLE_TRANSLATE_API_KEY’)
{% endhighlight %}

然后就可以变魔术了
{% highlight ruby %}
 > '你好'.to_english
 => "Hello" 
 > 'hotfix'.to_simplified_chinese
 => "修复" 
 > "Rails 有非常強大的路徑指派功能，讓我們看看有哪些設定方式吧".to_simplified_chinese_from_traditional_chinese
 => "Rails 有非常强大的路径指派功能，让我们看看有哪些设定方式吧" 
{% endhighlight %}

也可以直接用String#translate方法
{% highlight ruby %}
“hello world”.translate(‘es’)
=> “hola mundo”
“a pie”.translate(‘es’, :from => ‘en’)
=> “un pastel”
{% endhighlight %}

#所有支持的语言
{% highlight bash %}
to_afrikaans
to_albanian
to_arabic
to_basque
to_belarusian
to_bulgarian
to_catalan
to_simplified_chinese
to_traditional_chinese
to_croatian
to_czech
to_danish
to_dutch
to_english
to_estonian
to_filipino
to_finnish
to_french
to_galician
to_german
to_greek
to_haitian_creole
to_hebrew
to_hindi
to_hungarian
to_icelandic
to_indonesian
to_irish
to_italian
to_japanese
to_latvian
to_lithuanian
to_macedonian
to_malay
to_maltese
to_norwegian
to_persian
to_polish
to_portuguese
to_romanian
to_russian
to_serbian
to_slovak
to_slovenian
to_spanish
to_swahili
to_swedish
to_thai
to_turkish
to_ukrainian
to_vietnamese
to_welsh
to_yiddish
{% endhighlight %}