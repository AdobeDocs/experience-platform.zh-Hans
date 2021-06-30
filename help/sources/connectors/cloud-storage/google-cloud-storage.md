---
keywords: Experience Platform；主页；热门主题；Google云存储；Google云存储
solution: Experience Platform
title: Google云存储源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Google云存储连接到Adobe Experience Platform。
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Google云存储连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接，允许您从这些系统中获取数据。

云存储源可以将您自己的数据引入平台，而无需下载、设置或上传。 摄取的数据可以采用符合体验数据模型(XDM)的JSON或Parquet格式，也可以采用分隔格式。 流程的每个步骤都会集成到源工作流中。 平台允许您从[!DNL Google Cloud Storage]批量导入数据。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

## 连接[!DNL Google Cloud Storage]帐户的先决条件设置

要连接到平台，您必须首先为[!DNL Google Cloud Storage]帐户启用互操作性。 要访问互操作性设置，请打开[!DNL Google Cloud Platform]，然后从导航面板的&#x200B;**[!UICONTROL 云存储]**&#x200B;选项中选择&#x200B;**[!UICONTROL 设置]**。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

此时将显示&#x200B;**[!UICONTROL Settings]**&#x200B;页面。 从此处，您可以看到有关[!DNL Google]项目ID的信息以及有关[!DNL Google Cloud Storage]帐户的详细信息。 要访问互操作性设置，请从顶部标题中选择&#x200B;**[!UICONTROL 互操作性]**。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 互操作性]**&#x200B;页面包含有关身份验证、访问密钥以及与您的服务帐户关联的默认项目的信息。 要为服务帐户生成新的访问密钥ID和密钥访问密钥，请选择&#x200B;**[!UICONTROL 为服务帐户创建密钥]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和密钥访问密钥将[!DNL Google Cloud Storage]帐户连接到平台。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义：`! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点号(.)和两个点号字符(.)。

## 将[!DNL Google Cloud Storage]连接到平台

以下文档提供了有关如何使用API或用户界面将[!DNL Google Cloud Storage]连接到平台的信息：

### 使用API

- [使用流量服务API创建Google云存储基础连接](../../tutorials/api/create/cloud-storage/google.md)
- [使用流量服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Google云存储源连接](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
