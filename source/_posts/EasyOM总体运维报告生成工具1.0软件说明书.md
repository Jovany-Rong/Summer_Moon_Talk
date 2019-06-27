---
title: 【开源】EasyOM总体运维报告生成工具1.0软件说明书
categories: 运维产品
tags:
  - EasyOM
  - 发布说明
  - 运维
  - Python
  - 开源
copyright: true
abbrlink: 71eafcbb
date: 2019-06-27 18:01:09
---

本工具可供集群环境下生成总体运维报告，源代码公开。

<!-- More -->

## 软件介绍

本工具需配合EasyOM运维工具箱1.1及以上版本使用。使用EasyOM运维工具箱执行运维检查后，可以生成对应计算机的单机数据源文件（*.esp格式）。若需要一次出具多台计算机的运维报告，可以收集在这些计算机中运行后的单机数据源文件，使用本工具生成总体运维报告。

## 使用手册

### 运行软件

打开 **EasyOM_TSG.exe** 文件。

![1.png](https://i.loli.net/2019/06/27/5d14844d79aee97780.png)

### 查看教程

按任意键，软件提示查看教程。

![2.png](https://i.loli.net/2019/06/27/5d1485799906270889.png)

*翻译：*

1. 检查conf/tsg.conf文件中的配置；
2. 将所有ESP文件放入Input目录中；
3. 按任意键以生成总体运维报告，它将出现在Output目录中。

### 检查配置文件

在conf目录中，打开tsg.conf配置文件，配置如图所示。

![3.png](https://i.loli.net/2019/06/27/5d1485e500c0529177.png)

如您不慎遗失该配置文件，可手动新建tsg.conf文件放入conf目录中。

title参数用于配置最终运维报告的标题。

header参数用于配置最终运维报告的页眉。

footer参数用于配置最终运维报告的页脚。

### 放入ESP文件

在Input目录中，放入从各计算机中执行运维检查后的ESP文件（ESP文件产生在EasyOM运维工具箱的esp目录中）。

![4.png](https://i.loli.net/2019/06/27/5d14880a9992318652.png)

### 执行配置检查

按任意键以使用软件进行配置检查，检查通过则显示OK字样。

![5.png](https://i.loli.net/2019/06/27/5d14888297e4734264.png)

### 执行Input目录检查

按任意键以使用软件进行Input目录检查，检查通过则显示OK字样。

![6.png](https://i.loli.net/2019/06/27/5d1488f28eddc53897.png)

### 执行ESP文件检查和评价

按任意键以使用软件进行ESP文件检查。软件要求用户对每个ESP文件对应的计算机进行评价，用户需针对每个ESP文件输入1-4打分，1代表运行良好，2代表运行正常，3代表运行基本正常，4代表运行异常。

![7.png](https://i.loli.net/2019/06/27/5d1489af6e9ac80522.png)

依次对每个ESP进行评分，全部完成后软件显示总共有几个ESP文件。

![8.png](https://i.loli.net/2019/06/27/5d1489e1bdb1777676.png)

### 输入巡检人姓名

按任意键以进行总体运维报告生成，首先需要输入巡检人姓名。

![9.png](https://i.loli.net/2019/06/27/5d148ac48e59f56255.png)

### 执行报告生成

键入回车，进行总体运维报告生成，完成后系统提示Report generated。

![10.png](https://i.loli.net/2019/06/27/5d148b54bbc5593680.png)

系统自动调用浏览器打开总体运维报告。

![11.png](https://i.loli.net/2019/06/27/5d148bb8b8c0f58115.png)

报告文件在Output目录中。

![12.png](https://i.loli.net/2019/06/27/5d148c03276f150868.png)

## 下载链接

直接[***点击此处***](https://rongchenfei.com/downloads/Operation_Softwares.html)下载。

## 源代码

本工具开源，大家可自由研究和使用，禁止用作商业用途～

请大家前往[我的GitHub](https://github.com/Jovany-Rong/EasyOM_Total_Specification_Generator)克隆代码仓库获取源代码。

## 项目官网

EasyOM项目官网：[点此进入](https://rongchenfei.com/EasyOM/)