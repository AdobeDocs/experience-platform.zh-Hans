---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: aabf715475b3634ef134226f67b722f84e830556
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 11 月 23 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [体验数据模型(XDM)](#xdm)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL AWS] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md) 以了解更多信息。 |
| [!DNL Google Ads Enhanced Conversions] 事件转发扩展 | 您现在可以将转化数据发送到 [!DNL Google Ads] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 以了解更多信息。 |
| [!DNL Microsoft Azure] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Microsoft Azure] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md) 以了解更多信息。 |

有关Platform数据收集功能的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 直接添加到架构时，为自定义类分配字段 | When [直接将单个字段添加到架构](../../xdm/ui/resources/schemas.md#add-individual-fields)，以前只能将字段分配给字段组作为其父资源。 现在，除了字段组之外，您还可以 [将字段分配给自定义类](../../xdm/ui/resources/schemas.md#add-to-class) 作为其父资源。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- | 
| oracle服务云源的测试版可用性 | 使用Oracle服务云源将数据从您的Oracle服务云帐户中摄取到Experience Platform。 有关更多信息，请阅读 [Oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
