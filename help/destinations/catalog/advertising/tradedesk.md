---
keywords: 广告；交易台；广告交易台
title: 交易台连接
description: Trade Desk是一个自助服务平台，供广告购买者跨显示器、视频和移动库存源执行重定位和面向受众的数字活动。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 2%

---

# [!DNL The Trade Desk]连接

## 概述 {#overview}

使用此目标连接器将配置文件数据发送到[!DNL The Trade Desk]。 此连接器将数据发送到[!DNL The Trade Desk]第一方终结点。 Adobe Experience Platform与[!DNL The Trade Desk]之间的集成不支持将数据导出到[!DNL The Trade Desk]第三方端点。

[!DNL The Trade Desk]是一个自助服务平台，供广告购买者跨显示、视频和移动库存源执行重定位和面向受众的数字营销活动。

若要将配置文件数据发送到[!DNL The Trade Desk]，您必须先连接到目标，如本页的以下部分所述。

## 用例 {#use-cases}

作为营销人员，我希望能够使用基于[!DNL Trade Desk IDs]或设备ID构建的受众来创建重定位或面向受众的数字营销活动。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk]支持根据下表所示的标识激活受众。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

以下是[!DNL The Trade Desk]目标支持的标识。 这些标识可用于激活[!DNL The Trade Desk]的受众。

下表中的所有标识均已预配置，并在激活期间自动映射。 您无需在激活工作流中手动配置这些映射。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当配置文件上存在GAID时激活。 |
| IDFA | 广告商的Apple ID | 当配置文件上存在IDFA时激活。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请阅读以下有关[ECID](/help/identity-service/features/ecid.md)的文档。 |
| [!DNL Tradedesk] | [!DNL TDID]平台中的[!DNL The Trade Desk] | 当配置文件具有ECID且Experience Platform中存在ECID到交易台ID映射时激活。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在将受众的所有成员导出到目标。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

先决条件取决于您计划用于受众激活的身份类型：

**仅针对移动设备ID激活**，没有先决条件。 只要您收集和管理客户的ID（GAID和/或IDFA），就可以开始将受众激活到[!DNL The Trade Desk]。

**对于基于[!DNL The Trade Desk]**&#x200B;的Cookie定位，请确保在ECID和[!DNL Trade Desk ID]之间建立映射。 完成以下步骤以执行此操作：

1. **启用ID同步功能**：如果您是第一次设置[!DNL The Trade Desk ID]激活，并且以前未在Experience Cloud ID服务中启用[ID同步功能](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync)&#x200B;(使用Adobe Audience Manager或其他应用程序)，请与Adobe Consulting或客户关怀部门联系以启用ID同步。
   * 如果您之前在Audience Manager中设置了[!DNL The Trade Desk]集成，则您现有的ID同步会自动转移到Experience Platform。

2. **检测您的网页**：在您的网页上实施代码以创建[!DNL The Trade Desk ID]和Adobe ECID之间的映射。 这允许Experience Platform将交易台ID与客户配置文件相关联。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Account ID]**：您的[!DNL The Trade Desk] [!UICONTROL Account ID]。
* **[!UICONTROL Server Location]**：询问您的[!DNL The Trade Desk]代表您应该使用哪个区域服务器。 以下是可供您选择的可用区域服务器：

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[受众计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，必须手动将受众映射到目标平台中其对应的ID或友好名称。

在映射受众时，Adobe建议您使用Experience Platform受众名称或其更短的形式，以便轻松使用。 但是，目标中的受众ID或名称不需要与Experience Platform帐户中的受众ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

### 预配置的映射 {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="预配置的映射集"
>abstract="我们已为您预配置了这四个映射集。 当您向交易台激活数据时，符合激活受众资格的用户档案不一定需要在用户档案中存在全部四个标识，因为此目标将使用此处显示的任何目标标识。 <br>对于基于交易台ID的基于Cookie的定位，您需要配置文件中存在ECID，以及交易台ID与ECID之间的ID同步映射。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="阅读有关预配置映射的更多信息"

已预配置以下标识映射&#x200B;**，并在受众激活工作流中自动为您填充**：

* GAID (Google Advertising ID)
* IDFA (适用于广告商的Apple ID)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![显示必需映射的屏幕截图](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

这些映射呈灰显状态且只读。 您无需在此步骤中配置任何内容。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

Experience Platform会自动检查属于激活工作流中映射的受众的每个配置文件，以查看所有支持的身份类型，然后使用存在的任意身份激活配置文件。

### 按激活类型列出的身份要求

**移动ID激活(GAID/IDFA)：**&#x200B;只包含GAID或IDFA的配置文件足以激活。 无需其他身份或先决条件。

**基于Cookie的定位([!DNL Trade Desk ID])：**&#x200B;需要两者：

* 配置文件中存在ECID
* [!DNL Trade Desk ID]与ECID之间的ID同步映射（如[先决条件](#prerequisites)部分中所述，进行了配置）

**多个ID行为：**&#x200B;如果配置文件包含多个受支持的身份，则每个身份将分别激活到[!DNL The Trade Desk]。 这确保在受众激活中实现最大的覆盖范围和灵活性。

### 激活示例

* **移动设备ID配置文件：**&#x200B;具有GAID和/或IDFA的配置文件已使用其各自的广告ID激活。 如果配置文件同时包含GAID和IDFA，则将单独激活每个ID。
* **基于Cookie的配置文件：**&#x200B;将使用交易台ID激活具有ECID和相应[!DNL Trade Desk ID]映射的配置文件以进行基于Cookie的定位。
* **仅限ECID的配置文件：**&#x200B;仅具有ECID且没有[!DNL Trade Desk ID]映射的配置文件将&#x200B;**无法导出**。 仅ECID不足以激活。

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL The Trade Desk]目标，请检查您的[!DNL The Trade Desk]帐户。 如果激活成功，则会在您的帐户中填充受众。
