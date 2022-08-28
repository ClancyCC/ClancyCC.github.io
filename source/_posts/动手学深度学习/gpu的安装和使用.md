---
title: gpu的安装和使用
date: 2022-07-16 19:18:00
updated:
tags:
categories: 《动手学深度学习》
keywords:
description:
top_img:
comments: true
cover: img/DIVE INTO DEEP LEARNING.png #应用于首页的文章标题封面，空白时默认采用主题配置文件中89/92行的参数，可选false
toc:
toc_number: true #目录是否添加序号，配置文件中为false
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex: true
aplayer:
highlight_shrink:
aside: true
---
> 本文章基于李沐老师的《动手学深度学习》(pytorch版)，在此学习观礼膜拜。
> 课程主页：https://courses.d2l.ai/zh-v2
> 教材： https://zh-v2.d2l.ai/
> 课程论坛讨论：https://discuss.d2l.ai/c/16Pytorch
> 论坛： https://discuss.pytorch.org/

首先为大家贴上关于gpu使用的课程链接：https://www.bilibili.com/video/BV1z5411c7C1?spm_id_from=333.999.0.0
因为前面李沐的课程安装的时候，使用的是cpu版本的pytorch，所以即使你的电脑有独立GPU的时候，也并不能调用GPU进行计算。我自己看攻略摸索弄了蛮久的，在这里为大家贴上我的安装过程，也是基于李沐课程最快捷的方式。

# 查询你的GPU版本以及python相关包的版本
## 查询GPU型号和CUDA版本
[zilangch/CSDN：conda换源+查看cuda版本+anaconda一步安装torch和cuda](https://blog.csdn.net/zilangch/article/details/112499472)
为GPU安装合理的驱动，可以从[官网](https://www.nvidia.cn/Download/index.aspx?lang=cn)下载。这里也有[攻略：Win10+NVIDIA GeForce MX150: CUDA9+cuDnn+TensorFlow-GPU的安装教程](https://waitfof.blog.csdn.net/article/details/109140711?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-109140711-blog-123183926.pc_relevant_multi_platform_whitelistv1&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-109140711-blog-123183926.pc_relevant_multi_platform_whitelistv1&utm_relevant_index=1)
> 注意：这里的CUDA版本是随着驱动版本变化的，表示你后面要安装的CUDA不应该超过这里的版本号。

## python及第三方包的版本号
因为最终要在d2l-zh这个虚拟环境里完成安装，所以你要先激活虚拟环境，然后进行检查。
```Powershell
conda activate d2l-zh
conda list

# Name                    Version                   Build  Channel
python                    3.8.13               h6244533_0    defaults
torch                     1.11.0                   pypi_0    pypi
torchvision               0.12.0                   pypi_0    pypi
```
## 选定待下载的CUDA和cuddn的版本
你最终选定的版本应当符合以下几条要求：
1. 你可以在[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/win-64/)里找到一些合适的对应版本。
2. cuda版本确定时，cudnn的版本也会相应确定，可能有几个，影响不大。
   CUDA下载地址：https://developer.nvidia.com/cuda-toolkit-archive
   CUDNN下载地址：https://developer.nvidia.com/rdp/cudnn-archive
3. cuda的版本会对GPU驱动的版本号有要求，具体见[官网文档](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html)。

最后以我上面的版本号为例，来演示怎么找到适合自己的版本:
![清华1](清华1.jpg)![清华2](清华2.jpg)![cuda下载](cuda下载.jpg)![cudnn下载](cudnn下载.jpg)
综上，我选择的pytorch和torchvision版本即清华镜像站中的两个，cuda11.3，cudnn8.2.0

# 安装CUDA和对应的cudnn版本
> Nvidia的网站大陆访问可能有点慢，要耐心。当然如果你可以在国内镜像网站找到也可以对应处理。
> 下载cudnn的时候需要注册账号，填入信息。

你也还是可以继续参考这个链接：[Win10+NVIDIA GeForce MX150: CUDA9+cuDnn+TensorFlow-GPU的安装教程](https://waitfof.blog.csdn.net/article/details/109140711?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-109140711-blog-123183926.pc_relevant_multi_platform_whitelistv1&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-109140711-blog-123183926.pc_relevant_multi_platform_whitelistv1&utm_relevant_index=1)

# 安装GPU版本的pytorch和torchvision
> 这里应用了清华镜像。卡住的话可以回车试试。

```PowerShell
conda install https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/win-64/pytorch-1.11.0-py3.8_cuda11.3_cudnn8_0.tar.bz2
conda install https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/win-64/torchvision-0.12.0-py38_cu113.tar.bz2
```

# 检验安装效果
```python
import torch
print(torch.cuda.is_available())
print(torch.cuda.device_count())

Out:
True
1
```

<style>
    p img{
        width: 80%;
        border: solid black 1px;
    }
    li img{
        width: 90%;
        border: solid black 1px;
    }
    table thead tr th:nth-of-type(1){
        width: 15%;
    }
</style>