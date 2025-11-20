---
title: 交易台实时转化API扩展概述
description: 了解Adobe Experience Platform中用于事件转发的Trade Desk Real-time Conversions API扩展。
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: 8cf838b6f6794b52f80cb899945c066014e211c2
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# [!DNL The Trade Desk Real-Time Conversions API]扩展概述

通过使用[[!DNL The Trade Desk Real-Time Conversions API]事件转发](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)规则中的API功能，您可以使用[!DNL The Trade Desk][扩展将数据从Adobe Experience Platform Edge Network发送到](../../../ui/event-forwarding/overview.md)。

使用[!DNL The Trade Desk Real-Time Conversions API]扩展，您可以在[事件转发](../../../ui/event-forwarding/overview.md)规则中利用API的功能，将数据从Adobe Experience Platform Edge Network发送到[!DNL The Trade Desk]。

请阅读本文档，了解如何安装该扩展并在事件转发[规则](../../../ui/managing-resources/rules.md)中使用其功能。

>[!NOTE]
>
>此扩展和文档页面由[!DNL The Trade Desk]团队维护。 如有任何查询或更新请求，请直接联系他们。

## 先决条件 {#prerequisites}

您必须具有相关的Advertiser ID，您的[!DNL The Trade Desk]帐户中必须具有UPixel ID和Tracker ID，才能配置[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)。

>[!INFO]
>
>如果您是商人，则还需要获取您的商家ID。

## 安装和配置[!DNL The Trade Desk]实时转化API {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL The Trade Desk]**&#x200B;实时转化API信息卡，然后选择&#x200B;**[!UICONTROL Install]**。

![扩展目录显示[!DNL The Trade Desk]扩展卡突出显示安装。](../../../images/extensions/server/tradedesk/install-extension.png)

在下一个屏幕中，输入[!UICONTROL Advertiser ID]，也可以输入[!UICONTROL Merchant ID]。 您可以将ID直接粘贴到这些输入中，也可以改用数据元素。 这些将用作对[!DNL The Trade Desk]实时转化API进行事件调用时使用的默认值。 完成后，选择 **[!UICONTROL Save]**。

要了解如何创建数据元素并使其可用于标记属性中的扩展，请按照[创建数据元素](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/data-collection/tags/create-data-elements)教程操作。

![突出显示了[!DNL The Trade Desk]和[!UICONTROL Advertiser ID]字段的[!UICONTROL Merchant ID]扩展配置页面。](../../../images/extensions/server/tradedesk/configure-extension.png)

扩展已安装，您现在可以在事件转发规则中使用该扩展的功能。

## 配置事件转发规则 {#rule}

安装并配置扩展后，您可以开始创建事件转发规则，以确定将事件发送到[!DNL The Trade Desk]的方法和时间。

您应该考虑配置多个规则，以便通过[和](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)实时转化API发送所有已接受的[!DNL The Trade Desk]请求属性[!DNL The Trade Desk]。

>[!NOTE]
>
>事件应当实时发送，或者尽可能接近实时发送。

在事件转发属性中创建新事件转发[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL The Trade Desk]**。 接下来，为&#x200B;**[!UICONTROL Real Time Conversion]**&#x200B;选择&#x200B;**[!UICONTROL Action Type]**。

![事件转发属性规则视图，突出显示添加事件转发规则操作配置所需的字段。](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

选择后，会显示其他控件以进一步配置将发送到[!DNL The Trade Desk]的事件数据。 选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以保存规则。

配置选项分为三个主要部分，如下所述：

**[!UICONTROL Basic Request Properties]**

| 输入 | 描述 |
| --- | --- |
| 跟踪器ID | 事件跟踪器的平台ID。 |
| 上像素ID | 事件的通用像素ID。 |
| 反向链接URL | 发生事件的网站URL（如果有）。 |
| 活动名称 | 合作伙伴平台定义的事件类型。 |
| 值 | 小数字符串中的收入跟踪值（例如，“19.98”）。 |
| 货币 | ISO格式的货币代码。 |
| 客户端IP | 客户端IPv4或IPv6 IP地址。 |
| 广告ID | 事件的唯一广告ID。 |
| 广告ID类型 | 广告ID的类型，在AD ID属性中指定：TDID、IDFA、AAID、DAID、NAID、IDL、EUID或UID2。 |
| 印象 | 36个字符的字符串（包括破折号），用作事件所归因的展示的唯一ID。 |
| 订单ID | 事件的关联订单标识符。 |
| td1-td10 | 可用于提供其他转化元数据的十个按顺序编号的自定义动态属性。 |

{style="table-layout:auto"}

![显示输入到字段中的示例数据的[!DNL Basic Request Properties]部分。](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

有关[!DNL The Trade Desk]实时转化API接受的[请求属性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)的更多信息，请参阅[!DNL The Trade Desk]开发人员文档。

**[!UICONTROL Object Request Parameters]**

包含更多信息的JSON对象。 您可以选择使用一组经过缩减的键值输入或提供原始JSON。 此外，您还可以通过选择右侧的磁盘（![磁盘图标](/help/images/icons/database.png)）从数据元素检索动态数据。


![显示可用字段的[!DNL Object Request Parameters]部分。](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

有关[及其属性的更多信息，请参阅](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items)实时转化事件[!UICONTROL Object Request Parameters]文档。

**[!UICONTROL Configuration Overrides]**

>[!NOTE]
>
>[!UICONTROL Configuration Overrides]字段允许您在每个规则上设置不同的[!DNL Advertiser ID]和/或[!DNL Merchant ID]。

| 输入 | 描述 |
| --- | --- |
| 广告商 ID | 与此事件关联的广告商的唯一标识符。 可以提供其他广告商ID以覆盖您在扩展配置中提供的ID。 |
| 商家ID | [!DNL The Trade Desk]在整个登记过程中为每个商家提供的唯一标识符。 可以提供其他贸易商ID以覆盖您在扩展配置中提供的ID。 |

![显示可用字段的[!DNL Configuration Overrides]部分。](../../../images/extensions/server/tradedesk/configure-overrides.png)

如果对规则满意，请选择&#x200B;**[!UICONTROL Save to Library]**。 最后，发布新的事件转发[生成](../../../ui/publishing/builds.md)以启用对库所做的更改。

## 后续步骤

本指南介绍了如何使用[!DNL The Trade Desk]实时转化API扩展将服务器端事件数据发送到[!DNL The Trade Desk]。 在此处，建议通过创建不同的规则来扩展您的集成，这些规则会根据促销活动发送特定的转化事件。 有关[!DNL Adobe Experience Platform]中事件转发功能的详细信息，请阅读[事件转发概述](../../../ui/event-forwarding/overview.md)。

有关如何有效实施集成的更多指导，请参阅[!DNL The Trade Desk]有关[实时转化API [!DNL The Trade Desk] 的](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)最佳实践的文档。

有关如何使用Experience Platform Debugger和事件转发监视工具调试实施的详细信息，请阅读[Adobe Experience Platform Debugger概述](../../../../debugger/home.md)和[监视事件转发中的活动](../../../ui/event-forwarding/monitoring.md)。
