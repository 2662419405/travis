---
layout: post
title: 加速自己的hexo，使用GitHub+Coding实现国内外网站加速
date: 2019-11-30 13:19:28
tags: [Hexo,学习之旅,Github,Coding,BLOG]
categories: 
  - [Hexo]
thumbnail: https://cdn.jsdelivr.net/gh/TRHX/ImageHosting/ITRHX-PIC/thumbnail/hexo.png
---

> 基于Github+Coding实现国内外网站加速，让你的用户访问飞起来

<!-- more -->

> 在配置好hexo之后，我们发现访问网站很慢，但又不是我们使用的主题的问题，那么就是网络环境的影响，即使我们使用了CDN加速，但还是没有我们国内的网站访问起来快速，（听说去美国的服务器要经过太平洋下面的区域,那访问起来也算是挺快了啊）,那我们就可以让我们的网站在国内和国外各备份一份,然后国内的用户访问国内的,国外的用户访问国外的网站

## 1. 创建项目

进入 <a href="https://coding.net/" target="_blank">Coding 官网</a>点击个人版登陆，没有账号就注册一个并登录，由于 Coding 已经被腾讯收购了，所以登录就会来到腾讯云开发者平台，点击创建项目
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-39-57.png" />
</fancybox>

项目名称建议和你的用户名一致，这样做的好处是：到时候可以直接通过 `user_name.coding.me` 访问你的博客，如果项目名与用户名不一致，则需要通过 `user_name.coding.me/project_name` 才能访问，项目描述可以随便写
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-42-25.png" />
</fancybox>

## 2. 配置公匙

配置 SSH 公钥方法与 GitHub Pages 的方式差不多，点击你的头像，依次选择【个人设置】-【SSH公钥】-【新增公钥】
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-44-44.png" />
</fancybox>

PS：公钥储存位置一般在 C:\Users\用户名\.ssh 目录下的 id_rsa.pub 文件里，用记事本打开复制其内容即可

## 3.配置 _config.yml
进入你的项目，在右下角有选择连接方式，选择 SSH 方式（HTTPS 方式也可以，但是这种方式有时候可能连接不上，SSH 连接不容易出问题），一键复制，然后打开你本地博客根目录的 `_config.yml` 文件，找到 `deploy` 关键字，添加 coding 地址：coding: `git@git.dev.tencent.com:user_name/user_name.git`，也就是刚刚复制的 SSH 地址
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-46-33.png" />
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-47-51.png" />
</fancybox>

添加完成后先执行命令 `hexo clean` 清理一下缓存，然后执行命令 `hexo g -d` 将博客双线部署到 Coding Pages 和 GitHub Pages，如下图所示表示部署成功：

## 4.开启 Coding Pages
进入你的项目，在代码栏下选择 Pages 服务，一键开启 Coding Pages，等待几秒后刷新网页即可看到已经开启的 Coding Pages，
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-49-56.png" />
</fancybox>

## 5.绑定域名并开启 HPPTS
首先在你的域名 DNS 设置中添加一条 CNAME 记录指向 Coding给的地址，解析路线选择默认，将 GitHub 的解析路线改为境外，这样境外访问就会走 GitHub，境内就会走 Coding，也有人说阿里云是智能解析，自动分配路线，如果解析路线都是默认，境外访问同样会智能选择走 GitHub，境内走 Coding，我没有验证过，有兴趣的可以自己试试，我的解析如下图所示：
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-52-33.png" />
</fancybox>

然后点击静态 Pages 应用右上角的设置，进入设置页面，这里要注意，如果你之前已经部署到了 GitHub Pages 并开启了 HTTPS，那么直接在设置页面绑定你自己的域名，SSL/TLS 安全证书就会显示申请错误，如下图所示，没有申请到 SSL 证书，当你访问你的网站时，浏览器就会提示不是安全连接

申请错误原因是：在验证域名所有权时会定位到 Github Pages 的主机上导致 SSL 证书申请失败

正确的做法是：<font color=red>先去域名 DNS 把 GitHub 的解析暂停掉，然后再重新申请 SSL 证书</font>，大约十秒左右就能申请成功，然后开启强制 HTTPS 访问
<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-11-30_13-58-18.png" />
</fancybox>

<a href="https://www.itrhx.com/2019/09/16/A47-hexo-deployed-to-github-and-coding/">参考</a>