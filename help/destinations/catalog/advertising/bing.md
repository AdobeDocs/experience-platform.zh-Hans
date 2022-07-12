---
keywords: '广告；bing; '
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以跨Microsoft显示广告执行重定位和受众定位的数字促销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 812688043a7da943832b5798de0f433928634998
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# [!DNL Microsoft Bing] 连接 {#bing-destination}

## 概述 {#overview}

的 [!DNL Microsoft Bing] 目标可帮助您将用户档案数据发送到 [!DNL Microsoft Display Advertising].

将用户档案数据发送到 [!DNL Microsoft Bing]，则必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用 [!DNL Microsoft Advertising IDs] 通过 [!DNL Microsoft Advertising] 渠道。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Bing] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 |
|---|---|
| 女佣 | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

**[!DNL Segment Export]**  — 将区段（受众）的所有成员导出到 [!DNL Microsoft Bing] 目标。

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要将区段（受众）的所有成员导出到 [!DNL Microsoft Bing] 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望通过 [!DNL Microsoft Bing] 尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Adobe Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Microsoft Bing] 集成时，您设置的ID同步会传递到Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]:这是您的 [!DNL Bing Ads CID]，格式为整数。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID].

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="映射ID"
>abstract="输入要将选定区段映射到的Bing区段ID数字。 如果提供 [!UICONTROL 映射ID] 与Bing目标中的区段ID不对应，您将在Bing帐户中看不到预期的受众数据。"

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

在 [区段计划](../../ui/activate-segment-streaming-destinations.md#scheduling) 步骤中，您必须在 [!DNL Bing] 目标。 填写从 [!DNL Bing] 在 [!UICONTROL 映射ID] 字段。

![显示区段映射屏幕的UI图像（以Bing映射ID为例）](../../assets/catalog/advertising/bing/mapping-id.png)

如果提供 [!UICONTROL 映射ID] 与Bing目标中的区段ID不对应，您将在Bing帐户中看不到预期的受众数据。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Microsoft Bing] 目标位置，检查 [!DNL Microsoft Bing Ads] 帐户。 如果激活成功，则帐户中会填充受众。
