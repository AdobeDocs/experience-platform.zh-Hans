---
title: Adobe Advertising DSP连接
description: 了解如何使用多种身份类型与Adobe Advertising Demand-Side Platform (DSP)共享经过身份验证和未经身份验证的第一方受众。
feature: Destinations
exl-id: 0ff80d38-993f-4609-bf2a-01a3e6cfe10b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 6%

---

# Adobe Advertising DSP连接

## 概述 {#overview}

Adobe Advertising Demand-Side Platform (DSP)目标允许用户与DSP帐户或帐户内的特定广告商共享经过身份验证的第一方受众和未经身份验证的第一方受众。

此目标允许客户与以下任何或所有ID共享第一方受众：

* 经过哈希处理的电子邮件ID，已转换为[!DNL LiveRamp RampID]或[!DNL Unified ID 2.0] (UID2.0)以便在DSP中定位

* Experience Cloud ID (ECID)和Adobe Advertising第三方Cookie

* 移动设备广告ID (MAID)：

   * [!DNL Google]台设备的[!DNL Android]个Advertising ID (GAID)

   * [!DNL Apple iOS]设备的广告商(IDFA)标识符

此连接取代了仅支持哈希电子邮件地址的[旧版Adobe Advertising Cloud DSP连接](adobe-advertising-cloud-dsp-connection-legacy.md)。

>[!IMPORTANT]
>
>此页面由Adobe Advertising [!DNL DSP]团队创建。 如有任何查询或更新请求，请直接通过`adcloud_support@adobe.com`联系Advertising支持部门。

## 用例 {#use-cases}

此目标允许广告商在具有Cookie和不具有Cookie的情况下跨浏览器访问其受众。

广告商可以选择与经过身份验证的第一方标识符（如[!DNL RampID]和[!DNL UID2.0]）或未经身份验证的ID（如Cookie和MAID）共享区段。

## 先决条件 {#prerequisites}

* 对于[!DNL RampID activation]、[!DNL DSP]帐户级别和营销活动级别的设置，启用与[!DNL LiveRamp RampID]的受众共享，这会将客户数据转换为[!DNL RampIDs]以创建目标区段。 您的Adobe客户团队将执行此配置。 [!DNL RampID]可通过[!DNL DSP]和[!DNL LiveRamp]之间的合作关系使用，您不需要自己的[!DNL LiveRamp]成员资格即可使用它。

* 受众ID：

   * 对于[!DNL RampID]和[!DNL UID2.0]，配置文件必须包含经过哈希处理的电子邮件ID。

   * 对于Cookie，请设置[!DNL Web SDK]数据流或[!DNL Experience Cloud ID Service]的Cookie同步进程。 请参阅下面的[设置ID同步以共享Cookie](#cookie-sync)。

   * 对于具有MAID的用户档案：

      * 对于每个GAID，在IdentityMap列中包含值`GAID`。

      * 对于每个IDFA，在IdentityMap列中包含值`IDFA`。

* Experience Platform帐户的Experience Cloud组织ID。 您可以在Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP])用户配置文件页面上找到您的ID。

