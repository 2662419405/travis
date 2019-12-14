---
layout: post
title: DIY自己的评论表情包
date: 2019-12-03 20:55:45
tags: [表情包,DIY,volantis,Hexo]
thumbnail: https://cdn.jsdelivr.net/gh/xaoxuu/volantis@1.0/img/weibo/dog7.png
---

> 定制属于自己的专属表情包,虽然Voline有自己的一套表情包,但是感觉不是很好看,那么现在就来自己定制一下吧

<!-- more -->

## 1. 下载js文件

这个是建立在valine的基础上修改的文件,所以和valine使用方式一样,就是导入的js改变一下即可
先clone一下<a href="https://github.com/2662419405/volantis" target="_blank">仓库</a>到本地,这个我就不说了

## 2. 本地测试

在clone的目录下面,新建一个html文件
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-03_21-19-51.png" />
</fancybox>
导入js运行html
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-03_21-20-57.png" />
</fancybox>
测试一下js是否生效了
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-03_21-21-19.png" />
</fancybox>

## 3. 加入自己想要的表情包

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-03_21-27-34.png" />
</fancybox>

重新打开html页面,发现表情包添加了,但是变成了下面这样

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-03_21-27-54.png" />
</fancybox>

微调css文件,加入下面的css文件调整,当然可以根据自己的个人爱好添加

```css
.l_main #comments .vemojis i .emoji {
    height: 24px;
    margin-top: 6px;
    background: transparent;
}
.l_main #comments .vemojis i {
    width: auto;
    height: 36px;
    padding: 0;
    margin: 8px 8px 0 8px;
}
```

## 4. 修改Hexo

这个表情包本身就是valine的表情包的扩展,所以直接修改hexo中导入的js文件即可
把修改好的文件上传到自己的服务器上面,如果没有可以参考<a href="https://github.com/2662419405/CDN">Github+jsDelivr</a>上传到CDN
我的是在`themes\material-x\layout\_partial\script.ejs`文件中,然后直接`Ctrl+F`搜索找到替换成自己的文件即可,我的js文件是`https://cdn.jsdelivr.net/gh/2662419405/CDN/volantisPlus.js`

* 最好把这个volantisPlus压缩一下,本人太懒了,就没弄,经过上面的配置,你也拥有了自己的DIY表情包,美滋滋啊