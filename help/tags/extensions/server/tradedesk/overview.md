---
title: 交易台实时转化API扩展概述
description: 了解Adobe Experience Platform中用于事件转发的Trade Desk Real-time Conversions API扩展。
hide: true
hidefromtoc: true
source-git-commit: d9d185685106ac160dcbefc5e9567a85c8302a73
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API] 扩展概述

您可以使用 [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) 将数据从Adobe Experience PlatformEdge Network发送到的扩展 [!DNL The Trade Desk] 通过在应用程序中使用API [事件转发](../../../ui/event-forwarding/overview.md) 规则。

使用 [!DNL The Trade Desk Real-Time Conversions API] 扩展上，您可以利用API在 [事件转发](../../../ui/event-forwarding/overview.md) 将数据发送到的规则 [!DNL The Trade Desk] 从Adobe Experience PlatformEdge Network访问。

请阅读本文档，了解如何安装扩展并在事件转发中使用其功能 [规则](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>此扩展和文档页面由维护 [!DNL The Trade Desk] 团队。 如有任何查询或更新请求，请直接联系他们。

## 先决条件 {#prerequisites}

您必须拥有相关的广告商ID，并且需要在中配备像素ID和跟踪器ID。 [!DNL The Trade Desk] 帐户，以配置 [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>如果您是商人，则还需要获取您的商家ID。

## 安装和配置 [!DNL The Trade Desk] 实时转化API {#install}

要安装扩展， [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或者选择现有的属性进行编辑。

选择 **[!UICONTROL 扩展]** 在左侧导航中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 交易台]** 实时转化API信息卡，然后选择 **[!UICONTROL 安装]**.

![扩展目录显示 [!DNL The Trade Desk] 扩展卡突出显示安装。](../../../images/extensions/server/tradedesk/install-extension.png)

在下一个屏幕中，输入 [!UICONTROL 广告商ID]和（可选） [!UICONTROL 商家ID]. 您可以将ID直接粘贴到这些输入中，也可以改用数据元素。 这些将用作对进行事件调用时使用的默认值 [!DNL The Trade Desk] 实时转化API。 选择 **[!UICONTROL 保存]** 完成后。

要了解如何创建数据元素并将它们提供给标记属性中的扩展，请按照 [创建数据元素](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) 教程。

![此 [!DNL The Trade Desk] 扩展配置页面，其中包含 [!UICONTROL 广告商ID] 和 [!UICONTROL 商家ID] 高亮显示的字段。](../../../images/extensions/server/tradedesk/configure-extension.png)

扩展已安装，您现在可以在事件转发规则中使用该扩展的功能。

## 配置事件转发规则 {#rule}

安装并配置扩展后，您可以开始创建事件转发规则，以确定将事件发送到的方法和时间 [!DNL The Trade Desk].

您应该考虑配置多个规则以发送所有已接受的规则 [请求属性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] 和 [!DNL The Trade Desk] 实时转化API。

>[!NOTE]
>
>事件应当实时发送，或者尽可能接近实时发送。

创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 在事件转发属性中。 下 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL 交易台]**. 接下来，选择 **[!UICONTROL 实时转换]** 对于 **[!UICONTROL 操作类型]**.

![Event Forwarding Property Rules视图，突出显示添加事件转发规则操作配置所需的字段。](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

选择后，会显示其他控件，以进一步配置将发送到的事件数据 [!DNL The Trade Desk]. 选择 **[!UICONTROL 保留更改]** 以保存规则。

配置选项分为三个主要部分，如下所述：

**[!UICONTROL 基本请求属性]**

| 输入 | 描述 |
| --- | --- |
| 跟踪器ID | 事件跟踪器的平台ID。 |
| 上像素ID | 事件的通用像素ID。 |
| 反向链接URL | 发生事件的网站URL（如果有）。 |
| 活动名称 | 合作伙伴平台定义的事件类型。 |
| 值 | 小数字符串中的收入跟踪值（例如，“19.98”）。 |
| 货币 | ISO格式的货币代码。 |
| 客户端IP | 客户端IPv4或IPv6 IP地址。 |
| 广告 ID | 事件的唯一广告ID。 |
| 广告 ID 类型 | 广告ID的类型，在AD ID属性中指定：TDID、IDFA、AAID、DAID、NAID、IDL、EUID或UID2。 |
| 印象 | 36个字符的字符串（包括破折号），用作事件所归因的展示的唯一ID。 |
| 订单ID | 事件的关联订单标识符。 |
| td1-td10 | 可用于提供其他转化元数据的十个按顺序编号的自定义动态属性。 |

{style="table-layout:auto"}

![此 [!DNL Basic Request Properties] 部分显示了输入到字段中的示例数据。](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

请参阅 [!DNL The Trade Desk] 开发人员文档，以了解有关 [请求属性](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) 接受者 [!DNL The Trade Desk] 实时转化API。

**[!UICONTROL 对象请求参数]**

包含更多信息的JSON对象。 您可以选择使用一组经过缩减的键值输入或提供原始JSON。 此外，您还可以通过选择磁盘(![磁盘图标](../../../images/extensions/server/tradedesk/disk-icon.png))在右侧。


![此 [!DNL Object Request Parameters] 部分显示可用的字段。](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

请参阅 [实时转化事件](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) 文档，以了解有关 [!UICONTROL 对象请求参数] 以及它们的属性。

**[!UICONTROL 配置覆盖]**

>[!NOTE]
>
>此 [!UICONTROL 配置覆盖] 利用字段，可设置其他 [!DNL Advertiser ID] 和/或 [!DNL Merchant ID] 每条规矩。

| 输入 | 描述 |
| --- | --- |
| 广告商 ID | 与此事件关联的广告商的唯一标识符。 可以提供其他广告商ID以覆盖您在扩展配置中提供的ID。 |
| 商家ID | 每个商家提供的唯一标识符 [!DNL The Trade Desk] 整个入职程序。 可以提供其他贸易商ID以覆盖您在扩展配置中提供的ID。 |

![此 [!DNL Configuration Overrides] 部分显示可用的字段。](../../../images/extensions/server/tradedesk/configure-overrides.png)

如果对规则满意，请选择 **[!UICONTROL 保存到库]**. 最后，发布新的事件转发 [生成](../../../ui/publishing/builds.md) 以启用对库所做的更改。

## 后续步骤

本指南介绍了如何将服务器端事件数据发送到 [!DNL The Trade Desk] 使用 [!DNL The Trade Desk] 实时转化API扩展。 在此处，建议通过创建不同的规则来扩展您的集成，这些规则会根据促销活动发送特定的转化事件。 有关中的事件转发功能的详细信息 [!DNL Adobe Experience Platform]，阅读 [事件转发概述](../../../ui/event-forwarding/overview.md).

请参阅 [!DNL The Trade Desk] 文档 [的最佳实践 [!DNL The Trade Desk] 实时转化API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 以获取有关如何有效实施集成的更多指导。

有关如何使用Debugger和Event Forwarding Monitoring工具调试Experience Platform的详细信息，请参阅 [Adobe Experience Platform Debugger概述](../../../../debugger/home.md) 和 [监测事件转发中的活动](../../../ui/event-forwarding/monitoring.md).
