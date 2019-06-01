---
title: Hexo + NexT进阶美化攻略
date: 2019-05-29 18:24:27
categories: Hexo
tags:
    - Hexo
    - NexT
    - 攻略
    - UI
copyright: true
---

## 前言

本文将介绍部署Hexo博客并启用NexT主题后一些进阶的美化技巧。美化后具体效果可以参考本站。

在本文中，**站点配置文件**指的是博客根目录下的 **_config.yml** 文件，**主题配置文件**指的是博客根目录下 **themes/next/_config.yml** 文件。

<!-- more -->

## 目录

 - 切换主题风格
 - 配置菜单
 - 配置动态背景
 - 添加页眉GitHub页面跳转
 - 配置RSS
 - 修改文章底部标签样式
 - 添加文章末尾“本文结束”说明
 - 修改代码块样式
 - 配置侧边栏社交图标
 - 配置首页文章阴影效果
 - 添加网站底部字数统计
 - 配置网站图标
 - 添加文章字数统计
 - 隐藏底部Hexo、NexT信息
 - 配置友情链接
 - 配置文章底部版权信息
 - 配置站内搜索
 - 配置Live2D动画效果

## 切换主题风格

安装NexT主题后，默认的主题风格为Muse。如要切换主题风格，打开主题配置文件，找到如下配置。

```
# Schemes
scheme: Muse  //默认主题
#scheme: Mist
#scheme: Pisces
#scheme: Gemini
```

注释掉当前的scheme，将需要切换的主题风格取消注释，重新生成博客后即可完成切换。

## 配置菜单

NexT主题默认只有两个菜单，**首页**和**归档**。

如果需要添加，在主题配置文件中，查找“**menu:**”配置项，将需要的菜单项取消注释。

如果需要添加的菜单项不在配置文件的预设菜单项中，则按照统一格式添加自定义菜单项，从**Font Awesome**网站寻找合适的图标，将图标名称写在“**||**”后。

完成菜单项的配置后，接下来需要添加新菜单项的页面。此处以 ***标签*** 菜单项为例。

打开终端定位到博客根目录，使用如下命令创建菜单项页面。

```
hexo new page "tags"
```

然后编辑博客根目录下 **source/*tags*/index.md** 文件，在其头信息中添加以下信息。

```
type: "tags"
```

## 配置动态背景

在主题配置文件中，查找“**canvas_nest:**”配置项，将其值配置为**true**即可。

## 添加页眉GitHub页面跳转

