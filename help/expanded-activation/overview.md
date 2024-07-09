---
title: Audience Manager 扩展激活
description: 了解如何通过Audience Manager扩展的激活，将Audience Manager受众激活到社交和广告目标。
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Audience Manager 扩展激活

Audience Manager扩展激活基于Adobe Experience Platform构建，可帮助现有 [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) 用户将其受众激活到 [社交](../destinations/catalog/social/overview.md) 和 [广告](../destinations/catalog/advertising/overview.md) Real-Time CDP的目标平台，例如 [facebook](../destinations/catalog/social/facebook.md)， [Google Ads](../destinations/catalog/advertising/google-ads-destination.md)，等等。

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] 仅适用于现有 [!DNL Audience Manager] 用户。

## 术语 {#terminology}

Audience Manager扩展激活使用Adobe Experience Platform中的概念和组件。 要更好地了解扩展的激活工作流程以及您将使用的组件，请确保您对以下概念有基本了解：

* [受众](../segmentation/ui/overview.md)：受众是指一组具有相似行为和/或特征的人员。 此人员集合可以由Adobe Experience Platform使用区段定义或受众合成（平台生成的受众）生成，也可以由外部源(例如自定义上传（外部生成的受众）)生成。 在扩展激活中，您的Audience Manager区段（受众）导入为 [自定义上传](../segmentation/ui/audience-portal.md#import-audience).
* [Source连接器](../sources/home.md)：Source连接器（也称为源）可帮助Experience Platform用户轻松地从多个源摄取数据，从而能够使用Experience Platform服务来构建、标记和增强数据。 数据可以从各种源摄取，如基于云的存储、第三方软件和CRM系统。
* [目标连接器](../destinations/home.md)：目标描述从中激活和交付受众的任何端点，如Adobe应用程序、广告平台、云存储服务或营销服务。 [!DNL Expanded Activation] 支持将受众激活到 [广告](../destinations/catalog/advertising/overview.md) 和 [社交](../destinations/catalog/social/overview.md) 目标连接器。

## 先决条件 {#prerequisites}

在通过扩展激活来激活受众之前，请确保您满足下述先决条件。

### 用户和角色要求 {#permission-requirements}

在可以使用之前 [!DNL Expanded Activation]，您必须从Admin Console创建用户帐户并将其分配给 [!DNL Expanded Activation] 角色。 请参阅 [管理](administration.md) 页面，以了解有关如何执行此操作的详细说明。

### 受众要求 {#audience-requirements}

要通过激活受众，请执行以下操作 [!DNL Expanded Activation]，确保您的Audience Manager受众基于 **经过哈希处理的电子邮件地址**. 根据您的Audience Manager使用情况，可通过两种方式确保这一点：

* 如果您使用 [Audience Manager基于人员的目标](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 功能，则您已在Audience Manager中摄取经过哈希处理的电子邮件地址。 在这种情况下，无需执行任何其他步骤。 您可以跳至 [通过扩展的激活来激活受众](activate-audiences.md).
* 如果您是 _非_ 使用 [Audience Manager基于人员的目标](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 功能，您必须在Audience Manager中创建新数据源，并使用它存储经过哈希处理的电子邮件地址。 请参阅相关文档 [为经过哈希处理的电子邮件工作流配置数据源](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) 来学习如何做到这一点。 在Audience Manager数据源中摄取经过哈希处理的电子邮件地址后，请阅读相关的文档 [通过扩展的激活来激活受众](activate-audiences.md).

## 后续步骤 {#next-steps}

现在，您已更好地了解了使用的用例和好处 [!DNL Expanded Activation]，开始 [配置帐户](administration.md) 然后 [激活您的受众](activate-audiences.md).
