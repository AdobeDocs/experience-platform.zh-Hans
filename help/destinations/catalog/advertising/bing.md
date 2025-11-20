---
keywords: 广告；必应；
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以在整个Microsoft Advertising网络（包括显示广告、搜索和原生）中执行重定位和面向受众的数字营销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 5%

---

# [!DNL Microsoft Bing]连接 {#bing-destination}

## 概述 {#overview}


>[!IMPORTANT]
>
>从2025年8月内部升级到目标服务后，您可能会遇到数据流中激活的配置文件数&#x200B;**降至**&#x200B;的情况。[!DNL Microsoft Bing]
>
> 导致此下降的原因是，针对此目标平台的所有激活引入了&#x200B;**ECID映射要求**。 有关详细信息，请参阅此页面中的[强制映射](#mandatory-mappings)部分。
>
>**更改内容：**
>
>* 现在，所有配置文件激活的ECID (Experience Cloud ID)映射都是&#x200B;**必需的**。
>* 没有ECID映射的配置文件将从现有激活数据流中&#x200B;**删除**。
>
>**您需要执行的操作：**
>
>* 查看您的受众数据，以确认用户档案具有有效的ECID值。
>* 监控您的激活量度以验证预期的配置文件计数。

使用[!DNL Microsoft Bing]目标将配置文件数据发送到整个[!DNL Microsoft Advertising Network]，包括[!DNL Display Advertising]、[!DNL Search]和[!DNL Native]。

[!DNL Microsoft Bing]目标在Microsoft中创建&#x200B;*[!DNL Custom Audiences]*。 这些内容在[!DNL Microsoft Search Network]和[!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic])中均可用，如[Microsoft Advertising文档](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500)中所列。

若要将配置文件数据发送到[!DNL Microsoft Bing]，您必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用[!DNL Microsoft Advertising IDs]构建的受众来通过[!DNL Microsoft Advertising]渠道中的显示或搜索广告定位用户。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Bing]支持根据下表所示的标识激活受众。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 身份标识 | 描述 |
|---|---|
| 女佣 | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud ID。 此身份是集成正常工作的必备条件，但不会用于受众激活。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

**[!DNL Audience Export]** — 您正在将受众的所有成员导出到[!DNL Microsoft Bing]目标。

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在将受众的所有成员导出到[!DNL Microsoft Bing]目标。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望使用[!DNL Microsoft Bing]创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Adobe Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Microsoft Bing]集成，则您设置的ID同步将会转移到Experience Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL Account ID]：这是以整数格式表示的[!DNL Bing Ads CID]。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 填写目标详细信息 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Account ID]**：您的[!DNL Bing Ads Customer ID] (CID)。 您的CID是一个整数，在您登录[!DNL Microsoft Advertising]时可在URL中找到。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="映射 ID"
>abstract="输入要将所选区段映射到的数值 Bing 受众 ID。如果提供的[!UICONTROL Mapping ID]与Bing目标中的受众ID不对应，则不会在Bing帐户中看到预期的受众数据。"

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，必须在[!UICONTROL Mapping ID]字段中手动映射受众名称。 这可确保受众元数据正确传递到[!DNL Bing]。

![显示受众计划屏幕的UI图像，其中包含如何将受众名称映射到Bing映射ID的示例。](../../assets/catalog/advertising/bing/mapping-id.png)

### 强制映射 {#mandatory-mappings}

[支持的标识](#supported-identities)部分中描述的所有目标标识都是必需的，必须在受众激活过程中映射。 这包括：

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

无法映射所有必需的标识，因而无法完成激活工作流。 每个标识在集成中均用于特定目的，而目标需要所有这些标识才能正常工作。

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Bing]目标，请检查您的[!DNL Microsoft Bing Ads]帐户。 如果激活成功，则会在您的帐户中填充受众。
