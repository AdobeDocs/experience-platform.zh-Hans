---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据登陆区源
topic-legacy: overview
description: 了解如何将数据登陆区连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是Adobe Experience Platform [!DNL Azure Blob] 配置的一个存储界面，它允许您访问安全的基于云的文件存储设施，以通过源和目标在平台内外摄取和输出文件。您可以在每个沙盒上访问一个[!DNL Data Landing Zone]容器，并且所有容器中的总数据量仅限于随Platform Produces and Services许可证提供的总数据量。 Platform及其应用程序服务（如[!DNL Customer Journey Analytics]、[!DNL Journey Orchestration]、[!DNL Intelligent Services]和[!DNL Real-time Customer Data Platform]）的所有客户都为每个沙盒配置一个[!DNL Data Landing Zone]容器。 您可以通过[!DNL Azure Storage Explorer]或命令行界面将文件读取和写入容器。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据在存放和传输 [!DNL Azure Blob] 时均使用标准存储安全机制进行保护。基于SAS的身份验证允许您通过公共Internet连接安全地访问[!DNL Data Landing Zone]容器。 访问[!DNL Data Landing Zone]容器不需要任何网络更改，这意味着您无需为网络配置任何允许列表或跨区域设置。 平台对上载到[!DNL Data Landing Zone]容器的所有文件强制实施严格的7天生存时间(TTL)。 七天后会删除所有文件。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（如`0x00`到`0x1F`、`\u0081`等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点号(.)和两个点号字符(..)。

## 将[!DNL Data Landing Zone]连接到[!DNL Platform]

以下文档提供了有关如何使用API或用户界面将数据从[!DNL Data Landing Zone]容器引入Adobe Experience Platform的信息。

### 使用API

- [使用流服务API创建 [!DNL Data Landing Zone] 源连接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [使用UI连接 [!DNL Data Landing Zone] 到平台](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
