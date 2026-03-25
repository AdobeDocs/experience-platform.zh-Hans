---
title: FreeWheel连接
description: 了解如何将Adobe Experience Platform中的受众激活到FreeWheel，以便跨连接的电视、显示和视频库存进行程序化广告。
hide: true
hidefromtoc: true
badge: label="Beta 版" type="Informative"
exl-id: 1f1d3e57-a8ef-4971-b3d1-43521bd158bb
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 8%

---

# [!DNL FreeWheel]连接 {#freewheel}

>[!AVAILABILITY]
>
>[!DNL FreeWheel]目标当前位于Beta中，仅适用于选定客户。 要请求访问权限，请与 Adobe 代表联系。

## 概述 {#overview}

[!DNL FreeWheel]是一个全球广告技术平台，支持跨连接电视(CTV)、视频和显示内容库的程序化购买和销售。 [!DNL FreeWheel]提供了一个数据驱动型市场，可将全球广告商与高级媒体所有者连接起来。

使用此目标将受众从[!DNL Adobe Experience Platform]发送到[!DNL FreeWheel]。 受众作为每日批处理文件提供，并可用于在[!DNL FreeWheel]个交易和营销活动中定位。

## 先决条件 {#prerequisites}

在将受众激活到[!DNL FreeWheel]之前，请查看以下要求：

* **FreeWheel网络ID**：您必须具有有效的[!DNL FreeWheel]网络ID。 此服务由[!DNL FreeWheel]在设置帐户时提供。

## 支持的身份 {#supported-identities}

