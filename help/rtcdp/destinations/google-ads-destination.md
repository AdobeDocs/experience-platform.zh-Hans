---
title: Google AdsDestination
seo-title: Google广告目标
description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
seo-description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# [!DNL Google Ads] 目标

## 概述

[!DNL Google Ads]在线广告服 [!DNL Google AdWords]务，它使企业能够跨基于文本的搜索、图形显示、视频和应用程序内移动显示屏按点击 [!DNL YouTube] 付费投放广告。

## 目标规范

请注意特定于目标的以下详细 [!DNL Google Ads] 信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到目 [!DNL Google Ads] 标： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众在平台中以编程方式 [!DNL Google] 创建。
* Adobe实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望创建您的第一个目标， [!DNL Google Ads] 并且过去(使用Experience Cloud [ID或其他应用程序](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) )未启用Audience ManagerID服务中的ID同步功能，请联系Adobe Consulting或客户服务部以启用ID同步。 如果您以前在Audience Manager中设置Google集成，则您设置的ID同步将结转到Adobe实时CDP。

## 先决条件

### 现有帐 [!DNL Google Ads] 户

[!DNL Google] 已暂停与第三方 [!DNL Google Ads] 供应商的任何新集成。 您必须与现有集成 [!DNL Google Ads] ，才能执行下一节中的允许列表步骤，并在Adobe实时CDP [!DNL Google Ads] 中创建目标。

### 允许列表

>[!NOTE]
>
>在Adobe实时CDP中设置您的第 [!DNL Google Ads] 一个目标之前，此允许列表是必需的。 在创建目标之前，请确保已完成下面 [!DNL Google] 描述的允许列表过程。

在Adobe实 [!DNL Google Ads] 时CDP中创建目标之前，您必须联系 [!DNL Google] Adobe，让其承担允许的数据提供者的列表，并将您的帐户添加到允许列表。 联系 [!DNL Google] 并提供以下信息：

* **帐户ID** : 这是Adobe的帐户ID [!DNL Google]。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **客户ID** : 这是Adobe的客户帐户ID [!DNL Google]。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* 您的帐户类型： **AdWords**
* **Google AdWords ID** : 这是你的身份证 [!DNL Google]。 ID格式通常为123-456-7890。

## 创建目标

1. 在“连 **[!UICONTROL 接”>“目标]**”中，选 [!DNL Google Ads]择并选择“创 **[!UICONTROL 建目标”]**。
   ![连接Google广告目标](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 在创建 **目标** 工作流的设置步骤中，填写目 [!UICONTROL 标的基本信] 息。 <br>

   ![Google Ads的基本信息](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL 名称]**: 填写此目标的首选名称。
* **[!UICONTROL 描述]**: 可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**: AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**: 用填写您的帐户ID [!DNL Google Ads]。 ID格式通常为123-456-7890。
* **[!UICONTROL 营销用例]**: 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关Adobe定义的个别营销用例的信息，请参阅数 [据使用策略概述](/help/data-governance/policies/overview.md#core-actions)。

## 将区段激活到 [!DNL Google Ads]

有关如何将区段激活到目的地的说 [!DNL Google Ads]明，请 [参阅将数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。

