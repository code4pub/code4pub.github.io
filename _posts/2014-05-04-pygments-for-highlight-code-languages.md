---
layout: post
title: "使用Jekyll原生代码高亮插件Pygments"
description: "Jekyll使用pygments对代码进行高亮显示，需要安装python支持Pygments"
category: tech
tags: [jekyll]
---
{% include JB/setup %}

##准备工作
- 安装python 2.7
[Python](https://www.python.org/downloads/windows/)

**jekyll 1.5.1还不支持python3**

- 设置环境变量
将python的安装目录和\Scripts加入`PATH`中
- 安装pip
1. 下载[get-pip.py](https://raw.githubusercontent.com/pypa/pip/master/contrib/get-pip.py)
2. 安装pip
`python get-pip.py`
3. 【可选】配置pip加速源
在用户目录下创建~\pip\pip.ini
修改内容为：
{% highlight ini %}
[global]
index-url = http://pypi.douban.com/simple

[install]
find-links = http://pypi.douban.com/simple https://pypi.python.org/simple/pygments
{% endhighlight %}

##安装Pygments
执行`pip Pygments`

**如果出现mimetypes.py的UnicodeEncodeError，可以修改Python27\Lib\mimetypes.py中的编码处理方式**
{% highlight Python %}
        if sys.getdefaultencoding() != 'gbk':
        	reload(sys)
        	sys.setdefaultencoding('gbk')
        
        default_encoding = sys.getdefaultencoding()
{% endhighlight %}

## 生成Jekyll所需的Pygments CSS文件
- 在工程目录下，执行
`pygmentize -S default -f html > assets\themes\twitter\css\pygments.css`
- 确认`_config.yml`的pygments设置
`pygments: true`

##修改default.html
路径：`_includes\themes\twitter\default.html`

{% highlight html %}
<link href="{{ ASSET_PATH }}/css/pygments.css?body=1" rel="stylesheet" type="text/css" media="all">
{% endhighlight %}

##效果
{% highlight JavaScript %}
<script type="text/javascript">
function foo(){
  var x = "";
  var time = new Date().getHours();
  
  if (time < 20){
    x = "Good day";
  }else{
    x = "Good evening";
  }
  
  console.log(x);
}
</script>
{% endhighlight %}
