---
title: Coding Pages绑定阿里云域名无法使用二级域名访问解决方案
categories: 网络技术
tags:
  - Hexo
  - Coding
  - 腾讯云开发者平台
  - 域名
  - 问题解决
copyright: true
abbrlink: 575e
date: 2019-05-18 23:14:42
---

## 问题描述

在腾讯云开发者平台（原Coding.net平台）部署Pages静态网页，在设置中绑定了阿里云顶级域名*ABC.com*。在阿里云域名控制台中，*ABC.com*域名有两条解析记录，分别通过主机记录的 **@**和**www**解析到Pages应用访问地址（*Username*.coding.me）。

解析完成后，通过顶级域名*ABC.com*能够正常访问到我们的Pages应用，但通过二级域名www.*ABC.com*访问时报404错误。

<!-- more -->

## 原因分析

与GitHub平台不同，腾讯云开发者平台Pages应用支持绑定多个域名，但不支持自动绑定顶级域名下的二级域名，需要手动增加二级域名的绑定才能生效。

## 解决方法

在Pages设置中增加二级域名www.*ABC.com*的绑定。稍待片刻，即可正常访问应用。