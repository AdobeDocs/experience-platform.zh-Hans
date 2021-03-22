---
keywords: 双击竞价管理器；双击竞价管理器；双击；显示和视频360；显示360；视频360；视频360；显示360；显示360；显示和视频
title: Google Display & Video 360连接
description: Display & Video 360（以前称为DoubleClick竞价管理器）是一种工具，用于跨显示、视频和移动库存源执行重定向和受众目标数字活动。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] 连接

## 概述 {#overview}

[!DNL Display & Video 360]此工具以前称 [!DNL DoubleClick Bid Manager]为，用于跨显示、视频和移动库存源执行重定向和受众目标数字活动。

## 目标特性{#specifics}

请注意特定于[!DNL Google Display & Video 360]目标的以下详细信息：

* 激活的受众是在Google平台中以编程方式创建的。
* 平台当前不包括测量量度以验证成功激活。 请参阅Google中的受众计数以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未启用Experience Cloud ID服务中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀以启用ID同步。 如果您之前在Audience Manager中设置Google集成，则您设置的ID同步将结转到平台。

## 支持的身份{#supported-identities}

[!DNL Google Ad Manager] 支持下表所述身份的激活。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 当源标识为GAID命名空间时，选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 当源标识为IDFA命名空间时，选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，又名 [!DNL Device ID]。一个38位的数字设备ID，Audience Manager将它关联到它与之交互的每个设备。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)来目标加利福尼亚州的用户，并为所有其他用户使用Google Cookie ID。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID目标加州以外的用户。 |
| 里达 | 用于广告的Roku ID。 此ID可唯一标识Roku设备。 |  |
| MAID | Microsoft广告ID。 此ID可唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

## 导出类型{#export-type}

**区段导出**  — 您正在将区段(受众)的所有成员导出到Google目标。

## 先决条件

### 允许列表

>[!NOTE]
>
>在平台中设置第一个[!DNL Google Display & Video 360]目标之前，必须允许列表。 在创建目标之前，请确保Google已完成下面描述的允许列表过程。

在平台中创建[!DNL Google Display & Video 360]目标之前，您必须联系Google，要求在允许的Adobe提供者列表上添加允许列表，并将您的帐户添加到该。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在Google上的帐户ID。请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **客户ID** :这是Adobe的Google客户帐户ID。请联系Adobe客户服务或您的Adobe代表以获取此ID。
* **您的帐户类型**:使 **[!DNL Invite advertiser]** 用可仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌，或 **[!DNL Invite partner]** 允许将受众共享到您的Display &amp; Video 360帐户中的所有品牌。

## 配置目标

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择[!DNL Google Display & Video 360]，然后选择&#x200B;**[!UICONTROL Configure]**。

![连接Google Display和Video 360目标](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关[!UICONTROL Activate]和[!UICONTROL Configure]之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。

在创建目标工作流的&#x200B;**设置**&#x200B;步骤中，填写目标的[!UICONTROL Basic Information]以及应应用于此目标的营销操作。

![基本信息Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Name]**:填写此目标的首选名称。
* **[!UICONTROL Description]**: 可选. 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL Account Type]**:根据您在Google上的帐户，选择一个选项：
   * 使用`Invite Advertiser`可仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用`Invite Partner`允许将受众共享给您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL Account ID]**:使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。通常，这是一个六位或七位数字ID。
* **[!UICONTROL Marketing action]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>设置[!DNL Google Display & Video 360]目标时，请与您的[!DNL Google Account Manager]或Adobe代表一起了解您的帐户类型。

## 将区段激活到[!DNL Google Display & Video 360]

有关如何将区段激活到[!DNL Google Display & Video 360]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Display & Video 360]目标，请检查您的[!DNL Google Display & Video 360]帐户。 如果激活成功，则受众将填充到您的帐户中。