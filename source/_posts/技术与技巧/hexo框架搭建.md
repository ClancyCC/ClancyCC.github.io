---
title: Hexo框架的搭建
date: 2022-04-14 15:22:00
updated: #啥也不写反而会自动更新
tags:
categories: 技术与技巧
keywords: 
description:
top_img:
comments: true
cover: /img/hexo2.jpg #应用于首页的文章标题封面，空白时默认采用主题配置文件中89/92行的参数，可选false
toc: #目录，默认true
toc_number: true #目录是否添加序号，配置文件中为false
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside: true
---
因为最近在[我的闲鱼平台](https://h5.m.goofish.com/app/idleFish-F2e/fish-mini-pha/detail.html?id=671451514245&ut_sk=1.YjSP7wUtEt0DAAFj5w4toHwK_12431167_1650822238007.Copy.detail.671451514245.2140905147&forceFlush=1&ownerId=448d6da334799d86a1eb3d74cbb9c96d&un=dee6729e812c40bda8fb54add16a2d54&share_crt_v=1&un_site=77&spm=a2159r.13376460.0.0&sp_abtk=common_xianyu_commonInfo&sp_tk=NzFncTJSdHQ5ZXY%3D&cpp=1&shareurl=true&short_name=h.fJgxHlU&bxsign=scdElZNSlYQN2hE1pLD2xfPBi2TUSz90vKjbSVqU8rcZMrQXlkwVWzTRB82jq2Z-UKlaEXJorHq0WhIT3x86e9Oh33rRgZk5YVzSZgpB4IrDCAdj7jWLH84E9aaSX2g5uMW&tk=71gq2Rtt9ev&app=chrome)帮助别人远程安装hexo博客框架，弄了几次下来觉得还是自己吧这个过程写下来比较好。
先声明，下文中nodejs的安装路径为`D:\Nodejs`，所有博客文件放在`D:\Blog`，github的用户名是`MYNAME123`，注册邮箱是`you@example.com`。

# nodejs和git的安装
nodejs下载网址：https://nodejs.org/zh-cn/download/
git下载网址：https://git-scm.com/downloads
根据自己的需求选择对应版本就好了，安装过程就是无限下一步。但是一定要注意好nodejs的安装路径，比如`D:\Nodejs`

使用下列命令检查nodejs是否安装成功，返回版本号则为成功。（新版本nodejs安装的同时会相应安装npm，所以可以同时检查）
```cmd
//在命令行中输入
node -v
npm -v

//在git bash中，桌面右击/显示更多选项(win11)/Git Bash Here
git --version
```

# nodejs环境变量的配置
这一步我看到有很多攻略，但是时而正确时而报错。建议根据我下面来：
假设你的安装路径为`D:\Nodejs`，那在这个路径下新建两个文件夹，分别命名为`node_global`和`node_cache`，之后在命令行内输入：
```cmd
npm config set prefix "D:\Nodejs\node_global"
npm config set cache "D:\Nodejs\node_cache"
```
打开：开始/设置（或者win+I）/高级系统设置（可以在搜索框中搜索）/环境变量
在上面的用户变量中，打开Path，新建并输入`D:\Nodejs\node_global`
在下面的系统变量中，新建变量名为NODE_PATH，变量值为`D:\Nodejs\node_global\node_modules`
Nodejs环境变量的配置除了安装一个组件之外，没有很好的检查方法。这里我已经帮多个人弄了很多次了，琢磨出来目前这个应当是没有问题的。

# 安装hexo
```cmd
npm install hexo-cli -g
//检查是否安装成功则输入，返回各个组件的版本号则为安装成功
hexo -v
```
## Bug No.1
```cmd
npm ERR! code EPERM
npm ERR! syscall mkdir
npm ERR! path D:/XXXXXXXXXXXXX
```
可以找到并删除`C:\Users\.npmrc`文件
或者直接采用命令：
```cmd
npm cache clean --force
```

## Bug No.2
'hexo' 不是内部或外部命令，也不是可运行的程序
说明是环境变量配置错误，建议回看上文“nodejs环境变量的配置”

# 建立仓库并生成SSH KEYS
在github中注册账号，并选择建立新仓库repository
假设你的用户名为MYNAME123，那么将仓库命名为`MYNAME123.GitHub.io`，建议添加readme.md文件

>确认好你的blog文件存放的位置，例如`D:\Blog`，那么在此处右击选择“git bash here”
>建议以后任何涉及到博客的内容，都从这个位置开始“git bash here”。

下面输入的邮箱为注册github的邮箱，一共回车4次
```bash
ssh
ssh-keygen -t rsa -C "you@example.com"
```
打开github个人主页，点击头像，`Settings/SSH and GPG keys/New SSH key`。title任意，key中输入id_rsa.pub文件内的所有内容，路径为`C:\Users\Administrator（或者是你自己的用户名）\.ssh\id_rsa.pub`
可以用下面的命令，检查是否绑定好了SSH KEYS，要求输入时输入yes
```bash
ssh -T git@github.com
```

# 本地初始化博客
打开blog文件存放的位置，例如`D:\Blog`，那么在此处右击选择“git bash here”
```bash
hexo init
```
>请注意，从2020年10月1日以后，github宣布所有仓库都将采用[main]来取代原来的[master]分支。所以这一步骤至关重要！

初始化完毕后，找到你的系统配置文件`D:\Blog\_config.yml`，将文件末尾进行修改，需要将用户名改成你自己的。
```yaml
deploy:
  type: git
  repository: https://github.com/MYNAME123/MYNAME123.github.io.git
  branch: main
```

# 设置github令牌，将博客发布到服务器中
打开github个人主页，点击头像，打开`Settings/Developer Settings/Personal access tokens/Generate new token`
title随意，勾选所有选项，有效时间里选30天或者更多都可以，点击绿色按钮`Generate token`。生成完毕后，把绿色勾号后面的所有字符给复制上。这一串字符就是你的令牌，建议永久保存好，有可能每次上传服务器都要用到。

安装hexo-deployer-g组件(注意下面是hexo-deployer-git而不是hexo-deployer-g，后者会报错code 404)，它帮助将文件上传到服务器中。
```bash
npm install hexo-deployer-git --save
```

## 最后一步！！！
```bash
git config --global user.name "MYNAME123"
git config --global user.email "you@example.com"
hexo g//生成页面文档
hexo d//上传至服务器
```
此后会出现弹窗，根据情况选择。但无论如何不要输入你的`github密码`！
如果是UI很高级的那种，就可以选择账号密码登录或者令牌登录的话，你就选令牌然后输入令牌；
如果是UI很低级的那种，就一个框加一些描述性文字，那就按要求来，要用户名就输用户名，要密码password也输入`令牌，而不是密码`；
此后，你只需要在浏览器的地址栏输入MYNAME123.github.io就可以访问你的网页了！


# 参考链接：
关于nodejs的安装
https://blog.csdn.net/lxw1844912514/article/details/119727823

关于git的安装
https://www.cnblogs.com/xueweisuoyong/p/11914045.html

github账号的注册
https://www.bilibili.com/read/cv5107169/

如果出现安装错误
http://www.qianduanheidong.com/blog/article/316744/db118ba3f128fa3f4ea9/

关于在github中建立仓库并生成密钥，见下方链接的第三节（这个链接的全过程也是可以参考的）
https://blog.csdn.net/qq_46922488/article/details/119348718

关于安装对应的主题，hexo给出了许多官方主题，根据各自的指引操作
https://hexo.io/themes/

本人采用的主题是butterfly，从安装文档1开始顺次阅读修改就可以了
https://butterfly.js.org/

关于将域名和自己的hexo博客绑定
https://blog.csdn.net/weixin_44718865/article/details/114760047