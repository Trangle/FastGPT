---
title: "Sealos 一键部署"
description: "使用 Sealos 一键部署 FastGPT"
icon: "cloud"
draft: false
toc: true
weight: 706
---

Sealos 的服务器在国外，不需要额外处理网络问题，无需服务器、无需魔法、无需域名，支持高并发 & 动态伸缩。点击以下按钮即可一键部署 👇

[![](https://fastly.jsdelivr.net/gh/labring-actions/templates@main/Deploy-on-Sealos.svg)](https://cloud.sealos.io/?openapp=system-fastdeploy%3FtemplateName%3Dfastgpt)

由于需要部署数据库，部署完后需要等待 2~4 分钟才能正常访问。默认用了最低配置，首次访问时会有些慢。

![](/imgs/sealos1.png)

点击 Sealos 提供的外网地址即可打开 FastGPT 的可视化界面。

![](/imgs/sealos2.png)

> 用户名：`root`
> 
> 密码就是刚刚一键部署时设置的环境变量

## 修改配置文件和环境变量

在 Sealos 中，你可以打开`应用管理`（App Launchpad）看到部署的 FastGPT，可以打开`数据库`（Database）看到对应的数据库。

在`应用管理`中，选中 FastGPT，点击变更，可以看到对应的环境变量和配置文件。

![](/imgs/fastgptonsealos1.png)

{{% alert icon="🤖 " context="success" %}}
在 Sealos 上，FastGPT 一共运行了 1 个服务和 2 个数据库，如暂停和删除请注意数据库一同操作。（你可以白天启动，晚上暂停它们，省钱大法）
{{% /alert %}}

## 更新

点击重启会自动拉取最新镜像更新，请确保镜像`tag`正确。

## 部署架构图

![](/imgs/sealos-fastgpt.webp)

## Sealos 使用

### 简介

FastGPT 商业版共包含了3个应用（fastgpt, fastgpt-plus, fastgpt-admin）和2个数据库，使用多 Api Key 时候需要安装 OneAPI（一个应用和一个数据库），总计4个应用和3个数据库。

![](/imgs/onSealos1.png)

点击右侧的详情，可以查看对应应用的详细信息。

### 如何更新/升级 FastGPT
[升级脚本文档](https://doc.fastgpt.in/docs/development/upgrading/)先看下文档，看下需要升级哪个版本。注意，不要跨版本升级！！！！！

例如，目前是4.5 版本，要升级到4.5.1，就先把镜像版本改成v4.5.1，执行一下升级脚本，等待完成后再继续升级。如果目标版本不需要执行初始化，则可以跳过。

升级步骤：

1. 查看[更新文档](/docs/development/upgrading/intro/)，确认要升级的版本，避免跨版本升级。
2. 打开 sealos 的应用管理
3. 有2个应用 fastgpt ， fastgpt-pro
4. 点击对应应用右边3个点，变更。或者点详情后右上角的变更。
5. 修改镜像的版本号

![](/imgs/onsealos2.png)

6. 点击变更/重启，会自动拉取最新镜像进行更新
7. 执行对应版本的初始化脚本(如果有)

### 如何获取 FastGPT 访问链接

打开对应的应用，点击外网访问地址。

![](/imgs/onsealos3.png)

### 配置自定义域名

点击对应应用的变更->点击自定义域名->填写域名-> 操作域名 Cname -> 确认 -> 确认变。

![](/imgs/onsealos4.png)

### 如何修改配置文件

打开 Sealos 的应用管理 -> 找到对应的应用 -> 变更 -> 往下拉到高级配置，里面有个配置文件 -> 新增或点击对应的配置文件可以进行编辑 -> 点击右上角确认变。

![](/imgs/onsealos5.png)

[配置文件参考](https://doc.fastgpt.in/docs/development/configuration/)

### 修改站点名称以及 favicon
修改应用的环境变量，增加

```
SYSTEM_NAME=FastGPT
SYSTEM_FAVICON=/favicon.ico
HOME_URL=/app/list
```

SYSTEM_FAVICON 可以是一个网络地址

![](/imgs/onsealos6.png)

### 挂载logo
目前暂时无法 把浏览器上的logo替换。仅支持svg，待后续可视化做了后可以全部替换。
新增一个挂载文件，文件名为：/app/projects/app/public/icon/logo.svg ，值为 svg 对应的值。

![](/imgs/onsealos7.png)

![](/imgs/onsealos8.png)

### 管理后台

![](/imgs/onsealos9.png)


### 商业版镜像配置文件

```
{
  "license": "",
  "system": {
    "title": "" // 系统名称
  }
}
```

### One API 使用

[参考 OneAPI 使用步骤](/docs/development/one-api/)