---
keywords: Experience Platform；主页；热门主题；Blob;Blob;Azure Blob;Azure Blob
solution: Experience Platform
title: Azure Blob Source连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Azure Blob连接到Adobe Experience Platform。
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Azure Blob连接器

Adobe Experience Platform为云提供商（如AWS、[!DNL Google Cloud Platform]和[!DNL Azure]）提供本机连接。 您可以将数据从这些系统导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、设置格式或上载。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤都会集成到源工作流中。 [!DNL Platform] 允许您批量导入 [!DNL Azure Blob] 数据。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

>[!IMPORTANT]
>
>[!DNL Azure Blob]源连接器当前不支持与平台的同一区域连接。 这意味着如果您的Azure实例使用与Platform相同的网络区域，则无法建立与Platform源的连接。 目前，仅支持跨区域连接。 有关更多信息，请联系您的Adobe客户经理。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点号(.)和两个点号字符(.)。

## 将[!DNL Azure Blob]连接到[!DNL Platform]

以下文档提供了有关如何使用API或用户界面将Azure Blob连接到Adobe Experience Platform的信息：

### 使用API

- [使用流服务API创建Azure Blob Base连接](../../tutorials/api/create/cloud-storage/blob.md)
- [使用流量服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Azure Blob源连接](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
