---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Adobe Experience Platform中的同意处理
description: 了解如何使用Adobe2.0标准在Adobe Experience Platform中处理客户同意信号。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---

# Adobe Experience Platform中的同意处理

Adobe Experience Platform允许您处理从客户那里收集的同意数据，并将其集成到存储的客户配置文件中。 然后，下游流程可使用此数据来确定数据收集是针对特定客户进行的，还是将其用户档案用于特定目的。 例如，特定用户档案的同意数据可以确定它是否可以包含在导出的受众区段中，或者它是否可以参与特定的营销渠道，如电子邮件、文本消息或推送通知。

本文档概述了如何配置您的Platform数据操作，以摄取由同意管理平台(CMP)生成的客户同意数据，并将该数据集成到客户配置文件中，以用于下游用例。

>[!NOTE]
>
>本文档重点介绍如何使用Adobe标准处理同意数据。 如果您在按照IAB透明度和同意框架(TCF) 2.0处理同意数据，请参阅 [Adobe Real-time Customer Data Platform中的TCF 2.0支持](../iab/overview.md).

## 先决条件

本指南要求您实际了解处理同意数据时涉及的各种Experience Platform服务：

* [体验数据模型(XDM)](../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity服务](../../../../identity-service/home.md)：通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [Real-time Customer Profile](../../../../profile/home.md)：用法 [!DNL Identity Service] 能够实时从数据集创建详细的客户配置文件。 Real-time Customer Profile从Data Lake中提取数据，并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md)：客户端JavaScript库，用于将各种Platform服务集成到面向客户的网站上。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md)：本指南中显示的与同意相关的SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md)：允许您将实时客户个人资料数据划分到一组个人资料中，这些个人资料具有相似的特征，且对营销策略的响应类似。

## 同意处理流程摘要 {#summary}

下面介绍了在正确配置系统后如何处理同意数据：

1. 客户通过网站上的对话框提供其关于数据收集的同意首选项。
1. 在每次页面加载时（或当CMP检测到同意首选项更改时），网站上的自定义脚本将当前首选项映射到标准XDM对象。 然后，将此对象传递到Platform Web SDK `setConsent` 命令。
1. 时间 `setConsent` 调用，Platform Web SDK会检查同意值是否与上次收到的值不同。 如果值不同（或没有以前的值），则将结构化同意/偏好设置数据发送到Adobe Experience Platform。
1. 同意/偏好设置数据会引入 [!DNL Profile]启用了数据集，其架构包含同意/偏好设置字段。

除了CMP同意更改挂接触发的SDK命令之外，同意数据还可以通过客户生成的任何直接上传到的XDM数据流入Experience Platform [!DNL Profile] — 启用的数据集。

### 同意执行

在Platform中同意处理支持的当前版本中，只有数据收集权限(`collect.val`)由Platform Web SDK自动实施。 虽然可以收集更细粒度的同意和偏好设置并将其保留在客户配置文件中，但这些附加信号必须在您自己的下游流程中手动实施。

>[!NOTE]
>
>有关上述XDM同意字段结构的更多信息，请参阅 [[!UICONTROL 同意和偏好设置] 数据类型](../../../../xdm/data-types/consents.md).

配置系统后，Platform Web SDK会解释当前用户的数据收集同意值，以确定数据应发送到Adobe Experience Platform Edge Network、从客户端删除还是保留，直到数据收集权限设置为“是”或“否”。

## 确定如何在CMP中生成客户同意数据 {#consent-data}

由于每个CMP系统都是唯一的，因此您必须确定允许客户在与您的服务交互时提供同意的最佳方式。 实现此目标的常见方法是使用Cookie同意对话框，类似于以下示例：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此对话框应允许客户选择加入或退出其数据的特定营销和个性化用例。 这些同意和偏好设置应符合您为定义的数据模型 [!DNL Profile] — 在下一步中启用数据集。

## 将标准化同意字段添加到 [!DNL Profile]启用数据集 {#dataset}

客户同意数据必须发送至 [!DNL Profile]启用了数据集，其架构包含同意字段。 这些字段必须包含在用于捕获有关各个客户的属性信息的相同架构和数据集中。

请参阅以下教程： [配置用于捕获同意数据的数据集](./dataset.md) 有关如何将这些必填字段添加到的详细步骤 [!DNL Profile]-enabled dataset，然后再继续本指南。

