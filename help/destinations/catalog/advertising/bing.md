---
keywords: 广告；必应；
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以在整个Microsoft Advertising网络（包括显示广告、搜索和原生）中执行重定位和面向受众的数字营销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 10%

---

# [!DNL Microsoft Bing]连接 {#bing-destination}

## 概述 {#overview}

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
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在将受众的所有成员导出到[!DNL Microsoft Bing]目标。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望使用[!DNL Microsoft Bing]创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Adobe Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=zh-Hans)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Microsoft Bing]集成，则您设置的ID同步将会转移到Experience Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]：这是整数格式的[!DNL Bing Ads CID]。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 填写目标详细信息 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL Bing Ads Customer ID] (CID)。 您的CID是一个整数，在您登录[!DNL Microsoft Advertising]时可在URL中找到。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="映射 ID"
>abstract="输入要将所选区段映射到的数值 Bing 受众 ID。如果提供的[!UICONTROL 映射 ID] 未与 Bing 目标中的受众 ID 相对应，您将不会在 Bing 帐户中看到预期受众数据。"

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，必须在[!UICONTROL 映射ID]字段中手动映射受众名称。 这可确保受众元数据正确传递到[!DNL Bing]。

![显示受众计划屏幕的UI图像，其中包含如何将受众名称映射到Bing映射ID的示例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Bing]目标，请检查您的[!DNL Microsoft Bing Ads]帐户。 如果激活成功，则会在您的帐户中填充受众。
