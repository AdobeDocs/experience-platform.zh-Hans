---
title: Merkury Enterprise Identity Resolution Source概述
description: 了解如何使用用户界面将Merkury Enterprise Identity Resolution连接到Adobe Experience Platform。
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform支持从数据合作伙伴应用程序中摄取数据。 数据合作伙伴的支持包括[!DNL Merkury Enterprise Identity Resolution]。

您可以通过[!DNL Merkury]使用[!DNL Merkle]识别更多数字访客（即使不使用Cookie），并提供客户所需的相关个性化体验。

您可以将&#x200B;**个人ID**&#x200B;用作[!DNL Merkury]源的一部分，以将您的组织所了解的有关个人的所有信息合并到单个综合配置文件中。 这些详细信息可能包括：

- 数字行为
- 购买偏好设置
- 标识信息，如名称、电子邮件地址、物理地址或设备ID。

您可以将摄取的数据格式设置为Experience Data Model (XDM) JSON、XDM Parquet或分隔。 该过程的每一步都集成到源工作中

![Merkury源的数据处理工作流程图示。](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP地址允许列表

在使用源连接器之前，必须将您所在地区所需的IP地址添加到允许列表。 如果不添加这些IP地址，源连接器可能无法正确工作或可能产生错误。 列入允许列表有关详细说明和允许的IP地址列表，请阅读[IP地址](../../ip-address-allow-list.md)页。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 先决条件

在开始使用[!DNL Merkury]源之前，您必须满足以下先决条件：

- 您必须与您的[!DNL Merkury]团队一起完成[!DNL Merkury]设置。
- 您必须从[!DNL Merkury]团队中检索凭据（访问密钥、密钥和存储段名称）。 

>[!NOTE]
>
>文件路径（如`myBucket/folder/subfolder/subsubfolder/abc.csv`）可能导致您仅访问`subsubfolder/abc.csv`。 如果要访问子文件夹，可以将存储段参数指定为myBucket，将folderPath指定为folder/subfolder，以确保文件探索从子文件夹开始，而不是从`subsubfolder/abc.csv`开始。

## 后续步骤

通过阅读本文档，您已完成将[!DNL Merkury]帐户中的数据导入Experience Platform所需的先决条件设置。 现在，您可以使用用户界面[在 [!DNL Merkury] 连接](../../tutorials/ui/create/data-partners/merkury.md)到Experience Platform时继续阅读指南。
