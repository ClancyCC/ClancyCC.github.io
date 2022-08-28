---
title: 个人介绍/更新日志
date: 2022-01-27 16:34:44
updated:
type: "about"
comments: false
description: 
keywords: 
top_img: #因为使用了一图流，不可以单独配置置顶图
mathjax:
katex:
aside: true
aplayer:
highlight_shrink:
---
# 📌欢迎前往留言板进行留言！
# 🎓关于ClancyCC
大家好！我是一个~~即将毕业的大四~~老油条，当然专业并不是CS的工科er。
时间过得真快，一晃已经~~临近~~毕业。从那个“航”大老远跑来了现在这个“航”，最后未来还要跑一个“航”。~~在最后一年的悠闲时光里，却意外地感觉自己并不需要放松、同时也并不能/不敢放松~~。2022给自己的一个目标，是建立并打理好这样的一个个人博客网站。现在已是vlog、plog的时代，内心却仿佛时光倒回20多年前，向往当时的“互联网人”们更擅长的blog。

全是有什么写什么，学了点什么读了点什么都贴上来，自娱自乐嘻嘻。特别渴望、特别欢迎你的留言！哪怕来留言板踩一脚也好呀555！！

关于某一次逃难，可以阅读[哈尔科夫——逃难回忆录](/2022/03/13/逃难回忆录/)。

联系方式：
QQ：867342167
Wechat：zqc867342167
Mail：zqc867342167@gmail.com
Mail: 867342167@qq.com

---
# 📑更新日志
## 2022/08/28
- Add the chat-btn by Tidio.

## 2022/06/21
- Here is the process of reviewing and editting articles.
1. Review the title, created time, updated time, cover image and other basical setting.
2. Check spelling, grammar and punctuation of content.
3. Express all the image files make sure them work normally.
- Add post-copyright mode.

## 2022/06/01
- Discovered that CDN set was moved to `/scripts/events/config.js` since theme version 4.1.0, so it's a method to avoid the fail to access to jsdelivr website by edit config.js.
- Use `hexo-butterfly-extjs` and its local js to initialise instead of online file.
- Regret to use hexo-sw-Racing!!!😭 It will take 3 months to completely disapper in my site(Located at js/sw_delete.js).

## 2022/05/27
- Use `KaTeX` to render math equations. 
- Here is the [official website](https://katex.org/docs/options.html).Learn KaTex gramma or quickly apply in this [link](https://blog.csdn.net/Leytton/article/details/103745169/) or this [link:recommend](https://fivecakes.com/p/5b1bd56d2392ec23b91bab2e).

## 2022/04/25
- Add the link page.

## 2022/03/26
- Transfer all the articles from Zhihu, which themed as Liquid Rocket Engine Design.

## 2022/03/24
- Try to updated the guest_info and placeholder of Valiine Comment System.
- Add the new post [Valine评论系统的设置](/2022/03/24/Valine评论系统的设置/).

## 2022/03/21
- Add the local search system by downloading the plugin [`hexo-generator-search`](https://github.com/wzpan/hexo-generator-search) and configuring based on the instruction.
    1. Install. Files located at <u>Blog\node_modules\hexo-generator-search</u>;
    ``` bash
    $ npm install hexo-generator-search --save
    ```
    2. Configure this plugin in your root `_config.butterfly.yml`. 
    ``` yaml
    local_search:
      enable: true
    
    search:
      path: search.xml
      field: post
      content: true
      template: ./search.xml
    ```

## 2022/03/17
- Add a new post & try to reform the images' format.

## 2022/03/15
- Add a new post.
- 对<u>Blog\themes\butterfly\source\posts</u>文件夹下的文件进行分类整合

## 2022/03/13
- Add a new post.

## 2022/02/09
- Add a new post.

## 2022/02/07
- 添加新文章《html遇到的问题》，会长期更新；
- 并没有偷很多懒，在自学html+css入门啦；

## 2022/01/29
- 学会使用命令来更改页面宽度，相应的文件调整位置位于Blog\themes\butterfly\source\css\ _page\common.styl；
- 采用新的教程来设置gitcalendar，链接地址为https://zfe.space/post/hexo-githubcalendar.html.
📌其中对于添加在根目录中_config.yml（非主题配置，而是博客的配置文件）最后的部分做了改动，也就是所谓的js加速文档，笔者放在了<u>js/githubcalendar.js</u>中，原来采用的js文档位于https://cdn.jsdelivr.net/gh/Zfour/hexo-github-calendar@1.21/hexo_githubcalendar.js

## 2022/01/28
- 学会使用命令来去除评论前的分割线；
```html
<style>hr{display:none}</style>
```
- 添加gitcalendar，教程的链接位于https://zfe.space/post/6948.html
相应的文件调整位置位于Blog\source\gitcalendar\js\gitcalendar.js；

## 2022/01/27
- 新增并完善“关于”页面和"留言板"页面；

## 2022/01/24
- 关于背景图采取了一图流的方式方法，教程链接为https://android99.me/2021/08/10/butterfly-top-image-modify/. 此时网站的背景由_config.butterfly.yml中的background属性决定（491行左右，随着更新会变动，因此贴上代码）
```html
# Website Background (設置網站背景)
# can set it to color or image (可設置圖片 或者 顔色)
# The formal of image: url(http://xxxxxx.com/xxx.jpg)
# background: "#49B1F5"
background: url(../img/黄山美景2.jpeg)
```
- 本主题的安装采用了Git(github)方式。
---
# 待解决问题
1. Valine评论系统的系统回复功能？
2. 背景图的适配效果
<style>
p {font-size: 16px;}
li {font-size: 16px;}
</style>