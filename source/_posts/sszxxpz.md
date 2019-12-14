---
layout: post
title: 史上最详细配置HTTPS
date: 2019-11-27 21:21:44
tags: [HTTPS,SSL,网络安全,CDN,服务器,域名]
categories: 
  - [网络安全]

thumbnail: https://cdn.jsdelivr.net/gh/TRHX/ImageHosting/ITRHX-PIC/thumbnail/combat.png
---

> 给自己的博客(或者自己的服务器)配置一个免费的ssl证书,通过https访问
>
> 参考文档: https://support.huaweicloud.com/scm_faq/scm_01_0023.html
>
> 当然还是有很多的坑
>
> 让自己的服务器也加上锁吧!

<!-- more -->

> HTTP（超文本传输协议），是一个基于请求与响应，无状态的，应用层的协议，常基于TCP/IP协议传输数据，互联网上应用最为广泛的一种网络协议，所有的WWW文件都必须遵守这个标准。设计HTTP的初衷是为了提供一种发布和接收HTML页面的方法。

> HTTPS（超文本传输安全协议），是以安全为目标的HTTP通道，简单讲是HTTP的安全版。即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。它是一个URI scheme（抽象标识符体系），句法类同http:体系。用于安全的HTTP数据传输。

### 预览三种网站的效果

- 普通的http网站 <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-41-53.png" /></fancybox>

- https的网站 <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-43-02.png"></fancybox>

- https+ssl证书的网站(也就是本网站) <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-43-45.png"></fancybox>

### 获得SSL证书

- 我选择的华为云的ssl证书

- 证书一般是收费的,当然现在有很多网站推出了白嫖的ssl证书,虽然没有正常的ssl证书那样有很多安全,但是可以证明网站备案等

- 在华为云头部搜索"免费证书"

- <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-47-52.png" /></fancybox>

- 这里我们直接购买ssl证书,价格为0,购买之后,我们会收到一个qq邮箱提醒

- <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-51-18.png"></fancybox>

- 我们点击下方的链接,用邮箱给我们的账号密码选择登录

- <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-52-43.png"></fancybox>

- 如果是第一次访问,需要写一下东西,配置完之后如上图

- <fancybox><img src="https://cdn.jsdelivr.net/gh/2662419405/img/Snipaste_2019-11-27_21-54-16.png"></fancybox>

- 我们下载之后,按照<a href="https://support.huaweicloud.com/scm_faq/scm_01_0023.html">这个文档进行配置

### 如果你没有遇到问题,那么你很强,就不需要继续往下看了

### 开始踩坑

> 第一个遇到的坑就是 `./Nginx -s reload` 重启Nginx的时候,会出现一个ssl模板没有找到的错误
>
> ## 解决方式
>
> ```js
> # 进入到/usr/local/nginx-1.14.2（注：是nginx的源码包的目录），执行以下命令
> ./configure --with-http_ssl_module
>  
> # 注意这里只能用make 而不要用make install，因为执行make install是覆盖安装的意思
> make
> 
> 先备份旧的nginx
> cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx_bak
> 
> 复制新生成的文件到安装路径：
> cp ./objs/nginx /usr/local/nginx/sbin/
> ./nginx -s reload  #进行重启
> ```

> 继续采坑中配置完之后发现,有了ssl证书,但是没有那个绿色的小锁头,很奇怪了
>
> 主要是由于页面使用了非`https`协议的文件,比如说`<img src="http:xxxx" />`,就会产生这个原因,那么我们把页面的`http`全部改写为`https`就发现我们的网站恢复了