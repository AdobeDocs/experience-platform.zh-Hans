---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: bf4271cec6126de3b5d9f98df280afdcc798589d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发布日期：2020年10月**

- [数据准备](#data-prep)
- [实时客户资料](#profile)
- [源](#sources)

## 数据准备 {#data-prep}

数据准备使数据工程师能够映射、转换数据并验证数据与体验数据模型(XDM)之间的关系。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| `is_set` 函数 | 函 `is_set` 数允许您检查源数据中是否存在属性。 `is_set` 可以与一起使 `is_empty` 用，检查属性的存在和属性中值的存在。 |
| `get_values` 函数 | 函 `get_values` 数允许您从输入图获取任何给定键的值。 |

有关详细信息，请阅读数 [据准备概述](../../data-prep/home.md)。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 用户档案预览API增加 | 用户档案预览API(`/previewsamplestatus`)现在包括在您的IMS组织中视图用户档案片段总数的细分，以及在身份命名空间中视图用户档案片段的分布。 |
| 合并模式视图更新 | 在Experience PlatformUI中，用户可以更轻松地找到有关所有模式和对合并模式有贡献的数据集的信息，以及表面关键属性，如标识和关系字段。 这些更新改进了对用户档案正确配置、身份正确拼接和数据成功摄取进行故障诊断和验证的能力。 |

有关更多信息( [!DNL Real-time Customer Profile]包括有关使用数据的教程和最 [!DNL Profile] 佳实践)，请阅 [读实时客户用户档案概述](../../profile/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 分层映射 | 在预览获取过程中，您可以分层的源文件，如JSON或Parke。 |
| SFTP的SSH身份验证支持 | 您可以使用RSA/DSA Open SSH [!DNL Platform] 密钥将您的SFTP帐户连接到。 有关更 [多信息](../../sources/connectors/cloud-storage/ftp-sftp.md) ，请参阅SFTP概述。 |
| UX改进 | 您可以在数据获取过 [!DNL Profile] 程中启用数据集。 有关详细 [信息，请参阅云存储](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 数据流工作流教程。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。