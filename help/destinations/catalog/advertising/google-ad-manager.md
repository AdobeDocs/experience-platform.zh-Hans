---
keywords: google ad manager；google ad；doubleclick；DoubleClick AdX；DoubleClick；Google Ad Manager；Google广告管理器；DFP
title: Google Ad Manager连接
description: Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的一个广告投放平台，它使发布者能够通过视频和移动应用程序管理其网站上的广告显示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 2%

---

# [!DNL Google Ad Manager] 连接

## 概述 {#overview}

[!DNL Google Ad Manager]，以前称为 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]是一个广告服务平台，来自 [!DNL Google] 这使出版商能够通过视频和移动应用程序，管理其网站上广告的展示。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Google Ad Manager] 目标：

* 激活的受众以编程方式创建于 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的度量指标。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。
* 将受众映射到 [!DNL Google Ad Manager] 目标，则受众名称会立即显示在 [!DNL Google Ad Manager] 用户界面。
* 区段人口需要24-48小时才能显示在 [!DNL Google Ad Manager]. 此外，受众必须具有至少50个配置文件才能在中显示 [!DNL Google Ad Manager]. 大小小于50个配置文件的受众将不会填充到 [!DNL Google Ad Manager].

## 支持的标识 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 当源身份是GAID命名空间时，选择此目标身份。 |
| IDFA | [!DNL Apple ID for Advertisers] | 当源身份是IDFA命名空间时，选择此目标身份。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 38位数的数字设备ID，Audience Manager将其关联到与其交互的每个设备。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans) 定位加利福尼亚的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID定位加利福尼亚州以外的用户。 |
| RIDA | 适用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| MAID | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

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

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

如果您希望使用创建您的第一个目标 [!DNL Google Ad Manager] 且尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去(使用Audience Manager或其他应用程序)的Experience CloudID服务中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Google] Audience Manager中的集成，您设置的ID同步会转移到平台。

### 允许列表 {#allow-listing}

必须先将添加到允许列表，然后才能设置您的第一个 [!DNL Google Ad Manager] Platform的目标。 在创建目标之前，请确保完成如下所述的允许列表流程。

1. 请按照 [Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en) 将Adobe添加为链接的数据管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 界面，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用 **[!UICONTROL API访问]** 滑块。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="将受众ID附加到受众名称"
>abstract="选择此选项可使Google Ad Manager中的受众名称包含Experience Platform中的受众ID，如下所示： `Audience Name (Audience ID)`"

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 帐户ID]**：输入您的 [!DNL Audience Link ID] 来自您的 [!DNL Google] 帐户。 这是与您的关联的特定标识符 [!DNL Google Ad Manager] 网络(不是您的 [!DNL Network code])。 您可在下找到此内容 **[!UICONTROL 管理员>全局设置]** 在 [!DNL Google Ad Manager] 界面。
* **[!UICONTROL 帐户类型]**：根据您在Google中的帐户，选择一个选项：
   * 使用 `DFP by Google` 对象 [!DNL DoubleClick] 发布者
   * 使用 `AdX buyer` 对象 [!DNL Google AdX]
* **[!UICONTROL 将受众ID附加到受众名称]**：选择此选项可使Google Ad Manager中的受众名称包含Experience Platform中的受众ID，如下所示： `Audience Name (Audience ID)`.

>[!NOTE]
>
>设置时 [!DNL Google Ad Manager] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表，以了解您所拥有的客户类型。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Google Ad Manager] 目标，检查您的 [!DNL Google Ad Manager] 帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系Adobe或Google，请随时保留以下ID。

这些是Adobe的Google帐户ID：

* **[!UICONTROL 帐户ID]**： 87933855
* **[!UICONTROL 客户ID]**： 89690775