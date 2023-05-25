---
title: Adobe Experience Platform发行说明2022年11月
description: Adobe Experience Platform 2022年11月版发行说明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 11 月 23 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [体验数据模型(XDM)](#xdm)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL AWS] 事件转发的扩展 | 您现在可以将数据发送到 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md) 了解更多信息。 |
| [!DNL Google Ads Enhanced Conversions] 事件转发的扩展 | 您现在可以将转化数据发送至 [!DNL Google Ads] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 了解更多信息。 |
| [!DNL Microsoft Azure] 事件转发的扩展 | 您现在可以将数据发送到 [!DNL Microsoft Azure] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md) 了解更多信息。 |

有关Platform数据收集功能的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| 直接添加到架构时为自定义类分配字段 | 时间 [将单个字段直接添加到架构](../../xdm/ui/resources/schemas.md#add-individual-fields)之前，您只能将字段作为父资源分配给字段组。 现在，除了字段组外，您还可以 [将字段分配给自定义类](../../xdm/ui/resources/schemas.md#add-to-class) 作为其父资源。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- | 
| oracle服务云源的测试版可用性 | 使用Oracle服务云源从Oracle服务云帐户中摄取数据以进行Experience Platform。 有关详细信息，请阅读有关 [oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
