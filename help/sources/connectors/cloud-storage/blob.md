---
keywords: Experience Platform；主页；热门主题；Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob源连接器概述
topic: overview
description: 了解如何使用API或用户界面将Azure Blob连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Azure Blob连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将这些系统中的数据导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从批中导入 [!DNL Azure Blob] 数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

>[!IMPORTANT]
>
>[!DNL Azure Blob]源连接器当前不支持与平台的同一区域连接。 这意味着，如果您的Azure实例使用与平台相同的网络区域，则无法建立到平台源的连接。 目前，仅支持跨区域连接。 有关详细信息，请与您的Adobe客户经理联系。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动删除它。
- 以下保留的URL字符必须正确转义：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COMPRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 将[!DNL Azure Blob]连接到[!DNL Platform]

以下文档提供了如何使用API或用户界面将Azure Blob连接到Adobe Experience Platform的信息：

### 使用API

- [使用流服务API创建Azure Blob源连接](../../tutorials/api/create/cloud-storage/blob.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Azure Blob源连接](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)