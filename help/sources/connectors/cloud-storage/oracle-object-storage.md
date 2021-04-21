---
keywords: Experience Platform；主页；热门主题；Oracle对象存储;oracle对象存储
solution: Experience Platform
title: Oracle对象存储源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Oracle对象存储连接到Adobe Experience Platform。
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Oracle对象存储连接器

Adobe Experience Platform为AWS等云提供商提供本机连接，允许您将这些系统中的数据导入平台，以用于下游服务和目标。[!DNL Google Cloud Platform]

云存储源无需下载、格式化或上传，即可将您的数据导入平台。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 平台允许您从[!DNL Oracle Object Storage]到批量导入数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)文档。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的约束列表:

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动删除它。
- 以下保留的URL字符必须正确转义：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COMPRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 将[!DNL Oracle Object Storage]连接到平台

以下文档提供了有关如何使用API或用户界面将Oracle对象存储连接到Adobe Experience Platform的信息：

### 使用API

- [使用Flow Service API创建Oracle对象存储源连接](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Oracle对象存储源连接](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
