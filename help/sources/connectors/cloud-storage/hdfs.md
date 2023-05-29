---
keywords: Experience Platform；主页；热门主题；HDFS；HDFS；Apache HDFS；Apache HDFS
solution: Experience Platform
title: Apache HDFS源连接器概述
description: 了解如何使用API或用户界面将Apache HDFS连接到Adobe Experience Platform。
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Apache] HDFS连接器

>[!NOTE]
>
>Apache HDFS连接器处于测试阶段。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]、和 [!DNL Azure]，允许您从这些系统获取数据。 引入的数据可以格式化为JSON、Parquet或分隔。 对云存储提供商的支持包括 [!DNL Apache] HDFS。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，它将被自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点如下 `\uE000`虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)，以及两个点字符(...)。

## Connect [!DNL Apache] HDFS到 [!DNL Platform]

以下文档提供了有关如何连接的信息 [!DNL Apache] HDFS到 [!DNL Platform] 使用API或用户界面：

### 使用API

- [使用流服务API创建HDFS基本连接](../../tutorials/api/create/cloud-storage/hdfs.md)
- [使用流服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在用户界面中创建Apache HDFS源连接](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
