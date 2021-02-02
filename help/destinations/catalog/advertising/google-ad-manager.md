---
keywords: google广告管理器；google广告；doubleclick;DoubleClick AdX;DoubleClick;Google广告管理器；Google广告管理器
title: Google Ad Manager目标
seo-title: Google Ad Manager目标
description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
seo-description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## 概述

[!DNL Google Ad Manager]此前称为“ [!DNL DoubleClick] 发布者”或 [!DNL DoubleClick AdX]“广告服务平台”，它 [!DNL Google] 为出版商提供了通过视频和移动应用程序管理其网站上广告显示的方法。

## 目标规范

请注意特定于[!DNL Google Ad Manager]目标的以下详细信息：

* 可以将以下[标识](../../../identity-service/namespaces.md)发送到[!DNL Google Ads]目标：[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)、Google cookie ID、IDFA、GAID、Roku ID、Microsoft ID和Amazon火电视ID。
   * Google将使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)目标加利福尼亚州的用户，并为所有其他用户使用Google Cookie ID。
* 激活的受众是在[!DNL Google]平台中以编程方式创建的。
* 平台当前不包括用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用[!DNL Google Ad Manager]创建您的第一个目标，并且过去(使用Experience Cloud或其他应用程序)未启用Audience ManagerID服务中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户服务部门以启用ID同步。 如果您以前在Audience Manager中设置[!DNL Google]集成，则您设置的ID同步将结转到平台。

### 导出类型{#export-type}

**区段导出** -您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 允许列表

>[!NOTE]
>
>在平台中设置第一个[!DNL Google Ad Manager]目标之前，此允许列表是必需的。 在创建目标之前，请确保[!DNL Google]已完成下面描述的允许列表过程。

在平台中创建[!DNL Google Ad Manager]目标之前，您必须联系[!DNL Google]，以便Adobe进入允许的数据提供者列表，并将您的帐户添加到允许列表。 联系[!DNL Google]并提供以下信息：

* **帐户ID** :这是Adobe的帐户ID  [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的客户帐户ID  [!DNL Google]请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **网络ID** :这是您的帐户  [!DNL Google Ad Manager]
* **受众链接ID** :这是您的帐户  [!DNL Google Ad Manager]
* 您的帐户类型。 Google或AdX买家提供的DFP。

## 配置目标

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择&#x200B;**[!DNL Google Ad Manager]**，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接Google Ad Manager目标](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在创建目标工作流的&#x200B;**设置**&#x200B;步骤中，填写目标的[!UICONTROL 基本信息]。

![基本信息Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 对发行商使用`DFP by Google`作为[!DNL DoubleClick]
   * 将`AdX buyer`用于[!DNL Google AdX]
* **[!UICONTROL 帐户ID]**:用填写您的帐户ID  [!DNL Google]。这可以是您的网络ID或受众链接ID。 通常，这是一个8位数字的ID。
* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关市场营销用例的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>设置[!DNL Google Ad Manager]目标时，请与您的[!DNL Google Account Manager]或Adobe代表联系，了解您的帐户类型。

## 将区段激活到[!DNL Google Ad Manager]

有关如何将区段激活到[!DNL Google Ad Manager]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Ad Manager]目标，请检查您的[!DNL Google Ad Manager]帐户。 如果激活成功，则受众将填充到您的帐户中。