前往[GitHub Corners](http://tholman.com/github-corners/)网站，选择一款喜欢的挂饰，并拷贝其代码。

打开博客根目录下 **themes/next/layout/_layout.swig** 文件，定位到如下代码。

```
<div class="headband"></div>
```

在其下方添加上挂饰的代码。

## 配置RSS

打开终端定位到博客根目录，使用如下命令安装相关依赖。

```
npm install --save hexo-generator-feed
```

打开站点配置文件，并定位到如下代码。

```
# Extensions
## Plugins: http://hexo.io/plugins/
```

在其下方添加如下代码。

```
plugins: hexo-generate-feed
```

在主题配置文件中，查找“**rss:**”配置项，将其值配置为 **/atom.xml** 即可。

## 修改文章底部标签样式

打开博客根目录下 **themes/next/layout/_macro/post.swig** 文件，查找“**rel="tag">#**”。

将“**#**”替换为如下代码。

```
<i class="fa fa-tag"></i>
```

## 添加文章末尾“本文结束”说明

打开博客根目录下 **themes/next/layout/_macro/** 目录，在其中新建 **passage-end-tag.swig** 文件。

使用文本编辑器在该文件中添加如下内容。

```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------</div>
    {% endif %}
</div>
```

打开博客根目录下 **themes/next/layout/_macro/post.swig** 文件，在其 **post-body** 和 **post-footer** 之间（一般为 **END POST BODY** 段落后）添加如下代码。

```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```

在主题配置文件中，在任意行添加如下内容。

```
# 文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true
```

## 修改代码块样式

打开博客根目录下 **themes/next/source/css/_custom/custom.styl** 文件，添加如下代码。

```
code {
    color: #ff7600;
    background: #fbf7f8;
    margin: 2px;
}
// 大代码块的自定义样式
.highlight, pre {
    margin: 5px 0;
    padding: 5px;
    border-radius: 3px;
}
.highlight, code, pre {
    border: 1px solid #d6d6d6;
}
```

## 配置侧边栏社交图标

在主题配置文件中，搜索“**social:**”，对其取消注释，并添加自己的社交账号，从**Font Awesome**网站寻找合适的图标，将图标名称写在“**||**”后。完成后配置示例如下。

```
# Social Links.
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimeter is the target permalink.
# Value after `||` delimeter is the name of FontAwesome icon. If icon (with or without delimeter) is not specified, globe icon will be loaded.
social:
  GitHub: https://github.com/Jovany-Rong || github
  E-Mail: mailto:amphliegg@gmail.com || envelope
  知乎: https://www.zhihu.com/people/rong-chen-fei/activities || book-open
  TapTap: https://www.taptap.com/user/4323230 || gamepad  
  #Google: https://plus.google.com/yourname || google
  #Twitter: https://twitter.com/yourname || twitter
  #FB Page: https://www.facebook.com/yourname || facebook
  #VK Group: https://vk.com/yourname || vk
  #StackOverflow: https://stackoverflow.com/yourname || stack-overflow
  #YouTube: https://youtube.com/yourname || youtube
  #Instagram: https://instagram.com/yourname || instagram
  #Skype: skype:yourname?call|chat || skype

social_icons:
  enable: true
  icons_only: false
  transition: false
```

## 配置首页文章阴影效果

打开博客根目录下 **themes/next/source/css/_custom/custom.styl** 文件，添加如下代码。

```
// 主页文章添加阴影效果
 .post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
  }
```

## 添加网站底部字数统计

打开终端定位到博客根目录，使用如下命令安装相关依赖。

```
npm install hexo-wordcount --save
```

打开博客根目录下 **themes/next/layout/_partials/footer.swig** 文件，在末尾添加如下代码。

```
<div class="theme-info">
  <div class="powered-by"></div>
  <span class="post-count">博客全站共{{ totalcount(site) }}字</span>
</div>
```

## 配置网站图标

首先准备好自己需要用到的图标，共需要准备16 x 16及32 x 32两种规格的图标。图标可以从第三方网站（如[阿里巴巴矢量图标库](https://www.iconfont.cn/)等)中下载。

将图片保存在博客根目录下 **themes/next/source/images/** 目录中。

在主题配置文件中，搜索“**favicon:**”，将其中的 **small** 参数和 **medium** 参数值分别设为16 x 16及32 x 32两种规格图标的相对路径。

## 添加文章字数统计

该功能需要用到**添加网站底部字数统计**中安装的依赖，安装过程在此不赘述。

在主题配置文件中，搜索“**post_wordcount:**”，配置修改为如下所示。

```
# Post wordcount display settings
# Dependencies: https://github.com/willin/hexo-wordcount
post_wordcount:
  item_text: true
  wordcount: true
  min2read: true
  totalcount: true
  separated_meta: true
```

## 隐藏底部Hexo、NexT信息

打开博客根目录下 **themes/next/layout/_partials/footer.swig** 文件，注释掉以下这段代码。

```
<!--
<span class="post-meta-divider">|</span>

{% if theme.footer.powered %}
  <div class="powered-by">{#
  #}{{ __('footer.powered', '<a class="theme-link" target="_blank" href="https://hexo.io">Hexo</a>') }}{#
#}</div>
{% endif %}

{% if theme.footer.powered and theme.footer.theme.enable %}
  <span class="post-meta-divider">|</span>
{% endif %}

{% if theme.footer.theme.enable %}
  <div class="theme-info">{#
  #}{{ __('footer.theme') }} &mdash; {#
  #}<a class="theme-link" target="_blank" href="https://github.com/iissnan/hexo-theme-next">{#
    #}NexT.{{ theme.scheme }}{#
  #}</a>{% if theme.footer.theme.version %} v{{ theme.version }}{% endif %}{#
#}</div>
{% endif %}

{% if theme.footer.custom_text %}
  <div class="footer-custom">{#
  #}{{ theme.footer.custom_text }}{#
#}</div>
{% endif %}
-->
```

## 配置友情链接

在主题配置文件中，搜索“**Blog rolls**”，如下配置，即可添加友情链接。

```
# Blog rolls
links_icon: link
links_title: 友情链接
#links_layout: block
links_layout: inline

#links中配置成自己需要的友情链接地址
links: 
  GitHub: https://github.com/
  南京国图信息产业有限公司: http://www.gtmap.cn/
  南京国图协同办公平台: http://oa.gtis.com.cn/ 
```

## 配置文章底部版权信息

打开博客根目录下 **themes/next/layout/_macro/** 目录，在其中新建 **my-copyright.swig** 文件。

使用文本编辑器在该文件中添加如下内容。

```
{% if page.copyright %}
<div class="my_post_copyright">
  <script src="//cdn.bootcss.com/clipboard.js/1.5.10/clipboard.min.js"></script>
  
  <!-- JS库 sweetalert 可修改路径 -->
  <script src="https://cdn.bootcss.com/jquery/2.0.0/jquery.min.js"></script>
  <script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
  <p><span>本文标题:</span><a href="{{ url_for(page.path) }}">{{ page.title }}</a></p>
  <p><span>文章作者:</span><a href="/" title="访问 {{ theme.author }} 的个人博客">{{ theme.author }}</a></p>
  <p><span>发布时间:</span>{{ page.date.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>最后更新:</span>{{ page.updated.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>原始链接:</span><a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ page.permalink }}</a>
    <span class="copy-path"  title="点击复制文章链接"><i class="fa fa-clipboard" data-clipboard-text="{{ page.permalink }}"  aria-label="复制成功！"></i></span>
  </p>
  <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" title="Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)">署名-非商业性使用-禁止演绎 4.0 国际</a> 转载请保留原文链接及作者。</p>  
</div>
<script> 
    var clipboard = new Clipboard('.fa-clipboard');
    $(".fa-clipboard").click(function(){
      clipboard.on('success', function(){
        swal({   
          title: "",   
          text: '复制成功',
          icon: "success", 
          showConfirmButton: true
          });
    });
    });  
</script>
{% endif %}
```

打开博客根目录下 **themes/next/source/css/_common/components/post/** 目录，在其中新建 **my-copyright.styl** 文件。

使用文本编辑器在该文件中添加如下内容。

```
.my_post_copyright {
  width: 85%;
  max-width: 45em;
  margin: 2.8em auto 0;
  padding: 0.5em 1.0em;
  border: 1px solid #d3d3d3;
  font-size: 0.93rem;
  line-height: 1.6em;
  word-break: break-all;
  background: rgba(255,255,255,0.4);
}
.my_post_copyright p{margin:0;}
.my_post_copyright span {
  display: inline-block;
  width: 5.2em;
  color: #b5b5b5;
  font-weight: bold;
}
.my_post_copyright .raw {
  margin-left: 1em;
  width: 5em;
}
.my_post_copyright a {
  color: #808080;
  border-bottom:0;
}
.my_post_copyright a:hover {
  color: #a3d2a3;
  text-decoration: underline;
}
.my_post_copyright:hover .fa-clipboard {
  color: #000;
}
.my_post_copyright .post-url:hover {
  font-weight: normal;
}
.my_post_copyright .copy-path {
  margin-left: 1em;
  width: 1em;
  +mobile(){display:none;}
}
.my_post_copyright .copy-path:hover {
  color: #808080;
  cursor: pointer;
}
```

打开博客根目录下 **themes/next/layout/_macro/post.swig** 文件，定位到如下代码。

```
    {% if theme.wechat_subscriber.enabled and not is_index %}
      <div>
        {% include 'wechat-subscriber.swig' %}
      </div>
    {% endif %}
```

在其上方添加如下代码。

```
<div>
      {% if not is_index %}
        {% include 'my-copyright.swig' %}
      {% endif %}
</div>
```

打开博客根目录下 **themes/next/source/css/_common/components/post/post.styl** 文件，在其末尾添加如下代码。

```
@import "my-post-copyright"
```

打开站点配置文件，搜索 **URL** ，配置为如下所示。

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://wenmobo.github.io/  //你的网站地址
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

以后写的Markdown文章头信息中，添加 **copyright: true** 即可。

## 配置站内搜索

打开终端定位到博客根目录，使用如下命令安装相关依赖。

```
npm install hexo-generator-search --save
```

再安装另一个依赖。

```
npm install hexo-generator-searchdb --save
```

在站点配置文件中，添加如下内容。

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

在主题配置文件中，搜索 **local_search:** 配置项，将 **enable** 参数配置为 **true** 即可。

## 配置Live2D动画效果

打开终端定位到博客根目录，使用如下命令安装相关依赖。

```
npm install --save hexo-helper-live2d
```

自己制作或从[第三方](https://github.com/xiazeyu/live2d-widget-models.git)下载需要的Live2D动画。

下载好之后将所有动画模板拷贝到博客根目录下node_modules目录中。

在站点配置文件中，添加如下配置。

```
live2d:
  enable: true
  pluginModelPath: assets/
  model:
    use: live2d-widget-model-epsilon2_1  #模板目录，在node_modules里
  display:
    position: right
    width: 150 
    height: 300
  mobile:
    show: false  #是否在手机进行显示
```