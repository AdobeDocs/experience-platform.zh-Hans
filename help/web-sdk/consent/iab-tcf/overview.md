---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支持
description: 了解如何使用Adobe Experience Platform Web SDK支持IAB TCF 2.0同意首选项
keywords: 同意；setConsent；配置文件隐私字段组；体验事件隐私字段组；隐私字段组；IAB TCF 2.0；Real-Time CDP；
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持交互式Advertising Bureau透明度和同意框架版本2.0 (IAB TCF 2.0)。 本指南演示了通过将Adobe Experience Platform Web SDK与Adobe Real-Time Customer Data Platform、Audience Manager、Experience Events、Adobe Analytics和Edge Network集成来支持IAB TCF 2.0的要求。

此外，还提供以下指南以帮助学习如何将IAB TCF 2.0与标记和不与标记集成。

- [带有标记](./with-tags.md)
- [不带标记](./without-tags.md)

## 快速入门

要使用IAB TCF 2.0实施Web SDK，您需要对Experience Data Model (XDM)和Experience Events有一定的了解。 在开始之前，请查看以下文档：

- [体验数据模型(XDM)系统概述](../../../xdm/home.md)：标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model (XDM)]由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

## Experience Platform集成

要使用SDK将同意数据发送到Adobe Experience Platform，需要满足以下条件：

- 其架构基于[!DNL XDM Individual Profile]类并包含已在[!DNL Real-Time Customer Profile]中启用的TCF 2.0同意字段的数据集。
- 使用Experience Platform设置的数据流以及上面提到的启用配置文件的数据集。

有关创建所需数据集和数据流的说明，请参阅[TCF 2.0合规性](../../../landing/governance-privacy-security/consent/iab/overview.md)指南。

## Audience Manager集成

Adobe Audience Manager (AAM)包含对IAB TCF 2.0的支持，该功能可让您评估、尊重客户隐私选择，并将其转发给下游合作伙伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通过Adobe Experience Platform Web SDK与Audience Manager集成，请确保已设置数据流以转发到Adobe Audience Manager。

## Experience Events与Adobe Analytics集成

Real-Time CDP和Audience Manager受众会跟踪客户当前的同意首选项，而Experience Event则可保存客户在收集事件时处于活动状态的同意首选项。

要收集有关事件的同意信息，需要满足以下条件：

- 基于[!DNL XDM Experience Event]类且具有[!DNL Experience Event]隐私架构字段组的数据集。
- 使用上述[!DNL XDM Experience Event]数据集设置的数据流。

有关如何将XDM Experience Event转换为Analytics点击的更多信息，请参阅[使用Web SDK将数据发送到Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md)。

## Adobe Experience Platform Web SDK集成

以下部分介绍IAB TCF 2.0与Adobe Experience Platform Web SDK之间的主要集成点。

>[!NOTE]
>
>即使未设置Real-Time CDP或Audience Manager，您仍可以将IAB TCF 2.0与Web SDK集成。 同意首选项可用于控制Experience事件的收集和设置身份Cookie。

### 默认同意

当尚未为客户保存同意首选项时，使用默认同意。 这意味着默认同意选项可以控制Adobe Experience Platform Web SDK的行为，并根据客户的区域进行更改。

例如，如果您的客户不在通用数据保护条例(GDPR)的管辖范围内，则默认同意可以设置为`in`，但在GDPR的管辖范围内，默认同意可以设置为`pending`。 您的同意管理平台(CMP)可能会检测客户的区域，并向IAB TCF 2.0提供标记`gdprApplies`。此标记可用于设置默认同意。 有关详细信息，请参阅[`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)。

### 更改时设置同意

Adobe Experience Platform Web SDK有一个`setConsent`命令，可使用IAB TCF 2.0将客户的同意首选项传达给所有Adobe服务。如果您要与Real-Time CDP集成，这会更新客户的个人资料。 如果您要与Audience Manager集成，这会更新您的客户信息。 调用此参数还会设置一个包含“全有或全无”同意首选项的Cookie，用于控制是否允许发送未来的体验事件。 其目的是每当同意更改时，都会调用此操作。 在将来的页面加载中，将读取Edge Network同意Cookie以确定是否可以发送Experience事件，以及是否可以设置身份Cookie。

与Audience Manager的IAB TCF 2.0集成类似，当客户明确同意以下目的时，Edge Network也会表示同意：

- **目的1：**&#x200B;存储和/或访问设备上的信息
- **目的10：**&#x200B;开发和改进产品
- **特殊目的1：**&#x200B;确保安全性、防止欺诈和调试。 （根据IAB TCF法规，此规定始终征得同意）
- **Adobe供应商权限：**&#x200B;同意Adobe （供应商565）

有关`setConsent`命令的详细信息，请阅读有关[setConsent](../../../web-sdk/commands/setconsent.md)的专用Web SDK文档。

### 向体验事件添加同意

Adobe Experience Platform Web SDK具有收集Experience事件的[`sendEvent`](/help/web-sdk/commands/sendevent/overview.md)命令。 如果您要与Experience Event或Adobe Analytics集成，并且希望获得每个Experience Event的同意首选项，请向每个`sendEvent`命令添加同意信息。

## 后续步骤

现在您已基本了解IAB透明度和同意框架2.0，请参阅关于将IAB TCF 2.0 [与标记](./with-tags.md)一起使用或[不使用标记](./without-tags.md)的任一指南。
