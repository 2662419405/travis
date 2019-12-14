---
layout: post
title: 第一个接触的前端项目
date: 2019-11-20 08:16:04
tags: [我的项目,学习之旅]
categories: 
  - [PHP]
  - [Mysql]
thumbnail: https://cdn.jsdelivr.net/gh/2662419405/img/462cec538681197a8369388fed5300f5.jpg
---

> 测试网址: <a href="https://studyit.club">https://studyit.club</a>
>
> 实现目标: 简易版社团,学习资源分享,富文本论坛,空间,美图秀秀等
>
> 简述原理: 常见前端框架混合使用
>
> 目前: 由于精力有限,目前暂停维护和开发 

<!-- more -->

# Study IT .club

### 萌新报道

``` js
Hello Everybody
```

​	第一次尝试分享一个自己写的非常简单的自己社团的官网 

​	有兴趣的小伙伴可以去开一下 -------> [网站地址](https://studyit.club)

#### 效果图
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/index.png" />
</fancybox>

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/main.png" />
</fancybox>

### 语言和框架

* 数据库方面使用`Mysql` 数据库 没有事务处理 存储引擎为`MyISAM`
* 后台语言为`PHP`
* 讨论专区的框架为` BootStrap`
* 首页框架为 `jQuery`
* 谈论专区发帖的模块使用了 富文本编辑器` UEditor`
* 在个人空间主要`AJAX`滚动局部刷新
* 个人空间方面用了`QQ`表情包
* 个人设置用了美图秀秀的PC插件`crossdomain.xml`
* 个人空间使用 `Highslide.js`图片预览插件和多图片上传插件



***

### 安装和使用

* 需要挂载在本地的`PHP`服务器之上

* 推荐使用`PHPstudy`或者warm等集成开发环境

* 数据库方面配置在`connect/config.php`中,端口和数据库配置在这里面

* 所有的数据库模型都在主目录的 `数据库.txt`目录下面

* 美图秀秀插件配置:把主目录的 `crossdomain.xml`放在服务器的根目录



[项目源码](https://github.com/2662419405/Studyit-club)---->地址