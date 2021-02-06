---
keywords: DoubleClick竞价管理器；DoubleClick竞价管理器；DoubleClick；显示和视频360；显示360；视频360；视频360；显示360；显示和视频
title: Google Display & Video 360连接目标
description: Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] 连接

[!DNL Display & Video 360]它以前称为 [!DNL DoubleClick Bid Manager]工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。

## 目标规范

请注意特定于[!DNL Google Display & Video 360]目标的以下详细信息：

* 可以将以下[标识](../../../identity-service/namespaces.md)发送到[!DNL Google Ads]目标：[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)、Google cookie ID、IDFA、GAID、Roku ID、Microsoft ID和Amazon火电视ID。
   * Google将使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)目标加利福尼亚州的用户，并为所有其他用户使用Google Cookie ID。
* 激活的受众是在Google平台中以编程方式创建的。
* 平台当前不包括用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且过去(在Adobe Audience Manager或其他应用程序中)未启用Experience CloudID服务中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户服务部门以启用ID同步。 如果您以前在Audience Manager中设置Google集成，则您设置的ID同步将结转到平台。

### 导出类型{#export-type}

**区段导出** -您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 允许列表

>[!NOTE]
>
>在平台中设置第一个[!DNL Google Display & Video 360]目标之前，此允许列表是必需的。 在创建目标之前，请确保Google已完成下面描述的允许列表过程。

在平台中创建[!DNL Google Display & Video 360]目标之前，您必须联系Google，要求将Adobe置于允许的数据提供者列表，并将您的帐户添加到允许列表。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在谷歌的帐户ID。请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的Google客户帐户ID。请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **您的帐户类型**:使 **[!DNL Invite advertiser]** 用受众仅可共享给Display &amp; Video 360帐户中的特定品牌，或 **[!DNL Invite partner]** 者使用受众可共享给Display &amp; Video 360帐户中的所有品牌。

## 配置目标

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Google Display & Video 360]，然后选择&#x200B;**[!UICONTROL 配置]**。

![Connect Google Display &amp; Video 360目标](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关[!UICONTROL Activate]和[!UICONTROL Configure]之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在创建目标工作流的&#x200B;**设置**&#x200B;步骤中，填写目标的[!UICONTROL 基本信息]以及应适用于此目标的市场营销用例。

![基本信息Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 使用`Invite Advertiser`可仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用`Invite Partner`允许将受众共享给Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**:使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。通常，这是一个6或7位数字ID。
* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关市场营销用例的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>设置[!DNL Google Display & Video 360]目标时，请与您的[!DNL Google Account Manager]或Adobe代表联系，了解您的帐户类型。

## 将区段激活到[!DNL Google Display & Video 360]

有关如何将区段激活到[!DNL Google Display & Video 360]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Display & Video 360]目标，请检查您的[!DNL Google Display & Video 360]帐户。 如果激活成功，则受众将填充到您的帐户中。