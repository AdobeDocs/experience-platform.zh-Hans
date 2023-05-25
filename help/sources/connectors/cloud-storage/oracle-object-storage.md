---
keywords: Experience Platform；主页；热门主题；Oracle对象存储；oracle对象存储
solution: Experience Platform
title: oracle对象存储源连接器概述
description: 了解如何使用API或用户界面将Oracle对象存储连接到Adobe Experience Platform。
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# oracle对象存储连接器

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]，允许您将来自这些系统的数据引入Platform以用于下游服务和目标。

云存储源可以将您的数据导入Platform，而无需下载、格式化或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 Platform允许您从以下位置引入数据 [!DNL Oracle Object Storage] 通过批处理。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 文档，以了解更多信息。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表：

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，它将被自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点如下 `\uE000`虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，例如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)，以及两个点字符(...)。

## Connect [!DNL Oracle Object Storage] 目标平台

以下文档提供了有关如何使用API或用户界面将Oracle对象存储连接到Adobe Experience Platform的信息：

### 使用API

- [使用流服务API创建Oracle对象存储基本连接](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [使用流服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Oracle对象存储源连接](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
