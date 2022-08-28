---
title: 新手html遇到的问题【长期更新】
date: 2022-02-07 22:13:00
updated: 2022-02-07 22:13:00
tags:
categories:
keywords:
description:
top_img:
comments: true
cover: /img/html_unsplash.jpg #应用于首页的文章标题封面，空白时默认采用主题配置文件中89/92行的参数，可选false
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
## 学习资料
本人跟学的bilibili的加百利先生的视频：
https://www.bilibili.com/video/BV1kb411n7NJ?spm_id_from=333.1007.top_right_bar_window_default_collection.content.click
我已经学完了，将我自己编的文件发布在了github中：
https://github.com/ClancyCC/html-css-js


## Q1:关于目录的读取
./是当前目录
../是父级目录
/是根目录
根目录指逻辑驱动器的最上一级目录，它是相对子目录来说的。打开“我的电脑”，双击C盘就进入C盘的根目录，双击D盘就进入D盘的根目录。其它类推。根目录在文件系统建立时即已被创建，其目的就是存储子目录（也称为文件夹）或文件的目录项。
但有时调用我发现./和/的应用是不太一样的。有时候不一定哪个是对的。

## Q2:关于img前后伪元素伪类的特殊情况

网络解释：

- 相关链接1：https://www.cnblogs.com/goodbeypeterpan/p/9620114.html

- 相关链接2：https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element

- 相关链接3：https://blog.csdn.net/weixin_40594645/article/details/109086358?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-1-109086358.pc_agg_new_rank&utm_term=img+%E5%8F%AF%E4%BB%A5after%E5%90%97css&spm=1000.2123.3001.4430

个人发现：

```html
<style>
	*{
        margin: 0;
        padding: 0;
    }
    .box{
        background-repeat: no-repeat;
        width: 250px;
        height: 250px;
        overflow: hidden;
        margin: 5px;
        float: left;
        position: relative;
    }
    .box > *{
        position: absolute;
    }
    .box img{
                transform: translateX(0) translateY(0);
    }
    .box img::after{
        content: "hjhghjg";
        left: 0px;
        top: 0px;
        position: absolute;
        background: transparent;
        height: 250px; width: 250px;
    }
    .box:hover img::after{
        background: rgb(255, 255, 255,0.3);
    }
</style>

<div class="box">
    <img src="xxxx.png" alt="">
    <img src="" alt="">             <!--关键行-->
</div>

<!--对于上文中的内容在此做描述：div容器中显示一张图片，当鼠标滑动至div容器时，会出现以蹭白色的遮罩-->
<!--当时当没有关键行时，效果不显示-->、
<!--检查网页时发现，效果出现时，第一张img后的伪元素几乎不存在，第二张的才存在。似乎只要img链接了正确的图片，伪元素就不能正常工作-->
```

## Q3:需要理解伪元素中的content属性有什么特殊意义
暂未解决


## Q4:关于在VS code中注释代码语句
```
注释语句：ctrl+/或者ctrl+K+ctrl+C
取消注释：ctrl+/或者ctrl+K+ctrl+U
块注释,多行注释：选中代码+alt+shift+A
```
