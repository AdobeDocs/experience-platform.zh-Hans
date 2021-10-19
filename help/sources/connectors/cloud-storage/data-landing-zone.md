---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据登陆区源
topic-legacy: overview
description: 了解如何将数据登陆区连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，允许您访问基于云的安全文件存储工具，以将文件导入平台。 您有权访问 [!DNL Data Landing Zone] 容器，且所有容器中的数据总量仅限于随Platform产品和服务许可证提供的总数据量。 平台及其应用程序服务(例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]和 [!DNL Real-time Customer Data Platform] 已配置一个 [!DNL Data Landing Zone] 每个沙盒的容器。 您可以通过 [!DNL Azure Storage Explorer] 或命令行界面。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据受标准保护 [!DNL Azure Blob] 储存安全机制在存放和运输中。 基于SAS的身份验证使您能够安全地访问 [!DNL Data Landing Zone] 容器。 您无需进行网络更改即可访问 [!DNL Data Landing Zone] 容器，这意味着您无需为网络配置任何允许列表或跨区域设置。 平台对上传到 [!DNL Data Landing Zone] 容器。 七天后会删除所有文件。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点，如 `\uE000`，但在NTFS文件名中有效，是无效的Unicode字符。 此外，某些ASCII或Unicode字符，如控制字符(例如 `0x00` to `0x1F`, `\u0081`等)，也不允许使用。 有关HTTP/1.1中控制Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点号(.)和两个点号字符(..)。

## 连接 [!DNL Data Landing Zone] to [!DNL Platform]

以下文档提供了有关如何从 [!DNL Data Landing Zone] 容器到Adobe Experience Platform。

### 使用API

- [创建 [!DNL Data Landing Zone] 源连接（使用流量服务API）](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [连接 [!DNL Data Landing Zone] 到使用UI的平台](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