## 更新 [!DNL Profile] 合并策略以包含同意数据 {#merge-policies}

创建 [!DNL Profile]启用用于处理同意数据的数据集，您必须确保合并策略已配置为在每个客户配置文件中始终包含同意字段。 这涉及设置数据集优先级，以使您的同意数据集优先于其他潜在冲突的数据集。

>[!NOTE]
>
>如果您没有任何冲突的数据集，则应该为合并策略设置时间戳优先顺序。 这有助于确保客户指定的最新同意是使用的同意设置。

有关如何使用合并策略的更多信息，请从阅读 [合并策略概述](../../../../profile/merge-policies/overview.md). 在设置合并策略时，必须确保配置文件中包含由提供的所有必需的同意属性。 [!UICONTROL 同意和偏好设置] 模式字段组，如以下指南中所述： [数据集准备](./dataset.md).

## 将同意数据引入平台

一旦您拥有数据集并合并策略，以表示客户配置文件中所需的同意字段，下一步是将同意数据本身引入平台。

通常，只要CMP检测到同意更改事件，您就应使用Adobe Experience Platform Web SDK将同意数据发送到Platform。 如果您在移动平台上收集同意数据，则应当使用Adobe Experience Platform Mobile SDK。 您还可以选择直接摄取收集的同意数据，方法是将其映射到同意数据集的XDM架构并通过批量摄取将其发送到Platform。

以下各小节提供了每种方法的详细信息。

### 配置Experience PlatformWeb SDK以处理同意数据 {#web-sdk}

将CMP配置为监听网站上的同意更改事件后，您可以集成Experience PlatformWeb SDK以接收更新的同意设置，并在每次加载页面时和发生同意更改事件时将其发送到Platform。 请参阅指南，网址为 [配置Web SDK以处理客户同意数据](../sdk.md) 了解更多信息。

### 配置Experience PlatformMobile SDK以处理同意数据 {#mobile-sdk}

如果您的移动应用程序需要客户同意首选项，则可以集成Experience PlatformMobile SDK以检索和更新同意设置，并在调用同意API时将它们发送到Platform。

请参阅Mobile SDK文档，了解 [配置Consent移动扩展](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) 和 [使用同意API](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). 有关如何使用Mobile SDK处理隐私问题的更多详细信息，请参阅部分 [隐私和GDPR](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### 直接摄取符合XDM标准的同意数据 {#batch}

您可以使用批量摄取从CSV文件中摄取与XDM兼容的同意数据。 如果您有尚未集成到客户配置文件中的先前收集的同意数据的积压，则此功能会非常有用。

请阅读以下教程： [将CSV文件映射到XDM](../../../../ingestion/tutorials/map-csv/overview.md) 了解如何将数据字段转换为XDM并将其摄取到Platform。 选择 [!UICONTROL 目标] 对于映射，请确保选择 **[!UICONTROL 使用现有数据集]** 选项，然后选择 [!DNL Profile] — 启用了您之前创建的同意数据集。

## 测试实施 {#test-implementation}

将客户同意数据摄取到 [!DNL Profile]-enabled数据集，您可以检查更新的配置文件，以查看它们是否包含同意属性。

>[!IMPORTANT]
>
>要在UI中查看现有配置文件的属性，您必须至少知道一个与该配置文件关联的身份值（及其对应的命名空间）。
>
>如果您无权访问此信息，则可以选择摄取您自己的测试同意数据，并将其与已知的身份值/命名空间关联。

请参阅以下部分： [按身份浏览配置文件](../../../../profile/ui/user-guide.md#browse) 在 [!DNL Profile] 有关如何查找用户档案详细信息的特定步骤的UI指南。

默认情况下，新的同意属性不会显示在用户档案的仪表板上。 因此，您必须导航到 **[!UICONTROL 属性]** 选项卡，以确认已按预期摄取用户档案。 请参阅 [配置文件仪表板](../../../../profile/ui/profile-dashboard.md) 以了解如何根据您的需求自定义仪表板。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 后续步骤

本指南介绍了如何配置您的Platform操作，以使用Adobe标准处理客户同意数据，并在客户配置文件中表示这些属性。 您现在可以将客户同意偏好设置作为区段鉴别和其他下游用例中的决定性因素进行集成。

有关Experience Platform隐私权相关功能的更多信息，请参阅 [Platform中的治理、隐私和安全性](../../overview.md).
