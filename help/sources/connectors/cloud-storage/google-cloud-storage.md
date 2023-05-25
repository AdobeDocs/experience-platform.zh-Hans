---
keywords: Experience Platform；主页；热门主题；Google Cloud Storage；google cloud storage
solution: Experience Platform
title: Google Cloud Storage源连接器概述
description: 了解如何使用API或用户界面将Google Cloud Storage连接到Adobe Experience Platform。
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Google云存储连接器

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]、和 [!DNL Azure]，允许您从这些系统获取数据。

云存储源可以将您自己的数据引入Platform，而无需下载、格式化或上传。 引入的数据可以设置为与Experience Data Model (XDM)兼容的JSON或Parquet格式，也可以采用分隔格式。 该过程的每个步骤都集成到源工作流中。 Platform允许您从以下位置引入数据 [!DNL Google Cloud Storage] 通过批处理。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 用于连接您的计算机的先决条件设置 [!DNL Google Cloud Storage] 帐户

要连接到Platform，您必须首先为您的 [!DNL Google Cloud Storage] 帐户。 要访问互操作性设置，请打开 [!DNL Google Cloud Platform] 并选择 **[!UICONTROL 设置]** 从 **[!UICONTROL 云存储]** 选项。

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

此 **[!UICONTROL 设置]** 页面。 从这里，您可以看到与您的 [!DNL Google] 项目ID以及有关您的项目的详细信息 [!DNL Google Cloud Storage] 帐户。 要访问互操作性设置，请选择 **[!UICONTROL 互操作性]** 从顶部标题中。

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

此 **[!UICONTROL 互操作性]** 页面包含有关身份验证、访问密钥以及与服务帐户关联的默认项目的信息。 要为您的服务帐户生成新的访问密钥ID和秘密访问密钥，请选择 **[!UICONTROL 为服务帐户创建密钥]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

您可以使用新生成的访问密钥ID和秘密访问密钥来连接 [!DNL Google Cloud Storage] Platform帐户。

欲知更多信息，请阅读 [创建和管理服务帐户密钥](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) 从 [!DNL Google Cloud] 文档。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，它将被自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点如下 `\uE000`虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)，以及两个点字符(...)。

## Connect [!DNL Google Cloud Storage] 目标平台

以下文档提供了有关如何连接的信息 [!DNL Google Cloud Storage] 至使用API或用户界面的Platform：

### 使用API

- [使用流服务API创建Google Cloud Storage基本连接](../../tutorials/api/create/cloud-storage/google.md)
- [使用流服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Google Cloud Storage源连接](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