* DSP[[!DNL Real-Time CDP] 中用于接收营销活动激活受众的](https://experienceleague.adobe.com/zh-hans/docs/advertising/dsp/audiences/sources/source-manage)源。 您的Adobe客户团队将使用您的Experience Cloud组织ID创建源。

* 在[!DNL DSP][[!DNL Real-Time CDP] 中创建 [!DNL DSP]源时生成的](https://experienceleague.adobe.com/zh-hans/docs/advertising/dsp/audiences/sources/source-manage)帐户或广告商的源密钥。 您的[!DNL DSP]帐户团队将与您共享此密钥。 您将在Experience Platform中使用它来创建与Advertising DSP目标的目标连接，如下所述。

### 设置ID同步以共享Cookie {#cookie-sync}

ID同步是共享第三方Cookie的先决条件。 使用[!DNL Web SDK]数据流或[!DNL Experience Cloud ID Service]设置Cookie同步进程。 有关第三方Cookie的标识处理的更多上下文，请参阅依赖于第三方Cookie集成的[Advertising目标](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations)。

**启用与[!DNL Web SDK]**&#x200B;同步的第三方ID

如果您使用的是[!DNL Experience Platform Web SDK]，请通过配置高级设置中的[!UICONTROL Third Party ID Sync]选项在数据流上启用第三方ID同步。 有关说明，请参阅数据流文档中的[配置高级选项](/help/datastreams/configure.md#advanced-options)。

**启用与[!DNL Experience Cloud ID Service]**&#x200B;同步的第三方ID

如果您将[!DNL Experience Platform]标记与[!DNL Experience Cloud ID Service]一起使用，请使用[Experience Cloud ID服务扩展](/help/tags/extensions/client/id-service/overview.md)配置第三方ID同步。 这样当您从[!DNL Real-Time CDP]激活受众时，特定ECID的匹配Adobe Advertising Cookie即可使用。

## 支持的身份 {#supported-identities}

Adobe Advertising DSP目标支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | 使用SHA256算法进行哈希处理的电子邮件地址 | Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使Experience Platform在激活时自动对数据进行哈希处理。 |
| `ECID` | 适用于Experience Cloud的第一方Cookie | 需要创建基于Cookie的区段。 |
| `adcloud` | 适用于Adobe Advertising的第三方Cookie | 需要创建基于Cookie的区段。 |
| `GAID` | [!DNL Android]设备标识 | 定位[!DNL Android]设备时需要。 |
| `IDFA` | [!DNL iOS]设备标识 | 定位[!DNL iOS]设备时需要。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
| -------------------- | --------- | ----------- | --------- |
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
| ---- | ---- | ----- |
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有所选标识符的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要具有Experience Platform的&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到目标，请按照说明，使用Experience Platform用户界面[创建目标连接](/help/destinations/ui/connect-destination.md)。 在目标配置工作流中，填写以下子部分中列出的字段。

### 验证目标 {#authenticate}

若要连接到目标，请在[!UICONTROL Connection type]部分提供以下参数，然后选择&#x200B;**[!UICONTROL Connect to destination]**：

* **[!UICONTROL Account or Advertiser Key]**：在DSP用户界面[!UICONTROL Source Key]中创建[[!DNL Real-Time CDP] 源时生成此](https://experienceleague.adobe.com/zh-hans/docs/advertising/dsp/audiences/sources/source-manage)。 您的Adobe客户团队将在创建源后与您共享此密钥。

![显示“帐户”或“广告商密钥”字段的连接类型部分的屏幕截图。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。

![目标详细信息字段屏幕截图，其中显示了“名称”和“说明”输入。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_adcloud_dsp"
>title="预配置映射集"
>abstract="我们已为您预配置以下两个映射集：ECID 和 [!DNL adcloud] Cookie。将数据激活到 Adobe Advertising DSP 时，符合激活受众条件的轮廓必须至少有一个与其轮廓相关联的 ECID 身份标识，才能成功导出到目标。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-platform/destinations/catalog/advertising/adobe-advertising-dsp-connection#preconfigured-mappings" text="了解有关预配置映射的更多信息"

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出身份，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

已部分预配置此目标的标识映射。 查看下面预配置的映射，并添加要包含的任何可选标识。

### 预配置映射 {#preconfigured-mappings}

在受众激活工作流期间，预配置并自动填充以下标识映射&#x200B;**：**

* **`ECID`** (Experience Cloud ID)
* **`adcloud`** （Adobe Advertising第三方Cookie）

![显示Cookie标识符、哈希电子邮件、IDFA和GAID选项的标识映射部分的屏幕截图。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

这些映射呈灰显状态且只读。 您无需在此步骤中配置任何内容。 您可以选择添加以下映射：

* **`email_lc_sha256`** （经过哈希处理的电子邮件）
* **IDFA** （[!DNL Apple iOS]设备ID）
* **GAID** （[!DNL Android]设备ID）

选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

>[!IMPORTANT]
>
>基于Cookie的导出需要&#x200B;**ECID才能成功。不带ECID的**&#x200B;配置文件将不会包含在基于Cookie的区段中。 对于使用[!DNL RampID]或[!DNL UID2.0]的经过身份验证的受众区段，配置文件必须包含经过哈希处理的电子邮件ID。

有关说明，请参阅[映射属性和身份](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)。

## 验证数据导出 {#exported-data}

要验证受众数据是否已与Adobe Advertising共享，请检查以下各项：

* [!DNL Real-Time CDP]目标中的数据流成功。

* 在DSP中，当您从&#x200B;**[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]**&#x200B;或从版面设置的&#x200B;**[!UICONTROL Audience Targeting]**&#x200B;部分创建或编辑受众时，该受众可用。 受众应显示在[!UICONTROL Adobe Segments]文件夹下的[!UICONTROL Real-Time CDP]选项卡中。

![DSP受众界面的屏幕截图，其中显示了[!DNL Real-Time CDP]文件夹，“Adobe区段”选项卡下列出了导入的受众区段。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
