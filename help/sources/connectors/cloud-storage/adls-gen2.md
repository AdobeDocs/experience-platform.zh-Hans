---
title: Azure Data Lake Storage Gen2 Source连接器概述
description: 了解如何使用API或用户界面将Azure Data Lake Storage Gen2连接到Adobe Experience Platform。
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接，允许您从这些系统引入数据。

云存储源可以将您自己的数据导入Experience Platform，而无需下载、设置格式或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 Experience Platform允许您通过批处理从[!DNL Azure Data Lake Storage Gen2] (ADLS Gen2)引入数据。

## IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

>[!IMPORTANT]
>
>[!DNL Azure Data Lake Storage Gen2]源不支持与Experience Platform的同区域连接。 如果您的[!DNL Azure]实例与Experience Platform使用相同的网络区域，则无法建立与Experience Platform源的连接。 目前，仅支持跨区域连接。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 将[!DNL Azure Data Lake Storage Gen2]连接到Experience Platform

>[!NOTE]
>
>用于创建[!DNL Azure Data Lake Storage Gen2]帐户的服务主体应至少具有从访问控制(IAM)分配的&#x200B;**存储Blob数据Reader**&#x200B;角色

以下文档提供了有关如何使用API或用户界面将[!DNL Azure Data Lake Storage Gen2]连接到Experience Platform的信息：

### 使用API

- [使用流服务API创建 [!DNL Azure Data Lake Storage Gen2] 基本连接](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [使用流量服务API浏览云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建 [!DNL Azure Data Lake Storage Gen2] 源连接](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
