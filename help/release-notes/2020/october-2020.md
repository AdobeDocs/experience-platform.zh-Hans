---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发布日期：2020年10月**

- [数据准备](#data-prep)
- [源](#sources)

## 数据准备 {#data-prep}

数据准备使数据工程师能够映射、转换数据并验证数据与体验数据模型(XDM)之间的关系。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| `is_set` 函数 | 函 `is_set` 数允许您检查源数据中是否存在属性。 `is_set` 可以与一起使 `is_empty` 用，检查属性的存在和属性中值的存在。 |
| `get_values` 函数 | 函 `get_values` 数允许您从输入图获取任何给定键的值。 |

有关详细信息，请阅读数 [据准备概述](../../data-prep/home.md)。

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