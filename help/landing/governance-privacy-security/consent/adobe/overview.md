---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 在Adobe Experience Platform中处理同意
topic-legacy: getting started
description: 了解如何在Adobe Experience Platform中使用Adobe2.0标准处理客户同意信号。
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---

# 在Adobe Experience Platform中处理同意

Adobe Experience Platform允许您处理从客户收集的同意数据，并将其集成到存储的客户配置文件中。 然后，下游流程可以使用此数据来确定是否针对特定客户进行数据收集，或者其配置文件是否用于特定目的。 例如，特定用户档案的同意数据可确定该用户档案是否可以包含在导出的受众区段中，或者该用户档案是否可以参与特定的营销渠道，如电子邮件、文本消息或推送通知。

本文档概述了如何配置Platform数据操作，以摄取由同意管理平台(CMP)生成的客户同意数据，并将该数据集成到客户配置文件中以用于下游用例。

>[!NOTE]
>
>本文档重点介绍如何使用Adobe标准处理同意数据。 如果您要处理符合IAB透明度和同意框架(TCF)2.0的同意数据，请参阅 [Adobe Real-time Customer Data Platform中的TCF 2.0支持](../iab/overview.md).

## 先决条件

本指南要求您对处理同意数据所涉及的各种Experience Platform服务有一定的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。
* [实时客户资料](../../../../profile/home.md):使用 [!DNL Identity Service] 功能从数据集实时创建详细的客户用户档案。 实时客户资料从数据湖中提取数据，并将客户资料保留在其单独的数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):客户端JavaScript库，允许您将各种平台服务集成到面向客户的网站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中显示的与同意相关的SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md):允许您将实时客户资料数据划分为一组具有相似特征并将对营销策略做出类似响应的个人。

## 同意处理流程摘要 {#summary}

以下说明在正确配置系统后如何处理同意数据：

1. 客户通过网站上的对话框为数据收集提供其同意首选项。
1. 在每次加载页面时（或当CMP检测到同意首选项发生更改时），您网站上的自定义脚本会将当前首选项映射到标准XDM对象。 然后，此对象将传递到Platform Web SDK `setConsent` 命令。
1. When `setConsent` 调用时，Platform Web SDK会检查同意值是否与上次收到的同意值不同。 如果值不同（或者没有前一个值），则结构化的同意/首选项数据会发送到Adobe Experience Platform。
1. 同意/首选项数据被摄取到 [!DNL Profile] — 启用的数据集，其架构包含同意/首选项字段。

除了由CMP同意更改挂钩触发的SDK命令外，同意数据还可以通过任何由客户生成的XDM数据流入Experience Platform，这些数据会直接上传到 [!DNL Profile] — 已启用的数据集。

### 同意执行

在Platform当前版本的同意处理支持中，仅具有数据收集权限(`collect.val`)会由平台Web SDK自动强制执行。 虽然可以在客户配置文件中收集和保留更细粒度的同意和首选项，但必须在您自己的下游流程中手动强制执行这些附加信号。

>[!NOTE]
>
>有关上述XDM同意字段结构的更多信息，请参阅 [[!UICONTROL 同意和首选项] 数据类型](../../../../xdm/data-types/consents.md).

配置系统后，Platform Web SDK会解释当前用户的数据收集同意值，以确定是否应将数据发送到Adobe Experience Platform边缘网络、从客户端删除，还是持久保留，直到数据收集权限设置为“是”或“否”。

## 确定如何在CMP中生成客户同意数据 {#consent-data}

由于每个CMP系统都是唯一的，因此您必须确定在客户与您的服务进行交互时允许其提供同意的最佳方式。 实现此目的的常见方法是使用Cookie同意对话框，如下例所示：

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

此对话框应允许客户为其数据选择加入或退出特定营销和个性化用例。 这些同意和首选项应符合您为 [!DNL Profile] — 在下一步中启用了数据集。

## 向 [!DNL Profile]已启用的数据集 {#dataset}

必须将客户同意数据发送到 [!DNL Profile] — 启用的数据集，其架构包含同意字段。 这些字段必须包含在用于捕获有关单个客户的属性信息的相同架构和数据集中。

请参阅 [配置用于捕获同意数据的数据集](./dataset.md) ，以了解有关如何将这些必填字段添加到 [!DNL Profile] — 启用的数据集，然后再继续使用本指南。

