---
title: Merkury Enterprise身份解析源概述
description: 了解如何使用用户界面将Merkury Enterprise Identity Resolution连接到Adobe Experience Platform。
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta 版
source-git-commit: 2f277e835333343ea22e52e05aa84a63f1d3d8ec
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>此 [!DNL Merkury Enterprise Identity Resolution] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

Adobe Experience Platform支持从数据合作伙伴应用程序中摄取数据。 对数据合作伙伴的支持包括 [!DNL Merkury Enterprise Identity Resolution].

您可以使用 [!DNL Merkury] 按 [!DNL Merkle] 识别更多数字访客（即使未使用Cookie），并根据客户要求提供相关的个性化体验。

您可以利用 **人员ID** 作为 [!DNL Merkury] “源”可将贵组织所了解的有关个人的所有信息整合到一个全面的配置文件中。 这些详细信息可能包括：

- 数字行为
- 购买偏好设置
- 标识信息，如姓名、电子邮件地址、物理地址或设备ID。

您可以将摄取的数据格式设置为Experience Data Model (XDM) JSON、XDM Parquet或分隔。 该过程的每一步都集成到源工作中

![Merkury源的数据处理工作流插图。](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，它将自动删除。
- 必须对以下保留的URL字符进行正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点如下 `\uE000`虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 先决条件

在开始使用之前，您必须满足以下先决条件 [!DNL Merkury] 来源：

- 您必须完成 [!DNL Merkury] 使用进行设置 [!DNL Merkury] 团队。
- 您必须从以下位置检索您的凭据（访问密钥、密钥和存储段名称）： [!DNL Merkury] 团队。 

>[!NOTE]
>
>文件路径，如 `myBucket/folder/subfolder/subsubfolder/abc.csv` 可能导致您仅访问 `subsubfolder/abc.csv`. 如果要访问子文件夹，可以将存储段参数指定为myBucket，将folderPath指定为folder/subfolder，以确保文件探索从子文件夹开始，而不是 `subsubfolder/abc.csv`.

## 后续步骤

通过阅读本文档，您已完成从获取数据所需的先决条件设置 [!DNL Merkury] 帐户到Experience Platform。 您现在可以继续阅读以下指南： [连接 [!DNL Merkury] 使用用户界面Experience Platform](../../tutorials/ui/create/data-partners/merkury.md).
