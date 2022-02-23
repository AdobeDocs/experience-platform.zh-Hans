---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: 3a81a6f41b1e6acfe0e79dd56f01cf1bcd99417c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 2 月 23 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [源](#sources)

## 数据收集 {#data-collection}

Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 改进了数据流配置的UI工作流 | 更新了在数据收集UI中创建新数据流的工作流。 向数据流添加服务时，选项列表中将仅包含您有权访问的服务。 请参阅 [配置数据流](../../edge/fundamentals/datastreams.md) 以了解更多信息。 |
| 为数据收集准备数据 | 如果您使用的是Adobe Experience Platform Web SDK，您现在可以利用数据准备功能将数据映射到服务器端的Experience Data Model(XDM)。 请参阅 [为数据收集准备数据](../../edge/fundamentals/datastreams.md#data-prep) （详细信息）。 |
| 第一方设备ID | 现在，在使用Platform Web SDK收集客户数据时，您可以将自己的设备ID发送到Adobe Experience Platform Edge Network，这为最近对第三方Cookie生命周期的浏览器限制提供了解决方法。 请参阅 [第一方设备ID](../../edge/identity/first-party-device-ids.md) 以了解更多信息。 |

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Data Prep] 支持Adobe Analytics源连接器 | Adobe Analytics源连接器现在支持数据准备功能，允许您在创建数据流时将Analytics报表包数据映射到目标XDM架构。 请参阅 [创建Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以了解更多信息。 |

有关 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 的新权限 `view-identity-graph` | 您现在可以使用 `view-identity-graph` 控制组织中的用户是否能够查看身份图数据的权限。 将禁止没有此权限的用户访问UI中的身份图查看器，或者在访问 [!DNL Identity Service] 返回身份的API。 请参阅 [访问控制概述](../../access-control/home.md) 以了解有关权限的更多信息。 |

有关 [!DNL Identity Service]，请参阅 [Identity Service概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 测试版源迁移至GA | 以下来源已从测试版提升为正式发布： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