## 更新 [!DNL Profile] 合并策略以包含同意数据 {#merge-policies}

创建 [!DNL Profile] — 启用了用于处理同意数据的数据集，您必须确保已将合并策略配置为始终在每个客户配置文件中包含同意字段。 这包括设置数据集优先级，以便同意数据集优先于其他可能存在冲突的数据集。

>[!NOTE]
>
>如果没有任何冲突的数据集，则应该为合并策略设置时间戳优先级。 这有助于确保客户指定的最新同意是所使用的同意设置。

有关如何使用合并策略的更多信息，请首先阅读 [合并策略概述](../../../../profile/merge-policies/overview.md). 在设置合并策略时，必须确保用户档案包含 [!UICONTROL 同意和首选项] 架构字段组，如 [数据集准备](./dataset.md).

## 将同意数据导入平台

在您拥有数据集和合并策略以在客户配置文件中表示必需的同意字段后，下一步是将同意数据本身引入Platform。

主要是，当CMP检测到同意更改事件时，您应使用Adobe Experience Platform Web SDK将同意数据发送到平台。 如果您在移动平台上收集同意数据，则应使用Adobe Experience Platform Mobile SDK。 您还可以选择直接摄取收集的同意数据，方法是将收集的同意数据映射到同意数据集的XDM架构，并通过批量摄取将其发送到平台。

下面各小节中提供了每种方法的详细信息。

### 配置Experience PlatformWeb SDK以处理同意数据 {#web-sdk}

将CMP配置为监听网站上的同意更改事件后，您可以集成Experience PlatformWeb SDK以接收更新的同意设置，并在每次页面加载时以及每当发生同意更改事件时将它们发送到平台。 请参阅 [配置Web SDK以处理客户同意数据](../sdk.md) 以了解更多信息。

### 配置Experience PlatformMobile SDK以处理同意数据 {#mobile-sdk}

如果您的移动设备应用程序中需要Experience Platform同意首选项，则可以集成客户Mobile SDK以检索和更新同意设置，每当调用同意API时，都会将它们发送到Platform。

有关 [配置同意移动扩展](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) 和 [使用同意API](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). 有关如何使用Mobile SDK处理隐私问题的更多详细信息，请参阅部分 [隐私和GDPR](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### 直接摄取符合XDM标准的同意数据 {#batch}

您可以使用批量摄取从CSV文件中摄取符合XDM规范的同意数据。 如果您之前收集的同意数据积压，且尚未集成到客户配置文件中，则此功能会非常有用。

请阅读本教程 [将CSV文件映射到XDM](../../../../ingestion/tutorials/map-a-csv-file.md) 了解如何将数据字段转换为XDM并将其摄取到平台。 选择 [!UICONTROL 目标] 对于映射，请确保选择 **[!UICONTROL 使用现有数据集]** 选项，然后选择 [!DNL Profile] — 已启用您之前创建的同意数据集。

## 测试实施 {#test-implementation}

在将客户同意数据摄取到 [!DNL Profile]启用的数据集中，您可以检查更新的配置文件，以确定是否包含同意属性。

>[!IMPORTANT]
>
>要在UI中查看现有配置文件的属性，您必须至少知道一个与该配置文件关联的标识值（及其对应的命名空间）。
>
>如果您无权访问此信息，则可以选择摄取您自己的测试同意数据，并将其与您已知的身份值/命名空间相关联。

请参阅 [按身份浏览用户档案](../../../../profile/ui/user-guide.md#browse) 在 [!DNL Profile] 有关如何查找用户档案详细信息的特定步骤的UI指南。

默认情况下，新的同意属性不会显示在用户档案的功能板上。 因此，您必须导航到 **[!UICONTROL 属性]** 选项卡，以确认已按预期摄取了这些量度。 请参阅 [配置文件仪表板](../../../../profile/ui/profile-dashboard.md) 了解如何自定义功能板以满足您的需求。

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 后续步骤

本指南介绍了如何配置您的平台操作以使用Adobe标准处理客户同意数据，并让这些属性显示在客户配置文件中。 现在，您可以将客户同意首选项作为区段鉴别和其他下游用例中的决定性因素进行集成。

有关Experience Platform隐私相关功能的更多信息，请参阅 [平台中的管理、隐私和安全](../../overview.md).
