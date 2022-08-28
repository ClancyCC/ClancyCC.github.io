---
title: Valine评论系统的设置
date: 2022-03-24 19:53:00
# updated: 2022-03-23 22:50:00 #啥也不写反而会自动更新
tags:
categories: 技术与技巧
keywords: 
description:
top_img:
comments: true
cover: /img/valine.png #应用于首页的文章标题封面，空白时默认采用主题配置文件中89/92行的参数，可选false
toc: #目录，默认true
toc_number: #目录是否添加序号，配置文件中为false
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
下文介绍我引入Valine评论系统的全过程：
> 首先请保证你的butterfly主题的版本比较新，截止到22/03/24，官方已经更新到了4.1.0

## 安装Valine系统
1. 遵循[Valine](https://github.com/xCss/Valine)的指示，配置好[LeanCloud](https://leancloud.cn/)应用,点击`控制台`->`注册并登录账号`->`创建应用`->`随便取名字填入描述`->`设置`->`应用凭证`，就能看到需要的信息重点关注其中的appId,appKey和Request域名。

2. 修改主题配置文件`_config.butterfly.yml`.输入appId和appKey即可；
```yaml
valine:
  appId: # leancloud application app id
  appKey: # leancloud application app key
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  serverURLs: # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
  bg: # valine background
  visitor: false
  option:
```
> 此后，所有评论的数据都将存储在`LeanCloud`->`数据存储`->`结构化数据`->`Comment`里面
> 如果更改了posts的路径，需要修改对应数据的url参数，否则评论会消失

## 对用户添加标签“博主/好友/访客”
1. 打开valine.pug,按指示添加如下字段。
安装butterfly系统时如果是npm安装，则文件位置在node_modules/hexo-theme-butterfly/layout/includes/third-party/comments/valine.pug，如果是git安装，文件在theme/butterfly/layout/includes/third-party/comments/valine.pug.
将pug文件里面关于fuction initValine()函数的部分替换成下面的部分，或者你也可以直接用我的文件覆盖[valine.pug(尚未发布)]()
```js
    function initValine () {
        const valine = new Valine(Object.assign({
            el: '#vcomment',
            appId: '#{theme.valine.appId}',
            appKey: '#{theme.valine.appKey}',
            placeholder: '#{theme.valine.placeholder}',
            avatar: '#{theme.valine.avatar}',
            meta: '#{theme.valine.guest_info }'.split(','),
            pageSize: '#{theme.valine.pageSize}',
            lang: '#{theme.valine.lang}',
            recordIP: #{theme.valine.recordIP},
            serverURLs: '#{theme.valine.serverURLs}',
            emojiCDN: '#{theme.valine.emojiCDN}',
            emojiMaps: !{emojiMaps},
            enableQQ: #{theme.valine.enableQQ},
            path: window.location.pathname,
            requiredFields: [!{theme.valine.requiredFields ? JSON.stringify(theme.valine.requiredFields).split(',') : ''}],
            master: '#{theme.valine.master}'.split(','),
            friends: '#{theme.valine.friends}'.split(','),
            tagMeta: '#{theme.valine.tagMeta || "博主,小伙伴,访客"}'.split(','),
            metaPlaceholder: !{JSON.stringify(theme.valine.metaPlaceholder || {})},
            visitor: #{theme.valine.visitor}
        }, !{JSON.stringify(theme.valine.option)}))
    }
```
2. 修改主题配置文件`_config.butterfly.yml`，其中重点关注master，friends；
```yaml
# valine
# https://valine.js.org
valine:
  appId:  # leancloud application app id
  appKey:  # leancloud application app key
  pageSize: 10 # comment list page size
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  lang: zh-CN # i18n: zh-CN/zh-TW/en/ja
  placeholder:  # valine comment input placeholder (like: Please leave your footprints)
  guest_info: nick,mail,link # valine comment header info (nick/mail/link)
  recordIP: false # Record reviewer IP
  serverURLs: https://3cc9dq6t.lc-cn-n1-shared.com # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
  bg: # valine background
  emojiCDN:  # emoji CDN
  enableQQ: true # enable the Nickname box to automatically get QQ Nickname and QQ Avatar
  requiredFields: nick,mail # required fields (nick/mail)
  master: # md5加密后的博主邮箱，32位小写
    - d4e7????????????44a14e9a94  #可添加多个
  friends: # md5加密后的小伙伴邮箱，32位小写
    - 5c?????????????e268ad3819c #可添加多个
    - 7c?????????????e2????3919c
  tagMeta: '博主,小伙伴,访客' # 标签要显示的文字,默认'博主,小伙伴,访客'
  metaPlaceholder:
    nick: 昵称/QQ号(必填)
    mail: 邮箱(必填)
    link: 网址(https://)
```

3. 在`_config.butterfly.yml`的CDN配置项添加如下内容。将Valine.min.js替换成适配版本。
```yaml
CDN:
  # comments
  gitalk:
  gitalk_css:
  blueimp_md5:
  valine: https://cdn.jsdelivr.net/gh/tzy13755126023/BLOG_SOURCE/valine_f/valine.min.js
```

## 修改信息框placeholder/info
似乎有部分用户安装butterfly时，关于valine可修改的参数比较少，找不到修改框格内信息的参数。可以按照上一小节的步骤修改代码，此后调整placeholder/guest_info/Requiredfield等参数即可。

## Valine获取评论失败(错误401或直接不显示评论框格)
该错误一般由区域问题导致。找到[LeanCloud](https://leancloud.cn/)应用,点击`控制台`->`登录账号`->`设置`->`应用凭证`，找到其中的Request域名(多个则取第一个，链接开头为appId的前八位)，粘贴到主题配置文件`_config.butterfly.yml`的`serverURLs`中；

```yaml
# valine
# https://valine.js.org
valine:
  appId:  # leancloud application app id
  appKey:  # leancloud application app key
  pageSize: 10 # comment list page size
  avatar: monsterid # gravatar style https://valine.js.org/#/avatar
  lang: zh-CN # i18n: zh-CN/zh-TW/en/ja
  placeholder:  # valine comment input placeholder (like: Please leave your footprints)
  guest_info: nick,mail,link # valine comment header info (nick/mail/link)
  recordIP: false # Record reviewer IP
  serverURLs: https://xxxxxxxx.lc-cn-n1-shared.com或者https://xxxxxxxx.api.lncldglobal.com # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
```

## 无法评论(错误124)
>Code 124: MongoDB timeout. Typically this indicates the request is too expensive. :post /1.1/classes/Comment {} [400 POST https://3cc9dq6t.lc-cn-n1-shared.com/1.1/classes/Comment]

参考链接：
[唐先森，Hexo+Butterfly主题美化，章节4.14](https://tzy1997.com/articles/hexo541u/)
[HCLonely，Valine 添加验证码、博主标签及评论微信、QQ 通知](https://blog.hclonely.com/posts/409d3090/)