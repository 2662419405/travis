---
layout: post
title: 用pjax让你的页面加载飞起来!
date: 2019-12-20 20:25:48
tags: [性能优化,pjax,ajax,html5,nprogress,github,loading]
categories: 
  - [Hexo]
thumbnail: https://cdn.jsdelivr.net/gh/TRHX/ImageHosting/ITRHX-PIC/thumbnail/hexo.png
---

> 什么是pjax?
>
> pjax = ajax + pushState
>
> 目的!
> 
> 让页面加载飞起来

<!-- more -->

## 什么是pjax?

pjax = ajax + pushState

> 通过ajax让页面进行局部刷新,然后通过pushstate让url发生改变,再让pushState,让页面产生一个回退的记录,从而让页面的性能进行大幅度的优化

### 简单demo感受一下

> 准备两个页面 index.html content.html

1. index.html
```html
<!DOCTYPE html>
<html class="font-auto" lang="zh-cmn-hans">
<head>
    <meta charset="UTF-8">
    <title>残梦博客园</title>
    <script src="https://cdn.jsdelivr.net/npm/pjax/pjax.js"></script>
</head>
<body>
	<loader>
	    <div class="plane"></div>
	</loader>
	<header>
	  页眉内容...
	</header>
	<main>
	  <a href="content.html">中间</a>
	</main>
	<footer>
	  页尾内容...
	</footer>
</body>
<script>
	var pjax = new Pjax({
	  // 在页面进行 PJAX 时需要被替换的元素或容器，一条一个 CSS 选择器，数组形式
	  selectors: [
	    "title",
	    "meta[name=description]", // 如果是全部 meta 替换的话，只需要写 meta
	    "main"
	  ],
	  cacheBust: false
	})
</script>
</html>
```

2. content.html
```html
<!DOCTYPE html>
<html class="font-auto" lang="zh-cmn-hans">
<head>
    <meta charset="UTF-8">
    <title>残梦博客园</title>
    <script src="https://cdn.jsdelivr.net/npm/pjax/pjax.js"></script>
</head>
<body>
	<loader>
	    <div class="plane"></div>
	</loader>
	<header>
	  页眉内容...
	</header>
	<main>
	  <a>中间</a>
	</main>
	<footer>
	  页尾内容...
	</footer>
</body>
<script>
	var pjax = new Pjax({
	  // 在页面进行 PJAX 时需要被替换的元素或容器，一条一个 CSS 选择器，数组形式
	  selectors: [
	    "title",
	    "main"
	  ],
	  cacheBust: false
	})
</script>
</html>
```

发现真的是神速啊,用f12看了一下,发现就中间的dom结构发生了改变(这里面也就是main发生了改变),页面的js,css脚本也不用重新下载

### 深度学习一下

感受到了他的牛逼之后,我们不如让我们的页面也能这样去渲染,岂不是很快

> 在<a href="https://github.com/">github</a>上面,我们可以找到pjax,主要分为两个版本

1. 不需要jquery插件的pjax  (这里面我们使用这种方式)
2. 需要jquery的pjax

#### 引入脚本

引入pjax的CDN加速脚本
```js
<script src="https://cdn.jsdelivr.net/npm/pjax/pjax.js"></script>
```

首先我们要实例化Pjax,并且传入一个对象
第一个参数一般是指我们想让点击哪里去触发pjax(这里面只能指向a或者form)
第二个参数为一个选择器数组,我们传递的是我们需要更新的dom节点(更新的dom越少,性能越好,当然尽量不要写重复的结构)
```js
var pjax = new Pjax({
      elements: "a",
      selectors: [
        "title",
        ".l_main",
        ".l_side .toc-wrapper",
        "#links",
        ".comments",
        "#pages",
      ]
})
```

这样我们就成功的配置完了pjax
但是新的页面可能需要渲染的dom结构很大,可能产生一瞬间的停顿,这样就会让页面像卡主了一样,没有给用户良好的反馈,我们可以自己做一个loading的加载或者使用nprogress,据说github就是使用的nprogress+pjax(发现自己之前真的是故落寡闻了)

#### 优化加载

准备css文件
```css
.loading{display:none}
.loading{height:100%;width:100%;position:fixed;top:0;left:0;z-index:999999;background-color:rgba(250,250,250,.9)}
.loading img{width: 280px;height:210px;position: relative;top: 45%;left: 50%;margin-left:-140px;margin-top: -105px;}
#loader{display: block; position: relative; left: 50%; top: 50%; width: 150px; height: 150px; margin: -75px 0 0 -75px; border-radius: 50%; border: 3px solid transparent; border-top-color: #ff5a5a; -webkit-animation: spin 1s linear infinite; animation: spin 1s linear infinite;}
#loader:before{content: ""; position: absolute; top: 5px; left: 5px; right: 5px; bottom: 5px; border-radius: 50%; border: 3px solid transparent; border-top-color: #5af33f; -webkit-animation: spin 3s linear infinite; animation: spin 3s linear infinite;}
#loader:after{content: ""; position: absolute; top: 15px; left: 15px; right: 15px; bottom: 15px; border-radius: 50%; border: 3px solid transparent; border-top-color: #6dc9ff; -webkit-animation: spin 2s linear infinite; animation: spin 2s linear infinite;}
@-webkit-keyframes spin{0%{-webkit-transform: rotate(0deg); -ms-transform: rotate(0deg); transform: rotate(0deg);} 100%{-webkit-transform: rotate(360deg); -ms-transform: rotate(360deg); transform: rotate(360deg);}}
@keyframes spin{0%{-webkit-transform: rotate(0deg); -ms-transform: rotate(0deg); transform: rotate(0deg);} 100%{-webkit-transform: rotate(360deg); -ms-transform: rotate(360deg); transform: rotate(360deg);}}
```

准备一个html结构的div,选择器的名字和上面对应上就好,怎么写就看个人爱好了
```html
<div class="loading"><div id="loader"></div></div>
```

准备一个js
```js
// 开始 PJAX 执行的函数
document.addEventListener('pjax:send', function (){
      $(".loading").css("display", "block");
});

// PJAX 完成之后执行的函数
document.addEventListener('pjax:complete', function (){
     $(".loading").css("display", "none");
});
```

这样子我们的页面就可以进行快速跳转了,主需要渲染一部分哦!

效果可以在我的<a href="https://shtodream.cn/">个人博客</a>上面去看