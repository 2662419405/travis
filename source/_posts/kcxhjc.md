---
layout: post
title: 使用 Travis-CI 持续集成部署 HEXO 博客项目
date: 2019-12-20 09:24:00
tags: [Hexo,学习之旅,Github,BLOG,Travis CI,持续集成自动部署,Token]
categories: 
  - [Hexo]
thumbnail: https://cdn.jsdelivr.net/gh/TRHX/ImageHosting/ITRHX-PIC/thumbnail/hexo.png
---

> 优点
> 
> 1. 让你的项目和源码能够完全分离,即使我们的项目被误删,也可以快速找回
> 
> 2. 当我们需要重复进行某些步骤的时候
>
> 3. 直接在线编辑文件，立即生效
> 
> 4. 自动部署，同时部署到多个地方
> 
> 5. 发生错误,邮箱自动提醒

<!-- more -->

### What is Travis CI?

Travis CI

CI(Continuous Integration)翻译为持续集成。Travis CI是一个提供持续集成功能的平台，在Github上，可以添加Travis CI，当有code push时候，会推送通知到Travis，根据设置的脚本运行指定任务。

目前有两个站点:

Travis.org 对于所有public项目完全免费

Travics.com 只针对private项目，提供更多一些额外功能，如cache，并行build个数

两个站点只能看到各自的项目，不能通用。

### Why we need Travis CI?

有人可能会有疑问: 在本地写完博客，直接一个命令hexo d，不就搞定了么， 为啥要费力搞CI？

的确, 想用TravisCI来自动部署Hexo博客程序，需要不少设置（瞎折腾），为了给大伙信心，列举一些优点：

#### 优点1：直接在线编辑文件，立即生效

假设你已经发表了一篇文章，过了几天你在朋友机器上浏览发现有几个明显的错别字，对于有强迫症的，这是不能容忍的。 但你手头又没有完整的hexo+nodejs+git的开发环境，重新下载git，node，hexo配置会花费不少时间，特别不划算。

如果按照这篇完整折腾完，你可以直接用浏览器访问github个人项目仓库，直接编辑那篇post的原md文件，前后2分钟改完。 稍等片刻，你的博客就自动更新了。

#### 优点2：自动部署，同时部署到多个地方

在gitcafe是被收购之前，很多同学（包括我）都是托管在上面的，国内访问速度比Github快很多。
配合DNS根据IP位置可以自动选择导到gitcafe, 还是github，甚至你还可以部署到七牛云的静态网站。
利用Travis CI可同时更新多个仓库。

比如我的博客现在有两个站：一个部署在码云，一个部署在github。都需要我自己手动部署。

注：最后发现码云并不支持。emmmmm

#### 优点3：部署快捷方便

手动deploy需要推送public整个folder到github上，当后期网站文章、图片较多时候，对于天朝的网络，有时候连接github 就是不顺畅，经常要傻等不少上传时间。
有了CI，你可以只提交post文件里单独的md文件即可，很快很爽，谁用谁知道。

#### 优点4：bigger than bigger

你的项目Readme里面可以显示CI build图标，很酷有没有？
另外通过设置，可以在当build失败时自动发邮件提醒你。
上面的图标，如果登陆后你在Github项目里，直接点击图标，会跳转到你当前项目build的log界面，很方便。

当然有了CI，你可以做很多事情，如自动运行单元测试，成功后再deploy等等。很多项目里的持续集成基本也是这个道理。

### 开始使用

#### 准备Travis CI账号

> 注册登录,<a href="https://travis-ci.org/">travis-ci</a>,就会自动显示我们的github下面的所有仓库,点击左上角

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-29-13.png" />
</fancybox>

> 选择开启持续更新哪个仓库

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-32-22.png" />
</fancybox>

#### 准备github的Token

> 登录你的github账号,选择setting->Personal access tokens

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-34-43.png" />
</fancybox>

> 注意,这里面生成token之后,在勾选的时候,除了删库,全都勾选上,<font color="red">注意生成之后的文件一定要保存起来,token之后就不可见了</font>

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-37-34.png" />
</fancybox>

#### 在travis ci中添加我们的token

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-40-57.png" />
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-41-53.png" />
</fancybox>

> 在hexo的根目录下面添加.travis.yml,并且开始编写

```yml
anguage: node_js

node_js: stable

cache:
  directories:
  - node_modules
before_install:

  - npm install -g hexo-cli

install:
  - npm install

script:
  - hexo g 

after_script:
  - cd ./public
  - git init
  - git config user.name "sh"
  - git config user.email "2662419405@qq.com"
  - git add .
  - git commit -m "TravisCI 自动部署"
  # Github Pages
  - git push --force --quiet "https://${githubblog}@${GH_REF}" master:master

env:
  global:
    - GH_REF: github.com/2662419405/2662419405.github.io.git
  
notifications:
  email:
    - 2662419405@qq.com
    - qq2662419405@163.com
  on_success: change
  on_failure: always

```

> 上面的邮箱和用户名改成自己的,GH_REF改为自己的github地址,注意格式和我的相符,${githubblog}改为刚刚token的key

#### 测试一下

当你弄完这些之后,在hexo根目录
```git
git init
git add .
git commit -m '测试Travis ci持续化集成'
git remote add origin xxx //这个地方是你的源码地址
git push origin master
```

<fancybox>
<img src="https://cdn.jsdelivr.net/gh/2662419405/imgPlus/Snipaste_2019-12-20_10-49-50.png" />
</fancybox>

我们的测试就大功告成!!!!