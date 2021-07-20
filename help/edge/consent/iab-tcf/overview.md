---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支持
description: 了解如何使用Adobe Experience Platform Web SDK支持IAB TCF 2.0同意首选项
keywords: 同意；设置同意；配置文件隐私字段组；体验事件隐私字段组；隐私字段组；IAB TCF 2.0；实时CDP；实时客户数据配置文件
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中支持IAB TCF 2.0

Adobe Experience Platform Web SDK支持交互式广告局透明度与同意框架版本2.0(IAB TCF 2.0)。 本指南显示了通过Adobe Experience Platform Web SDK支持IAB TCF 2.0与实时客户数据平台、Audience Manager、体验事件、Adobe Analytics和Experience Edge集成的要求。

此外，以下指南可帮助了解如何将IAB TCF 2.0与Adobe Experience Platform Launch集成（无论是否与Analytics集成）。

- [使用Adobe Experience Platform Launch](./with-launch.md)
- [没有Adobe Experience Platform Launch](./without-launch.md)

## 快速入门

要使用IAB TCF 2.0实施Web SDK，您需要对体验数据模型(XDM)和体验事件有一定的了解。 在开始之前，请查阅以下文档：

- [体验数据模型(XDM)系统概述](../../../xdm/home.md):标准化和互操作性是Adobe Experience Platform背后的关键概念。[!DNL Experience Data Model (XDM)]在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理模式。

## Experience Platform集成

要使用SDK将同意数据发送到Adobe Experience Platform，需要满足以下条件：

- 其架构基于[!DNL XDM Individual Profile]类且包含TCF 2.0同意字段的数据集，可在[!DNL Real-time Customer Profile]中使用。
- 使用Platform和上述启用了用户档案的数据集设置的数据流。

有关创建所需数据集和数据流的说明，请参阅[TCF 2.0合规性](../../../landing/governance-privacy-security/consent/iab/overview.md)指南。

## Audience Manager集成

Adobe Audience Manager(AAM)包含对IAB TCF 2.0的支持，通过该支持，您可以评估、尊重客户隐私选择，并将这些选择转发给下游合作伙伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通过Adobe Experience Platform Web SDK与Audience Manager集成，请确保已设置数据流以转发到Adobe Audience Manager。

## 体验事件和Adobe Analytics集成

虽然实时CDP和Audience Manager的受众可以跟踪客户的当前同意首选项，但体验事件可以保存客户的同意首选项，这些首选项在收集事件时处于活动状态。

要收集有关事件的同意信息，需要满足以下条件：

- 基于[!DNL XDM Experience Event]类且具有[!DNL Experience Event]隐私架构字段组的数据集。
- 使用上面的[!DNL XDM Experience Event]数据集设置的数据流。

有关如何将XDM体验事件转换为Analytics点击的更多信息，请首先阅读[Analytics概述](../../data-collection/adobe-analytics/analytics-overview.md)文档。

## Adobe Experience Platform Web SDK集成

以下部分介绍了IAB TCF 2.0与Adobe Experience Platform Web SDK之间的主要集成点。

>[!NOTE]
>
>即使没有设置实时CDP或Audience Manager，您仍可以将IAB TCF 2.0与Web SDK集成。 同意首选项可用于控制体验事件的收集和设置身份Cookie。

### 默认同意

如果尚未为客户保存同意首选项，则使用默认同意。 这意味着，默认同意选项可以控制Adobe Experience Platform Web SDK的行为，并根据客户所在的区域进行更改。

例如，如果您的客户不在《通用数据保护条例》(GDPR)的管辖范围内，则默认同意可以设置为`in`，但在GDPR的管辖范围内，默认同意可以设置为`pending`。 您的同意管理平台(CMP)可能会检测到客户的区域，并将标记`gdprApplies`提供到IAB TCF 2.0。可以使用此标记设置默认同意。

有关默认同意的更多信息，请参阅SDK配置文档中的[默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 在更改时设置同意

Adobe Experience Platform Web SDK具有`setConsent`命令，该命令使用IAB TCF 2.0将客户的同意首选项与所有Adobe服务进行通信。如果您要与实时CDP集成，则此命令将更新您客户的配置文件。 如果您要与Audience Manager集成，则会更新客户信息。 调用此调用还会设置一个包含“全部”或“无”同意首选项的Cookie，以控制是否允许发送未来体验事件。 我们打算在同意发生更改时调用此操作。 在将来加载页面时，将读取Experience Edge同意Cookie，以确定是否可以发送体验事件，以及是否可以设置身份Cookie。

与Audience Manager的IAB TCF 2.0集成类似，Experience Edge在客户明确同意以下目的时会给予客户同意：

- **用途1:** 在设备上存储和/或访问信息
- **用途10:** 开发和改进产品
- **特殊目的1:** 确保安全、防止欺诈和调试。（根据IAB TCF法规，始终同意）
- **Adobe供应商权限：** 同意Adobe（供应商565）

有关`setConsent`命令的更多信息，请阅读[支持同意](../../consent/supporting-consent.md)上的文档。

### 向体验事件添加同意

Adobe Experience Platform Web SDK具有用于收集Experience事件的`sendEvent`命令。 如果您要与体验事件或Adobe Analytics集成，并且希望在每个体验事件中都使用同意首选项，则应将同意信息添加到每个`sendEvent`命令中。

有关`sendEvent`命令的更多信息，请阅读有关[跟踪事件](../../fundamentals/tracking-events.md)的文档。

## 后续步骤

既然您对IAB透明度与同意框架2.0有了基本的了解，请参阅有关将IAB TCF 2.0 [与Adobe Experience Platform Launch](./with-launch.md)一起使用或将[与Adobe Experience Platform Launch](./without-launch.md)不使用的指南中的任一指南。
