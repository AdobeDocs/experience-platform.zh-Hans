---
keywords: 广告；必应；
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以在Microsoft展示广告中执行重新定位和面向受众的数字营销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 8%

---

# [!DNL Microsoft Bing] 连接 {#bing-destination}

## 概述 {#overview}

此 [!DNL Microsoft Bing] 目标可帮助您将配置文件数据发送到 [!DNL Microsoft Display Advertising].

要将配置文件数据发送到 [!DNL Microsoft Bing]，您必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用由构建的受众 [!DNL Microsoft Advertising IDs] 要通过显示广告定位用户，请执行以下操作 [!DNL Microsoft Advertising] 渠道。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Bing] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 |
|---|---|
| MAID | Microsoft广告ID |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可以导出到此目标的所有受众。

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表中描述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 从CSV文件引入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

**[!DNL Audience Export]**  — 您要将受众的所有成员导出到 [!DNL Microsoft Bing] 目标。

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您要将受众的所有成员导出到 [!DNL Microsoft Bing] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望使用创建您的第一个目标 [!DNL Microsoft Bing] 且尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去(使用Adobe Audience Manager或其他应用程序)的Experience CloudID服务中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Microsoft Bing] Audience Manager中的集成，您设置的ID同步会转移到平台。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]：这是您的 [!DNL Bing Ads CID]，采用整数格式。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 [!DNL Bing Ads Customer ID] (CID)。 您的CID是一个整数，在登录时可在URL中找到 [!DNL Microsoft Advertising].

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="映射 ID"
>abstract="输入要将所选区段映射到的数字 Bing 受众 ID。如果提供的[!UICONTROL 映射 ID] 未与 Bing 目标中的受众 ID 相对应，您将不会在 Bing 帐户中看到预期受众数据。"

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

在 [受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling) 步骤，您必须手动映射 [!UICONTROL 映射Id] 字段。 这可确保受众元数据正确传递到 [!DNL Bing].

![显示受众计划屏幕的UI图像，其中包含如何将受众名称映射到Bing映射ID的示例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Microsoft Bing] 目标，检查您的 [!DNL Microsoft Bing Ads] 帐户。 如果激活成功，则会在您的帐户中填充受众。
