---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360 Destination
seo-title: Google Display & Video 360 Destination
description: Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。
seo-description: 'Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。 '
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] 目标

## 概述

[!DNL Display & Video 360]它以前称为 [!DNL DoubleClick Bid Manager]工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。

## 目标规范

请注意特定于目标的以下详细 [!DNL Google Display & Video 360] 信息：

* 您可以将以下身份 [发送](../../../identity-service/namespaces.md) 到目 [!DNL Google Display & Video 360] 标：Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID和AmazonFire TV ID。
* 激活的受众是在Google平台中以编程方式创建的。
* 实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且过去(使用 [Adobe Audience Manager或其他应用程序](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) )Experience CloudID服务中未启用ID同步功能，请联系Adobe咨询或客户关怀以启用ID同步。 如果您以前在Audience Manager中设置Google集成，则您设置的ID同步将结转到实时CDP。

### 导出类型 {#export-type}

**区段导出** -您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 允许列表

>[!NOTE]
>
>在以实时CDP设置您的第 [!DNL Google Display & Video 360] 一个目标之前，必须进行允许列表。 在创建目标之前，请确保Google已完成下面描述的允许列表过程。

在实时 [!DNL Google Display & Video 360] CDP中创建目标之前，您必须联系Google，要求对允许的Adobe提供者进行列表，并将您的帐户添加到允许列表。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在谷歌的帐户ID。 请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的Google客户帐户ID。 请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **您的帐户类型**:使 **[!DNL Invite advertiser]** 用以仅允许受众共享到您的Display &amp; Video 360帐户中的特定品牌，或 **[!DNL Invite partner]** 者使用以允许受众共享到您的Display &amp; Video 360帐户中的所有品牌。

## 配置目标

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Google Display & Video 360]，选 **[!UICONTROL 择并选择“]**&#x200B;配置”。

![Connect Google Display &amp; Video 360目标](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 [!UICONTROL 间差异] 的详 [!UICONTROL 细信]息，请参 [阅目标工](../../ui/destinations-workspace.md#catalog) 作区文档的“目录”部分。

在创 **建目标** 工作流的设置步骤中，填写目标的 [!UICONTROL 基本信息] ，以及应应用于此目标的市场营销用例。

![基本信息Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 使 `Invite Advertiser` 用以仅允许受众共享到您的显示和视频360帐户中的特定品牌。
   * 使 `Invite Partner` 用，允许受众共享到您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**:使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。 通常，这是一个6或7位数字ID。
* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](../../../rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](../../../data-governance/policies/overview.md#core-actions)。

>[!NOTE]
>
>设置目标时，请 [!DNL Google Display & Video 360] 与您的或Adobe [!DNL Google Account Manager] 代表联系，了解您的帐户类型。

## 将区段激活到 [!DNL Google Display & Video 360]

有关如何将区段激活到目的地的说 [!DNL Google Display & Video 360]明，请 [参阅将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到目 [!DNL Google Display & Video 360] 标，请检查您的 [!DNL Google Display & Video 360] 帐户。 如果激活成功，则受众将填充到您的帐户中。