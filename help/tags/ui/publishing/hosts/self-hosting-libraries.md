---
title: 自托管库
description: 了解如何在Adobe Experience Platform中为标记库内部版本实施自托管。
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 72%

---

# 自托管库

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

Adobe Experience Platform中的标记允许生成一组名为[内部版本](../builds.md)的文件。 这组文件控制应用程序在运行时的行为。

内部版本需要托管在某个位置，这样客户端设备才能在运行时根据需要对其进行检索。

这些文件的托管既可以由Experience Platform为您进行管理，也可以由您自行管理。

## 由 Adobe 管理 {#managed-by-adobe}

Adobe不从事Web托管业务。 如果您选择由 Adobe 管理您的托管文件，则您构建的库将交付到已与我们签约的第三方内容交付网络(CDN)。

目前，Akamai 是一个主要的 CDN 提供商。在 Akamai 托管的文件会使用域 `assets.adobedtm.com`。

### 为何使用受管的托管？

使用受管的托管主要是为了寻求便利。这样可以更轻松地创建所需的主机，而且无需担忧维护问题。

## 自托管

如果不希望由 Adobe 管理您的托管文件，则必须自行托管。要托管文件，您需要从Experience Platform中获取已完成的内部版本，并负责通过贵公司的发行周期将文件放到公司管理的服务器上。

### 为何使用自托管？

选择自行托管内部版本文件的原因有很多。

* 一些浏览器会根据最终用户配置的隐私设置阻止 assets.adobedtm.com 域
* 自托管可减少所需的 DNS 查找次数
* 出于安全原因，您需要设置特定的标头
* 您的缓存控制要求与Adobe默认设置不同
* 您希望更好地控制边缘节点的位置
* 贵组织制定了安全和法律要求，禁止您使用“由 Adobe 管理”选项

### 如何自托管

可以使用两种方法获取已完成的内部版本，以便进行自托管。

* 下载
* 直接交付

#### 下载

内部版本可以作为打包的.zip文件交付（可以选择是否加密）。 然后，可以解压缩该包，并将其中的内容插入到您的发行周期，以将其放置到自己的服务器上。

使用 [Managed by Adobe](self-hosting-libraries.md) 主机，然后在您的环境中选择 [Archive](../environments.md) 选项。此时环境会提供一个下载链接。每当创建内部版本时，您都可以从环境的下载链接中检索该内部版本。

#### 直接交付

内部版本也可以直接交付到您创建的SFTP服务器。 您负责将这些文件插入到发行周期，并实时推送这些文件。

要执行直接交付，应创建一个 [SFTP 主机](sftp-host.md)，并将该主机分配给您的环境。每当在该环境中生成库时，系统都会将文件交付到您的 SFTP 服务器。
