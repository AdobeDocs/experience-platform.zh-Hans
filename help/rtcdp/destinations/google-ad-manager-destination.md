---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Google Ad Manager目标
seo-title: Google Ad Manager目标
description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
seo-description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## 概述

[!DNL Google Ad Manager]它以前为发 [!DNL DoubleClick] 行商或 [!DNL DoubleClick AdX]者所称，是一个广告服务平台，它使发行商能够通过视频和移动 [!DNL Google] 应用程序管理其网站上的广告显示。

## 目标规范

请注意特定于目标的以下详细 [!DNL Google Ad Manager] 信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到目 [!DNL Google Ad Manager] 标： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon火电电视ID**。
* 激活的受众在平台中以编程方式 [!DNL Google] 创建。
* Adobe实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望创建您的第一个目标， [!DNL Google Ad Manager] 并且过去(使用Experience Cloud [ID或其他应用程序)未启用Audience ManagerID服务中的](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，请联系Adobe咨询或客户服务部以启用ID同步。 如果您以前在Audience Manager [!DNL Google] 中设置集成，则您设置的ID同步将转入Adobe实时CDP。

### 导出类型 {#export-type}

**区段导出** -您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 允许列表

>[!NOTE]
>
>在允许列表实时CDP中设置您的 [!DNL Google Ad Manager] 第一个目标之前，必须进行Adobe。 在创建目标之前，请确保已完成下面 [!DNL Google] 描述的允许列表过程。

在Adobe实 [!DNL Google Ad Manager] 时CDP中创建目标之前，您必须联系 [!DNL Google] Adobe，让进入允许的数据提供者列表，并将您的帐户添加到允许列表。 联系 [!DNL Google] 并提供以下信息：

* **帐户ID** :这是Adobe的帐户ID [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的客户帐户ID [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **网络ID** :这是您的帐户 [!DNL Google Ad Manager]
* **受众链接ID** :这是您的帐户 [!DNL Google Ad Manager]
* 您的帐户类型。 Google或AdX买家提供的DFP。

## 配置目标

1. 在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 **[!DNL Google Ad Manager]**，选 **[!UICONTROL 择并选择“]**配置”。
   ![连接Google Ad Manager目标](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](/help/rtcdp/destinations/destinations-workspace.md#catalog) 作区文档的“目录”部分。

2. 在创建 **目标** 工作流的设置步骤中，填写目 [!UICONTROL 标的基本信] 息。 <br>

   ![基本信息Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 供发 `DFP by Google` 布 [!DNL DoubleClick] 者使用
   * 用 `AdX buyer` 于 [!DNL Google AdX]
* **[!UICONTROL 帐户ID]**:用填写您的帐户ID [!DNL Google]。 这可以是您的网络ID或受众链接ID。 通常，这是一个8位数字的ID。
* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](/help/data-governance/policies/overview.md#core-actions)。

>[!NOTE]
>
> 设置目标时，请 [!DNL Google Ad Manager] 与您的或Adobe [!DNL Google Account Manager] 代表联系，了解您的帐户类型。

## 将区段激活到 [!DNL Google Ad Manager]

有关如何将区段激活到目的地的说 [!DNL Google Ad Manager]明，请 [参阅将数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到目 [!DNL Google Ad Manager] 标，请检查您的 [!DNL Google Ad Manager] 帐户。 如果激活成功，则受众将填充到您的帐户中。