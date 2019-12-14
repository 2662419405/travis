---
layout: post
title: 博客园样式
date: 2019-11-24 14:48:34
tags: [博客园,样式自定义,BLOG,jQuery]
categories: 
  - [jQuery]
thumbnail: https://cdn.jsdelivr.net/gh/TRHX/ImageHosting/ITRHX-PIC/thumbnail/hexo.png
---

> 测试网址: <a href="https://www.cnblogs.com/sunhang32/">https://www.cnblogs.com/sunhang32/</a>
>
> 实现目标: 学习更多的知识,了解更广的世界
>
> 简述原理: 自己整合并且简单修改
>
> 目前: 长期活跃的论坛之一,还在不断完善中

<!-- more -->

# 欢迎来到残梦博客园

<font color="#999">首先声明一点: 样式并不全是本人所写,是我个人整合(感觉每个人的博客都喜欢一点,所以自己整合了一下)</font>

<font color=red size=5>由于每次更新博客,都需要重新更新此文档很麻烦,所以此博客只会定期更新,如果想要使用最新版本博客园样式,请前往本人<a href="https://github.com/2662419405/cnblogs">github</a></font>

## 如果喜欢的小伙伴可以自己配置

### 首先你要有一个博客园(这个我估计我说的有点废话了)

### 在[博客园](https://www.cnblogs.com)的官网左上角开通博客园

### 博客园的个人配置页面->先申请js权限
<fancybox>
<img src="https://img2018.cnblogs.com/blog/1860563/201911/1860563-20191113210840922-512269453.png" />
</fancybox>

### 禁用页面的css样式
<fancybox>
<img src="https://img2018.cnblogs.com/blog/1860563/201911/1860563-20191113210905600-717115239.png" />
</fancybox>

### 选择页面的主题
<fancybox>
<img src="https://img2018.cnblogs.com/blog/1860563/201911/1860563-20191113211243480-623230909.png" />
</fancybox>

### 粘贴一下代码到定制页面css代码中,由于css文件较大,所以这里提供了超链接

<a href="https://blog-static.cnblogs.com/files/sunhang32/canmeng.css">css</a>

### 粘贴博客侧面公告代码

```html
<script type="text/javascript">
    window.cnblogsConfig = {
        GhVersions    : 'v1.2.0', // 版本
        blogUser      : "残梦", // 用户名
        essayCodeHighlightingType: "highlightjs",
        essayCodeHighlighting: "a11y-dark",
        homeTopImg: [
           "https://cdn.jsdelivr.net/gh/2662419405/imgPlus/o_o_wallhaven-698904.jpg"
        ],
         menuUserInfoBgImg: 'https://bndong.github.io/images/menu_bg.gif',
         menuNavList: [ // 列表数据 ['导航名称', '链接']
             ['github', 'https://github.com/2662419405'],
             ['CSDN', 'https://blog.csdn.net/qq_43268396'],
             ['技能树', 'https://shtodream.cn/about/'],
             ['留言板', 'https://shtodream.cn/message/'],
        ],
        fontIconExtend: "//at.alicdn.com/t/font_543384_ezv3l7gd9r7.css",  //字体图标扩展
        webpageTitleOnblur        : "(◍´꒳`◍)你为何狠心离去 ", // 当前页失去焦点，页面title显示文字
        webpageTitleOnblurTimeOut : 500, // 当前页失去焦点，页面title变化，延时时间，单位毫秒
        webpageTitleFocus         : "(*´∇｀*) 帅的人回来了！", // 当前页获取焦点，页面title显示文字，显示后延时恢复原title
        webpageTitleFocusTimeOut  : 2000, // 当前页获取焦点，页面title变化，延时时间，单位毫秒
        blogAvatar    : "https://cdn.jsdelivr.net/gh/2662419405/CDN@1.0/sh.jpg", // 用户头像
        blogStartDate : "2019-11-07", // 入园时间，年-月-日。入园时间查看方法,鼠标停留园龄时间上，会显示入园时间
    }