[!DNL FreeWheel]支持激活下表中描述的标识。 除了这些标识之外，您还可以使用[!DNL FreeWheel]帐户中可用的任何标识。 有关如何映射下表中未列出的标识的说明，请参阅[映射属性和标识](#map)。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `idfa` | 广告商的Apple ID | 当源身份是IDFA命名空间时，请选择此目标身份。 |
| `aaid` | ANDROID ADVERTISING ID | 当源身份是GAID命名空间时，请选择此目标身份。 |
| `ctv` | 已连接的电视设备ID | 定位CTV设备时选择此目标身份。 |
| `ip` | IPv4地址 | 选择此目标身份以根据用户的IP地址定位用户。 映射包含有效IPv4地址的配置文件属性，或使用计算字段派生值。 |
| `ipv6` | IPv6地址 | 选择此目标身份以根据用户的IPv6地址定位用户。 映射包含有效IPv6地址的配置文件属性，或使用计算字段派生值。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li>自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li>相似的受众，</li><li>联合受众，</li><li>其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众，</li><li>等等。</li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | CTV重定位、禁止访问 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出受众的所有成员，以及在[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的映射步骤中选择的所需标识字段。 |
| 导出频率 | **[!UICONTROL Batch]** | 第一次导出是符合激活受众条件的所有用户档案的完整快照。 后续导出是每日增量更新，包括新的受众资格（添加）和受众退出（删除）。 此外，还提供了一个可配置的完整受众刷新间隔（4、8或12周），除了每日增量之外，还会触发定期完整导出。 完整导出仅包含当前符合条件的用户档案。 不包括受众退出，仅通过每日增量更新提供。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

对[!DNL FreeWheel]目标的身份验证由Adobe自动处理。 在身份验证过程中，您不需要提供凭据或API密钥。 Adobe代表您管理与[!DNL FreeWheel]的安全连接。

![FreeWheel目标的身份验证步骤屏幕截图。](../../assets/catalog/advertising/freewheel/connect-destination.png)

选择&#x200B;**[!UICONTROL Connect to destination]**&#x200B;以继续执行目标详细信息步骤。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_freewheel_backfill"
>title="完整受众刷新间隔"
>abstract="选择除了每日增量更新外，将完整受众导出发送到[!DNL FreeWheel]的时间间隔。 完整的受众导出功能可防止您的受众成员在[!DNL FreeWheel]后过期，这样在营销活动运行时，就不会遇到目标成员数量下降的情况。 可用的选项为4周、8周和12周。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示如何填写FreeWheel目标详细信息的示例屏幕截图。](../../assets/catalog/advertising/freewheel/destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Region]**：您的帐户所在的[!DNL FreeWheel]区域。 选择以下选项之一：
   * **[!UICONTROL US East]**
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Asia Pacific]**
* **[!UICONTROL FreeWheel network ID]**：您的[!DNL FreeWheel]网络ID。 此值由[!DNL FreeWheel]提供，用于在[!DNL FreeWheel]平台中唯一标识您的组织。
* **[!UICONTROL Full audience refresh interval]**：除每日增量更新外，将完整受众导出发送到[!DNL FreeWheel]的频率。 完整的受众导出功能可防止您的受众成员在[!DNL FreeWheel]后过期，这样在营销活动运行时，就不会遇到目标成员数量下降的情况。 从下拉列表中选择一个时间间隔。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 计划受众导出 {#schedule}

![FreeWheel激活工作流中计划步骤的屏幕截图。](../../assets/catalog/advertising/freewheel/scheduling.png)

在&#x200B;**[!UICONTROL Scheduling]**&#x200B;步骤中，为每个受众配置导出计划。 [!DNL FreeWheel]使用混合导出模型：每个激活受众的第一个导出是完整快照，随后是每日增量更新。

配置以下字段：

* **[!UICONTROL File export options]**： **[!UICONTROL Export incremental files]**&#x200B;是预选的，是唯一受支持的选项。 第一次导出自动包括所有符合条件的配置文件的完整快照。 后续导出仅提供自上次导出以来的新受众资格和退出。
* **[!UICONTROL Frequency]**：选择&#x200B;**[!UICONTROL Daily]**。 [!DNL FreeWheel]需要每日增量文件投放。
* **[!UICONTROL Scheduled start time]**：以UTC格式输入运行每日导出的时间。
* **[!UICONTROL Date]**：设置激活的开始和结束日期。 开始日期决定发送第一个完整快照导出的时间。

>[!NOTE]
>
>完整导出（初始快照和定期完整刷新）仅包含当前符合条件的配置文件。 完全导出中不包含受众退出，并且仅通过每日增量更新提供。

### 映射属性和身份 {#map}

在映射步骤中，从Experience Platform配置文件中选择源字段，并将其映射到[!DNL FreeWheel]支持的身份类型。 至少需要一个映射。

>[!IMPORTANT]
>
>在映射UI中，[!DNL FreeWheel]支持的身份类型显示为&#x200B;**目标属性**，而不是身份命名空间。

如果[!DNL FreeWheel]帐户支持[支持的标识](#supported-identities)表中未列出的标识类型，则可以通过在目标字段中手动输入标识名称而不是从预定义列表中进行选择来映射到它们。

![屏幕截图显示在映射步骤中直接键入目标字段的自定义标识名称。](../../assets/catalog/advertising/freewheel/custom-identity.png)

以下是示例映射。 您的实际映射将取决于您的配置文件架构以及[!DNL FreeWheel]帐户支持的身份类型。

| 源字段 | 目标字段 |
| --- | --- |
| `identityMap.IDFA` | `idfa` |
| `identityMap.GAID` | `aaid` |
| `homeAddress.ipAddress` | `ip` |

{style="table-layout:auto"}

>[!NOTE]
>
>不强制执行任何强制映射。 但是，导出文件中不包括至少具有一个有效标识映射的配置文件。

## 导出的数据/验证数据导出 {#exported-data}

[!DNL FreeWheel]每次导出时接收两种类型的文件。 这两种文件类型都会自动生成和交付。 您无需执行任何操作。

**标识（数据）文件**&#x200B;包含受众成员资格数据。 每一行将用户标识符映射到一个或多个受众ID。 文件以CSV格式传送到[!DNL FreeWheel]，不带列标题。 为导出中存在的每个标识类型生成单独的文件（例如，`aaid`有一个文件，`idfa`有一个单独的文件）。

示例数据文件格式：

```csv
aebc1234-56f7-89ab-cdef-0123456789ab,segment_1,segment_2
f7c9a8b0-4d33-11ec-81d3-0242ac130003,segment_1,segment_3
123e4567-e89b-12d3-a456-426614174000,segment_2
```

**分类文件**&#x200B;描述了导出中包含的受众。 这些文件与数据文件一起提供，包括受众ID、名称和TTL（生存时间）（以天为单位）。 [!DNL FreeWheel]支持的最大TTL为90天。 以下示例中的值具有说明性。

分类文件格式示例：

```csv
Segment ID,Segment Name,TTL
segment_1,my_first_segment,30
segment_2,my_second_segment,30
segment_3,my_third_segment,30
```

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

有关[!DNL FreeWheel]及其广告技术平台的更多信息，请参阅[FreeWheel网站](https://www.freewheel.com){target="_blank"}。
