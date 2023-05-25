---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支持
description: 了解如何使用Adobe Experience Platform Web SDK支持IAB TCF 2.0同意首选项
keywords: 同意；setConsent；配置文件隐私字段组；体验事件隐私字段组；隐私字段组；IAB TCF 2.0；Real-Time CDP；
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持交互式广告局透明度和同意框架2.0版(IAB TCF 2.0)。 本指南展示了通过与Adobe Real-time Customer Data Platform、Audience Manager、Experience Events、Adobe Analytics和Experience Edge集成的Adobe Experience Platform Web SDK支持IAB TCF 2.0的要求。

此外，还提供以下指南以帮助学习如何将IAB TCF 2.0与标记和不与标记集成。

- [带有标记](./with-launch.md)
- [不带标记](./without-launch.md)

## 快速入门

要使用IAB TCF 2.0实施Web SDK，您需要对体验数据模型(XDM)和体验事件有一定的了解。 在开始之前，请查看以下文档：

- [Experience Data Model (XDM)系统概述](../../../xdm/home.md)：标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model (XDM)](由Adobe推动)致力于标准化客户体验数据并定义客户体验管理的模式。

## Experience Platform集成

要使用SDK将同意数据发送到Adobe Experience Platform，需要满足以下条件：

- 其架构基于的数据集 [!DNL XDM Individual Profile] 类并包含TCF 2.0同意字段，这些字段支持在 [!DNL Real-Time Customer Profile].
- 使用Platform设置的数据流以及上面提到的启用配置文件的数据集。

请参阅指南，网址为 [符合TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) 有关创建所需数据集和数据流的说明。

## Audience Manager集成

Adobe Audience Manager (AAM)包含对IAB TCF 2.0的支持，这让您能够评估、尊重客户隐私选择，并将其转发给下游合作伙伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通过Adobe Experience Platform Web SDK与Audience Manager集成，请确保已设置数据流以转发到Adobe Audience Manager。

## Experience Events与Adobe Analytics集成

Real-Time CDP和Audience Manager的受众会跟踪客户当前的同意偏好，而Experience Events可以保存客户在收集事件时处于活动状态的同意偏好。

要收集有关事件的同意信息，需要满足以下条件：

- 基于以下项的数据集 [!DNL XDM Experience Event] 类，使用 [!DNL Experience Event] 隐私架构字段组。
- 使用设置的数据流 [!DNL XDM Experience Event] 上面的数据集。

有关如何将XDM体验事件转换为Analytics点击的更多信息，请从阅读 [Analytics概述](../../data-collection/adobe-analytics/analytics-overview.md) 文档。

## Adobe Experience Platform Web SDK集成

以下部分介绍IAB TCF 2.0与Adobe Experience Platform Web SDK之间的主要集成点。

>[!NOTE]
>
>即使未设置Real-Time CDP或Audience Manager，您仍可以将IAB TCF 2.0与Web SDK集成。 同意首选项可用于控制体验事件的收集和设置身份Cookie。

### 默认同意

当尚未为客户保存同意首选项时，使用默认同意。 这意味着默认同意选项可以控制Adobe Experience Platform Web SDK的行为，并根据客户的地区进行更改。

例如，如果您的客户不在《通用数据保护条例》(GDPR)的管辖范围内，则默认同意可以设置为 `in`，但在GDPR的管辖区内，默认同意可以设置为 `pending`. 您的同意管理平台(CMP)可能会检测客户的区域并提供标记 `gdprApplies` 更改为IAB TCF 2.0。此标记可用于设置默认同意。

有关默认同意的更多信息，请参阅 [默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) 在SDK配置文档中。

### 更改时设置同意

Adobe Experience Platform Web SDK具有 `setConsent` 命令，可使用IAB TCF 2.0将客户的同意首选项传达给所有Adobe服务。如果您要与Real-Time CDP集成，这会更新您的客户资料。 如果您要与Audience Manager集成，这会更新您的客户信息。 调用此项还会设置一个包含“全部或无”同意首选项的Cookie，用于控制是否允许发送未来的体验事件。 其目的是每当同意更改时，都会调用此操作。 在将来的页面加载中，将读取Experience Edge同意Cookie以确定是否可以发送Experience事件，以及是否可以设置身份Cookie。

与Audience Manager的IAB TCF 2.0集成类似，Experience Edge在客户明确同意以下目的时提供同意：

- **目的1：** 在设备上存储和/或访问信息
- **目的十：** 开发和改进产品
- **特殊目的1：** 确保安全性、防止欺诈和调试。 （根据IAB TCF法规，这始终是同意的）
- **Adobe供应商权限：** 同意Adobe（供应商565）

欲知关于 `setConsent` 命令，请阅读以下文档： [支持同意](../../consent/supporting-consent.md).

### 向体验事件添加同意

Adobe Experience Platform Web SDK具有 `sendEvent` 收集体验事件的命令。 如果您要与Experience Events或Adobe Analytics集成，并且希望获得每个体验事件的同意首选项，则应将同意信息添加到每个 `sendEvent` 命令。

欲知关于 `sendEvent` 命令，请阅读以下文档： [跟踪事件](../../fundamentals/tracking-events.md).

## 后续步骤

现在您已基本了解IAB透明度和同意框架2.0，请参阅任一有关使用IAB TCF 2.0的指南 [带有标记](./with-launch.md) 或 [不带标记](./without-launch.md).
