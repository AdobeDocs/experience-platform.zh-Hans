---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Google AdsDestination
seo-title: Google广告目标
description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
seo-description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# [!DNL Google Ads] 目标

## 概述

[!DNL Google Ads]在线广告服 [!DNL Google AdWords]务，它使企业能够跨基于文本的搜索、图形显示、视频和应用程序内移动显示屏按点击 [!DNL YouTube] 付费投放广告。

## 目标规范

请注意特定于目标的以下详细 [!DNL Google Ads] 信息：

* 您可以将以下身份 [发送](../../../identity-service/namespaces.md) 到目 [!DNL Google Ads] 标：Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID和AmazonFire TV ID。
* 激活的受众在平台中以编程方式 [!DNL Google] 创建。
* 实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望创建您的第一个目标， [!DNL Google Ads] 并且过去(使用Experience Cloud [ID或其他应用程序)未启用Audience ManagerID服务中的](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) ID同步功能，请联系Adobe咨询或客户服务部以启用ID同步。 如果您以前在Audience Manager中设置Google集成，则您设置的ID同步将结转到实时CDP。

### 导出类型 {#export-type}

**区段导出** -您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 现有帐 [!DNL Google Ads] 户

[!DNL Google] 已暂停与第三方 [!DNL Google Ads] 供应商的任何新集成。 您必须与现有集 [!DNL Google Ads] 成，才能执行下一节中的允许列表步骤，并在实时CDP [!DNL Google Ads] 中创建目标。

### 允许列表

>[!NOTE]
>
>在以实时CDP设置您的第 [!DNL Google Ads] 一个目标之前，必须进行允许列表。 在创建目标之前，请确保已完成下面 [!DNL Google] 描述的允许列表过程。

在实时 [!DNL Google Ads] CDP中创建目标之前，您必须联系 [!DNL Google] Adobe，让列表加入允许的数据提供者的，并让帐户添加到允许列表。 联系 [!DNL Google] 并提供以下信息：

* **帐户ID** :这是Adobe的帐户ID [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的客户帐户ID [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* 您的帐户类型： **AdWords**
* **Google AdWords ID** :这是你的身份证 [!DNL Google]。 ID格式通常为123-456-7890。

## 配置目标

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Google Ads]，选 **[!UICONTROL 择并选择“]**&#x200B;配置”。

![连接Google广告目标](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](../../ui/destinations-workspace.md#catalog) 作区文档的“目录”部分。

在创建 **目标** 工作流的设置步骤中，填写目 [!UICONTROL 标的基本信] 息。

![Google Ads的基本信息](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**:AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**:用填写您的帐户ID [!DNL Google Ads]。 ID格式通常为123-456-7890。
* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](../../../rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](../../../data-governance/policies/overview.md#core-actions)。

## 将区段激活到 [!DNL Google Ads]

有关如何将区段激活到目的地的说 [!DNL Google Ads]明，请 [参阅将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到目 [!DNL Google Ads] 标，请检查您的 [!DNL Google Ads] 帐户。 如果激活成功，则受众将填充到您的帐户中。