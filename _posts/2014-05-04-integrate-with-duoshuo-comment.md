---
layout: post
title: "在Github Pages中集成多说评论插件"
description: "在jekyllbootstrap中集成多说社会化评论组件，需要"
category: tech
tags: [jekyll]
---
{% include JB/setup %}

## 创建多说账号
- 在[多说](http://duoshuo.com)中，创建账号。
- 创建站点。`多说域名`为之后用到的short_name。
- 设置站点。审核规则，垃圾评论，评论框选项等。

## 修改相关源文件
- `_config.yml`
{% highlight text %}
  comments :
    provider : duoshuo
    duoshuo :
      short_name : come
    disqus :
      short_name : jekyllbootstrap
{% endhighlight %}


- `_includes\JB\comments`
{% highlight text %}
{% raw %}
{% case site.JB.comments.provider %}

{% when "duoshuo" %}
  {% include JB/comments-providers/duoshuo %}
{% when "disqus" %}
  {% include JB/comments-providers/disqus %}
{% endraw %}
{% endhighlight %}

##创建duoshuo文件
- 创建`_includes\JB\comments-providers\duoshuo`
- 内容为：

{% highlight html %}
{% raw %}
<!-- 多说评论框 start -->
	<div class="ds-thread" data-thread-key="{{ page.url }}" data-title="{{ page.title }}" data-url="{{site.production_url}}{{ page.url }}"></div>
<!-- 多说评论框 end -->
<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
var duoshuoQuery = {short_name:"{{ site.JB.comments.duoshuo.short_name }}"};
	(function() {
		var ds = document.createElement('script');
		ds.type = 'text/javascript';ds.async = true;
		ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
		ds.charset = 'UTF-8';
		(document.getElementsByTagName('head')[0] 
		 || document.getElementsByTagName('body')[0]).appendChild(ds);
	})();
	</script>
<!-- 多说公共JS代码 end -->
{% endraw %}
{% endhighlight %}

**注**`data-thread-key`设置为`page.url`