---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 在Adobe Experience Platform中处理同意
topic: getting started
description: 了解如何使用Adobe 2.0标准在Adobe Experience Platform中处理客户同意信号。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
translation-type: tm+mt
source-git-commit: a0f585e4aaeecb968a9fc9f408630946e1c30b2b
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 在Adobe Experience Platform中处理同意

Adobe Experience Platform允许您处理从客户那里收集的同意数据，并将其集成到存储的客户用户档案中。 然后，下游流程可以使用此数据来确定数据收集是否针对特定客户进行，或者其用户档案是否用于特定用途。 例如，特定用户档案的同意数据可确定是否可将其包含在导出的受众区段中，或者是否可以参与特定营销渠道（如电子邮件、文本消息或推送通知）。

本文档概述了如何配置您的平台数据操作，以摄取由同意管理平台(CMP)生成的客户同意数据，并将这些数据集成到客户用户档案中以用于下游用例。

>[!NOTE]
>
>此文档侧重于使用Adobe标准处理同意数据。 如果您要处理符合IAB透明度和同意框架(TCF)2.0的同意数据，请参阅有关实时客户数据平台](../iab/overview.md)中[TCF 2.0支持的指南。

## 先决条件

本指南要求对处理同意数据所涉及的各种Experience Platform服务进行有效了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../../../../profile/home.md):使用 [!DNL Identity Service] 功能从数据集实时创建详细的客户用户档案。实时客户用户档案从Data Lake中提取数据，并将客户用户档案保留在其自己的单独数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):客户端JavaScript库，允许您将各种平台服务集成到面向客户的网站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示的同意相关SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md):允许您将实时客户用户档案数据分为具有相似特征且响应类似营销策略的群体。

## 同意处理流程摘要{#summary}

以下说明在正确配置系统后如何处理同意数据：

1. 客户通过网站上的对话框提供数据收集的同意偏好。
1. 在每次载入页面时（或当CMP检测到同意首选项发生更改时），站点上的自定义脚本会将当前首选项映射到标准XDM对象。 然后，此对象将传递到Platform Web SDK `setConsent`命令。
1. 当调用`setConsent`时，平台Web SDK将检查同意值是否与上次收到的同意值不同。 如果这些值不同（或没有以前的值），则结构化的同意/首选项数据将发送到Adobe Experience Platform。
1. 同意/偏好数据被引入[!DNL Profile]启用的数据集中，其模式包含同意/偏好字段。

除了由CMP同意 — 更改挂接触发的SDK命令外，同意数据还可以通过任何客户生成的XDM数据流入Experience Platform，这些数据直接上传到支持[!DNL Profile]的数据集。

### 同意执行

在平台中当前版本的同意处理支持中，只有数据收集权限(`collect.val`)由平台Web SDK自动强制执行。 虽然可以在客户用户档案中收集和保留更细粒度的同意和偏好，但必须在您自己的下游流程中手动强制执行这些附加信号。

>[!NOTE]
>
>有关上述XDM同意字段结构的详细信息，请参阅[同意和首选项数据类型](../../../../xdm/data-types/consents.md)上的指南。

配置系统后，Platform Web SDK将解释当前用户的数据收集同意值，以确定应将数据发送到Adobe Experience Platform Edge Network、从客户端删除还是持续存在，直到数据收集权限设置为“是”或“否”。

## 确定如何在您的CMP {#consent-data}中生成客户同意数据

由于每个CMP系统都是独一无二的，因此您必须确定允许客户在与您的服务交互时提供同意的最佳方式。 实现此目的的常见方法是使用Cookie同意对话框，与以下示例类似：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此对话框应允许客选择加入户访问或退出其数据的特定营销和个性化使用案例。 这些同意和首选项应符合您在下一步中为启用[!DNL Profile]的数据集定义的数据模型。

## 将标准化同意字段添加到[!DNL Profile]启用的数据集{#dataset}

必须将客户同意数据发送到[!DNL Profile]已启用的模式包含同意字段的数据集。 这些字段必须包含在用于捕获各个客户的属性信息的同一模式和数据集中。

有关如何在继续使用本指南之前将这些必填字段添加到启用[!DNL Profile]的数据集的详细步骤，请参阅[配置数据集以捕获同意数据](./dataset.md)的教程。

## 更新[!DNL Profile]合并策略以包含同意数据{#merge-policies}