</script>
<script src="https://cdn.jsdelivr.net/gh/BNDong/Cnblogs-Theme-SimpleMemory@v1.2.0/src/script/simpleMemory.min.js"></script>
```

- 粘贴页首代码 
```html
// 此处为空
```

- 粘贴页脚代码 
```html
<!-- 滚动进度 -->
<div id="bottomProgressBar"></div>
<!-- 音乐菜单 -->
<link rel="stylesheet" href="https://blog-static.cnblogs.com/files/elkyo/APlayer.min.css">
  <div id="player" class="aplayer aplayer-withlist aplayer-fixed" data-id="3025663508" data-server="netease" data-type="playlist" data-order="random" data-fixed="true" data-listfolded="true" data-theme="#2D8CF0"></div>
  <script src="https://blog-static.cnblogs.com/files/elkyo/APlayer.min.js"></script>
  <script src="https://blog-static.cnblogs.com/files/elkyo/Meting.min.js"></script>
<!-- 网站运行时间 -->
<p style="text-align:center;"><span id="timeDate">载入天数...</span><span id="times">载入时分秒...</span></p>
<script>
    var now = new Date(); 
    function createtime() { 
        var grt= new Date("11/06/2019 17:38:00");//在此处修改你的建站时间
        now.setTime(now.getTime()+250); 
        days = (now - grt ) / 1000 / 60 / 60 / 24; dnum = Math.floor(days); 
        hours = (now - grt ) / 1000 / 60 / 60 - (24 * dnum); hnum = Math.floor(hours); 
        if(String(hnum).length ==1 ){hnum = "0" + hnum;} minutes = (now - grt ) / 1000 /60 - (24 * 60 * dnum) - (60 * hnum); 
        mnum = Math.floor(minutes); if(String(mnum).length ==1 ){mnum = "0" + mnum;} 
        seconds = (now - grt ) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum); 
        snum = Math.round(seconds); if(String(snum).length ==1 ){snum = "0" + snum;} 
        document.getElementById("timeDate").innerHTML = "本站勉强运行 "+dnum+" 天 "; 
        document.getElementById("times").innerHTML = hnum + " 小时 " + mnum + " 分 " + snum + " 秒"; 
    } 
setInterval("createtime()",250);
</script>
<!-- 右下角菜单 -->
<div id="rightMenu"></div>
   <!--看板娘 - 猫-->
  <script src="https://eqcn.ajz.miesnfu.com/wp-content/plugins/wp-3d-pony/live2dw/lib/L2Dwidget.min.js"></script>
<script>
      L2Dwidget.init({
          "model": {
              jsonPath: "https://unpkg.com/live2d-widget-model-hijiki/assets/hijiki.model.json",<!--这里改模型，前面后面都要改-->
              "scale": 1
          },
          "display": {
              "position": "left",<!--设置看板娘的上下左右位置-->
              "width": 100,
              "height": 200,
              "hOffset": 70,
              "vOffset": 0
          },
          "mobile": {
              "show": true,
              "scale": 0.4
          },
          "react": {
              "opacityDefault": 0.5,<!--设置透明度-->
              "opacityOnHover": 0.2
          }
      });
window.onload=function(){
       $("#live2dcanvas").attr("style","display:block;position: fixed; opacity: 0.7; left: 70px; bottom: 0px; z-index: 1; pointer-events: none;")
}
</script>
<!-- 线条效果 -->
<script type="text/javascript"
color="220,220,220" opacity='0.9' zIndex="-2" count="500" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js">
</script>
<script type="text/javascript" src="https://blog-static.cnblogs.com/files/sunhang32/myconsole.js"></script>
<!-- 文字显示 -->
<script type="text/javascript" src="https://files.cnblogs.com/files/sunhang32/myText.js"></script>
```



*--------------如果你对你的代码不满意的话,可以接下来自定义设置----------------*

<font color=red size=4>此处请前往<a href="https://github.com/2662419405/cnblogs">github</font>