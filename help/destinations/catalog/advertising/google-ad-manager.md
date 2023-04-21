---
keywords: Google Ad Manager;Google Ad;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager;DFP
title: Google Ad Manager连接
description: Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的一个广告服务平台，它为出版商提供了通过视频和移动设备应用程序管理其网站上广告显示的方法。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: ea480854c6058d84615b66a7df2d7c8fbd619bab
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 5%

---

# [!DNL Google Ad Manager] 连接

## 概述 {#overview}

[!DNL Google Ad Manager]，以前称为 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]，是 [!DNL Google] 这为出版商提供了通过视频和移动设备应用程序管理网站上广告显示的方法。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Ad Manager] 目标：

* 激活的受众是在 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。
* 在将区段映射到 [!DNL Google Ad Manager] 目标，区段名称会立即显示在 [!DNL Google Ad Manager] 用户界面。
* 区段人口需要24-48小时才能显示在 [!DNL Google Ad Manager]. 此外，区段的受众大小必须至少为50个用户档案，才能在 [!DNL Google Ad Manager]. 将不会在中填充受众大小小于50个用户档案的区段 [!DNL Google Ad Manager].

## 支持的标识 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 一个38位数的数字设备ID，Audience Manager会将其与之交互的每个设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans) 来定位加利福尼亚州的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 会使用此ID来定位加州以外的用户。 |
| RIDA | 用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您将区段（受众）的所有成员导出到Google目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

如果您希望通过 [!DNL Google Ad Manager] 尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Google] 集成时，您设置的ID同步会传递到Platform。

### 允许列表 {#allow-listing}

在设置第一个允许列表之前，必须将其添加到允许列表 [!DNL Google Ad Manager] 目标。 在创建目标之前，请确保完成下面描述的允许列表流程。

1. 按照 [Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en) 将Adobe添加为链接的数据管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 界面，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用 **[!UICONTROL API访问]** 滑块。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="将分段 ID 附加到分段名称"
>abstract="选择此选项可让 Google Ad Manager 中的区段名称包含来自 Experience Platform 的区段 ID，如下所示：`Segment Name (Segment ID)`"

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户ID]**:输入 [!DNL Audience Link ID] 从 [!DNL Google] 帐户。 这是与 [!DNL Google Ad Manager] 网络 [!DNL Network code])。 您可以在 **[!UICONTROL 管理员>全局设置]** 在 [!DNL Google Ad Manager] 界面。
* **[!UICONTROL 帐户类型]**:根据您使用Google的帐户选择一个选项：
   * 使用 `DFP by Google` 表示 [!DNL DoubleClick] （发布者）
   * 使用 `AdX buyer` 表示 [!DNL Google AdX]

<!--

*  **[!UICONTROL Append segment ID to segment name]**: Select this option to have the segment name in Google Ad Manager include the segment ID from Experience Platform, like this: `Segment Name (Segment ID)`

-->

>[!NOTE]
>
>设置 [!DNL Google Ad Manager] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表，了解您拥有的帐户类型。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Google Ad Manager] 目标位置，检查 [!DNL Google Ad Manager] 帐户。 如果激活成功，则帐户中会填充受众。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系到Adobe或Google，请保留以下ID。

这些是Adobe的Google帐户ID:

* **[!UICONTROL 帐户ID]**:87933855
* **[!UICONTROL 客户ID]**:89690775