在为处理同意数据创建了启用[!DNL Profile]的数据集后，必须确保您的合并策略已配置为始终在每个客户用户档案中包含同意字段。 这包括设置数据集优先级，以便您的同意数据集优先于其他可能冲突的数据集。

>[!NOTE]
>
>如果没有任何冲突的数据集，则应改为设置合并策略的时间戳优先级。 这有助于确保客户指定的最新同意是使用的同意设置。

有关如何使用合并策略的详细信息，请参阅[合并策略用户指南](../../../../profile/ui/merge-policies.md)。 在设置合并策略时，您必须确保您的用户档案包含由“同意和首选项”混合提供的所有必需的同意属性，如[数据集准备](./dataset.md)指南中所述。

## 将同意数据导入平台

在您拥有数据集并合并策略以在客户用户档案中表示必需的同意字段后，下一步是将同意数据本身引入平台。

主要是，只要您的CMP检测到同意更改事件，您应使用Adobe Experience Platform Web SDK将同意数据发送到平台。 如果您在移动平台上收集同意数据，应使用Adobe Experience Platform Mobile SDK。 您还可以选择直接收集收集的同意数据，方法是将其映射到您同意数据集的XDM模式，并通过批量摄取将其发送到平台。

以下各小节提供了每种方法的详细信息。

### 配置Experience Platform Web SDK以处理同意数据{#web-sdk}

一旦您将CMP配置为在您的网站上侦听同意更改事件，您就可以集成Experience Platform Web SDK以接收更新的同意设置，并在每次加载页面时以及每当发生同意更改事件时将它们发送到平台。 有关详细信息，请参阅[配置Web SDK以处理客户同意数据](./sdk.md)的指南。

### 配置Experience Platform Mobile SDK以处理同意数据{#mobile-sdk}

如果您的移动应用程序中需要Experience Platform同意首选项，您可以集成Mobile SDK以检索和更新同意设置，每当调用同意API时会将其发送到平台。

有关使用“同意API”](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent/edge-consent-api-reference)配置“同意移动扩展”](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent)和“[”的信息，请参阅Mobile SDK文档。 [有关如何使用Mobile SDK处理隐私问题的更多详细信息，请参阅[隐私和GDPR](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/resources/privacy-and-gdpr)部分。

### 直接收集符合XDM的同意数据{#batch}

您可以使用批量摄取功能从CSV文件中摄取符合XDM规范的同意数据。 如果您之前收集的同意数据积压尚未整合到您的客户用户档案中，则此功能可能很有用。

请按照[将CSV文件映射到XDM](../../../../ingestion/tutorials/map-a-csv-file.md)上的教程，学习如何将数据字段转换为XDM并将其引入平台。 选择映射的[!UICONTROL Destination]时，请确保选择&#x200B;**[!UICONTROL Use existing dataset]**&#x200B;选项，然后选择您之前创建的[!DNL Profile]启用的同意数据集。

## 测试实施{#test-implementation}

在将客户同意数据引入[!DNL Profile]启用的数据集后，您可以检查更新的用户档案，以了解它们是否包含同意属性。

>[!IMPORTANT]
>
>要视图UI中现有用户档案的属性，您必须至少知道与该用户档案关联的一个标识值(及其相应命名空间)。
>
>如果您无权访问此信息，您可以选择收录您自己的测试同意数据，并将其与您所知的身份值/命名空间关联。

有关如何查找用户档案详细信息的具体步骤，请参阅[!DNL Profile]用户界面指南中关于[按标识](../../../../profile/ui/user-guide.md#browse)浏览用户档案的部分。

默认情况下，新的同意属性不会显示在用户档案的仪表板上。 因此，您必须导航到用户档案详细信息页面上的&#x200B;**[!UICONTROL Attributes]**&#x200B;选项卡，以确认已按预期方式摄取它们。 请参阅[用户档案仪表板](../../../../profile/ui/profile-dashboard.md)上的指南，了解如何自定义仪表板以满足您的需求。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 后续步骤

本指南介绍如何配置您的平台操作，以使用Adobe标准处理客户同意数据，并让这些属性在客户用户档案中表示。 现在，您可以将客户同意偏好整合为细分资格和其他下游使用案例的决定性因素。

有关Experience Platform隐私相关功能的详细信息，请参阅Platform](../../overview.md)中关于[治理、隐私和安全性的概述。
