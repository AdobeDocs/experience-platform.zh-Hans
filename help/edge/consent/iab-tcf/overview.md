---
title: IAB透明度与同意框架2.0概述
seo-title: 支持Adobe Experience PlatformWeb SDK同意首选项（来自交互式广告局透明度与同意框架2.0）
description: 了解如何使用Experience PlatformWeb SDK支持IAB TCF 2.0同意首选项
seo-description: 了解如何使用Experience PlatformWeb SDK支持IAB TCF 2.0同意首选项
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---


# IAB透明度与同意框架2.0概述

Adobe Experience PlatformWeb SDK(AEP Web SDK)支持交互式广告局透明度和同意框架，版本2.0(IAB TCF 2.0)。 本指南显示了通过集成实时客户数据平台、Audience Manager、体验事件、Adobe Analytics和Experience Edge的AEP Web SDK支持IAB TCF 2.0的要求。

此外，还提供以下指南，帮助学习如何将IAB TCF 2.0与Adobe Experience Platform Launch集成，而不与之集成。

- [与Adobe Experience Platform Launch](./with-launch.md)
- [没有Adobe Experience Platform Launch](./without-launch.md)

## 入门指南

为了在IAB TCF 2.0中实施AEP Web SDK，您必须对体验数据模型(XDM)和体验事件有正确的了解。 在开始之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../../xdm/home.md):标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model (XDM)]由Adobe驱动，旨在实现客户体验数据标准化并定义模式以进行客户体验管理。

## 实时客户数据平台集成

以Adobe Experience Platform为构建基础的实时客户数据平台（实时CDP）可以帮助您整合来自多个企业来源的已知和匿名数据。 这使您能够创建可用于在所有渠道和设备上实时提供个性化客户体验的客户用户档案。 要通过AEP Web SDK将同意数据发送到实时CDP，需要满足以下条件：

- 基于类的数据集 [!DNL XDM Individual Profile] ，允许在中使用， [!DNL Real-time Customer Profile]具有用户档案隐私混合。
- 使用实时CDP设置的边缘配置以及上述用户档案数据集。

有关如何创建所需 [数据集，请参阅有关如何获取TCF 2.0同意](../../../rtcdp/privacy/iab/dataset-preparation.md) 的创建数据集的教程。

有关创建 [边缘配置的说明，请参阅](../../../rtcdp/privacy/privacy-overview.md) IAB TCF 2.0规范概述。

## Audience Manager集成

Adobe Audience Manager(AAM)包含对IAB TCF 2.0的支持，它使您能够评估、尊重客户隐私并将其转发给下游合作伙伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通过AEP Web SDK与Audience Manager集成，请确保您已设置好要转发给Adobe Audience Manager的边缘配置。

## 体验事件和Adobe Analytics集成

实时CDP和Audience Manager的受众可以跟踪客户当前的同意偏好，而体验事件可以保持客户的同意偏好，这些偏好在收集事件时是有效的。

要收集有关事件的同意信息，需要满足以下条件：

- 基于类的数据集 [!DNL XDM Experience Event] ，包含隐 [!DNL Experience Event] 私混合。
- 使用上述数据集设置的 [!DNL XDM Experience Event] 边缘配置。

有关如何将XDM体验事件转换为Analytics点击的更多信息，请阅读Analytics概述文 [档进行开始](../../data-collection/adobe-analytics/analytics-overview.md) 。

## AEP Web SDK集成

以下各节介绍IAB TCF 2.0与AEP Web SDK之间的主要集成点。

>[!NOTE]
>
>即使没有实时CDP或Audience Manager设置，您仍可以将IAB TCF 2.0与Web SDK集成。 同意首选项可用于控制体验事件的收集和设置身份cookie。

### 默认同意

如果尚未为客户保存同意首选项，则使用默认同意。 这意味着默认同意选项可以控制AEP Web SDK的行为并根据客户的区域进行更改。

例如，如果您的客户不属于一般数据保护规定(GDPR)的管辖范围，则默认同意可设置为，但在 `in`GDPR的管辖范围内，默认同意可设置为 `pending`。 您的云管理平台(CMP)可以检测客户的区域，并为 `gdprApplies` IAB TCF 2.0提供标志。此标志可用于设置默认同意。

有关默认同意的详细信息，请参 [阅SDK配置文档中](../../fundamentals/configuring-the-sdk.md#default-consent) “默认同意”部分。

### 更改时设置同意

AEP Web SDK有一个命 `setConsent` 令，该命令使用IAB TCF 2.0向所有Adobe服务传达客户的同意偏好。如果您要与实时CDP集成，这将更新客户的用户档案。 如果您要与Audience Manager集成，则此操作会更新客户信息。 调用此功能还会设置一个cookie，其中包含“全部”或“无”同意首选项，控制是否允许将来发送体验事件。 只要同意发生更改，就会调用此操作。 在将来的页面加载时，将读取Experience Edge同意Cookie，以确定是否可以发送体验事件，以及是否可以设置身份Cookie。

与Audience Manager的IAB TCF 2.0集成相似，当客户明确同意以下目的时，Experience Edge会予以同意：

- **用途1:** 在设备上存储和／或访问信息
- **目的十：** 开发和改进产品
- **特别目的1:** 确保安全、防止欺诈和调试。 （根据IAB TCF条例，始终同意）
- **Adobe供应商权限：** 同意Adobe（供应商565）

有关该命令的详 `setConsent` 细信息，请阅读有关支持同意 [的文档](../../consent/supporting-consent.md)。

### 向体验事件添加同意

AEP Web SDK有一个 `sendEvent` 用于收集体验事件的命令。 如果您要与体验事件或Adobe Analytics集成，并且希望每个体验事件都有同意偏好，则应将同意信息添加到每个 `sendEvent` 命令。

有关该命令的详 `sendEvent` 细信息，请阅读有关跟踪 [事件的文档](../../fundamentals/tracking-events.md)。

## 后续步骤

既然您对IAB透明度和同意框架2.0有了基本的了解，请参阅与Adobe Experience Platform Launch一起使用IAB TCF 2.0或不与一起使用IAB TCF 2.0 [的指南](./with-launch.md) ，或 [不与Adobe Experience Platform Launch合作](./without-launch.md)。
