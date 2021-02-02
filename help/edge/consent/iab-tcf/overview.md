---
title: IAB透明度与同意框架2.0概述
seo-title: 支持Adobe Experience PlatformWeb SDK同意首选项（来自交互式广告局透明度与同意框架2.0）
description: 了解如何使用Experience PlatformWeb SDK支持IAB TCF 2.0同意首选项
seo-description: 了解如何使用Experience PlatformWeb SDK支持IAB TCF 2.0同意首选项
keywords: 同意；设置同意；用户档案隐私混合；体验事件隐私混合；隐私混合；IAB TCF 2.0；实时CDP；实时客户用户档案
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# IAB透明度与同意框架2.0概述

Adobe Experience PlatformWeb SDK支持交互式广告局透明度和同意框架，版本2.0(IAB TCF 2.0)。 本指南说明了通过集成实时客户数据平台、Audience Manager、体验事件、Adobe Analytics和Experience Edge的Adobe Experience PlatformWeb SDK支持IAB TCF 2.0的要求。

此外，还提供以下指南，帮助学习如何将IAB TCF 2.0与Adobe Experience Platform Launch集成，而不与之集成。

- [与Adobe Experience Platform Launch](./with-launch.md)
- [没有Adobe Experience Platform Launch](./without-launch.md)

## 入门指南

要使用IAB TCF 2.0实施Web SDK，您必须对体验数据模型(XDM)和体验事件有正确的了解。 在开始之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../../xdm/home.md):标准化和互操作性是Adobe Experience Platform背后的关键概念。[!DNL Experience Data Model (XDM)]由Adobe驱动，旨在实现客户体验数据标准化并定义模式以进行客户体验管理。

## Experience Platform集成

要使用SDK向Adobe Experience Platform发送同意数据，需要满足以下条件：

- 模式基于[!DNL XDM Individual Profile]类并包含TCF 2.0同意字段的数据集，可在[!DNL Real-time Customer Profile]中使用。
- 使用平台和上述支持用户档案的数据集设置的边缘配置。

有关创建所需数据集和边缘配置的说明，请参阅[TCF 2.0 compliance](../../../landing/governance-privacy-security/consent/iab/overview.md)上的指南。

## Audience Manager集成

Adobe Audience Manager(AAM)包含对IAB TCF 2.0的支持，它使您能够评估、尊重客户隐私并将其转发给下游合作伙伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通过Adobe Experience PlatformWeb SDK与Audience Manager集成，请确保您已设置了要转发给Adobe Audience Manager的边缘配置。

## 体验事件和Adobe Analytics集成

实时CDP和Audience Manager的受众可以跟踪客户当前的同意偏好，而体验事件可以保持客户的同意偏好，这些偏好在收集事件时是有效的。

要收集有关事件的同意信息，需要满足以下条件：

- 基于[!DNL XDM Experience Event]类的数据集，带有[!DNL Experience Event]隐私混合。
- 使用上面的[!DNL XDM Experience Event]数据集设置的边缘配置。

有关如何将XDM体验事件转换为Analytics点击的详细信息，请阅读[Analytics概述](../../data-collection/adobe-analytics/analytics-overview.md)文档进行开始。

## Adobe Experience PlatformWeb SDK集成

以下各节介绍IAB TCF 2.0与Adobe Experience PlatformWeb SDK之间的主要集成点。

>[!NOTE]
>
>即使没有实时CDP或Audience Manager设置，您仍可以将IAB TCF 2.0与Web SDK集成。 同意首选项可用于控制体验事件的收集和设置身份cookie。

### 默认同意

如果尚未为客户保存同意首选项，则使用默认同意。 这意味着默认同意选项可以控制Adobe Experience PlatformWeb SDK的行为并根据客户的区域进行更改。

例如，如果您的客户不属于一般数据保护规定(GDPR)的管辖范围，则默认同意可设置为`in`，但在GDPR的管辖范围内，默认同意可设置为`pending`。 您的云管理平台(CMP)可以检测客户的区域，并将标志`gdprApplies`提供给IAB TCF 2.0。此标志可用于设置默认同意。

有关默认同意的详细信息，请参阅SDK配置文档中的[默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 更改时设置同意

Adobe Experience PlatformWeb SDK具有`setConsent`命令，该命令使用IAB TCF 2.0向所有Adobe服务传达客户的同意偏好。如果您正在与实时CDP集成，这将更新客户的用户档案。 如果您要与Audience Manager集成，则此操作会更新客户信息。 调用此功能还会设置一个cookie，其中包含“全部”或“无”同意首选项，控制是否允许将来发送体验事件。 只要同意发生更改，就会调用此操作。 在将来的页面加载时，将读取Experience Edge同意Cookie，以确定是否可以发送体验事件，以及是否可以设置身份Cookie。

与Audience Manager的IAB TCF 2.0集成相似，当客户明确同意以下目的时，Experience Edge会予以同意：

- **用途1:** 在设备上存储和／或访问信息
- **用途10：开** 发和改进产品
- **特殊目的1:** 确保安全、防止欺诈和调试。（根据IAB TCF条例，始终同意）
- **Adobe供应商权** 限：Adobe同意（供应商565）

有关`setConsent`命令的详细信息，请阅读[支持同意](../../consent/supporting-consent.md)上的文档。

### 向体验事件添加同意

Adobe Experience PlatformWeb SDK具有`sendEvent`命令，用于收集体验事件。 如果您要与体验事件或Adobe Analytics集成，并且希望每个体验事件都有同意偏好，则应将同意信息添加到每个`sendEvent`命令。

有关`sendEvent`命令的详细信息，请阅读有关[跟踪事件](../../fundamentals/tracking-events.md)的文档。

## 后续步骤

既然您对IAB透明度和同意框架2.0有基本的了解，请参阅将IAB TCF 2.0 [与Adobe Experience Platform Launch](./with-launch.md)或[与Adobe Experience Platform Launch](./without-launch.md)一起使用的指南。
