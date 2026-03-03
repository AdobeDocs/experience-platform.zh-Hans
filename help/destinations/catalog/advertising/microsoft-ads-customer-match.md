---
keywords: 广告；microsoft ads；客户匹配；
title: Microsoft Ads客户匹配连接
description: 使用Microsoft广告客户匹配目标按电子邮件地址匹配客户，并在Microsoft Advertising网络中重新与客户互动，包括搜索和受众广告。
badge: Beta 版
hide: true
hidefromtoc: true
source-git-commit: 6f246d87f44cd1fa9b22e40e9ee7b5d8250452e7
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 3%

---

# [!DNL Microsoft Ads Customer Match]连接 {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>此目标连接器当前处于受限可用性。 要获得访问权限，请联系您的Adobe代表。</br>

## 概述 {#overview}

使用[!DNL Microsoft Ads Customer Match]目标按电子邮件地址匹配客户，并在[!DNL Microsoft Advertising Network]中与客户重新互动，包括搜索和受众广告。 将您的[!DNL Microsoft Advertising]帐户关联到Real-Time CDP，以直接从Experience Platform自动创建和管理客户匹配列表。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用[!DNL Microsoft Ads Customer Match]目标，以下是Adobe Experience Platform客户可以使用此功能解决的示例用例。

### 用例#1

电子商务品牌希望通过[!DNL Microsoft Search]和[!DNL Microsoft Audience Network]联系现有客户，以根据优惠过去的购买和浏览历史记录对其进行个性化设置。 该品牌可以从自己的CRM中将电子邮件地址摄取到Experience Platform，从自己的离线数据构建受众，并将这些受众发送到[!DNL Microsoft Ads Customer Match]以在搜索和受众广告中使用，从而优化其广告支出。

### 用例#2

一家科技公司推出了一种新产品。 为了推广此新产品，他们希望提高以前购买过相关产品的客户的认识。 他们使用电子邮件地址作为标识符，将电子邮件地址从CRM数据库上传到Experience Platform。 根据拥有相关产品的客户创建受众。 这些受众将发送到[!DNL Microsoft Ads Customer Match]，以便公司可以跨[!DNL Microsoft Advertising Network]定位当前客户和类似客户。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Ads Customer Match]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `email` | 纯文本电子邮件地址 | [!DNL Microsoft Ads Customer Match]连接仅支持纯文本电子邮件地址。 Experience Platform会在导出时自动对电子邮件地址进行哈希处理，以符合Microsoft的要求。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 在其他Experience Platform应用程序(如Adobe Journey Optimizer)中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在Adobe Experience Platform数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有[!DNL Microsoft Ads Customer Match]目标中所用标识符（电子邮件地址）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要将受众数据发送到[!DNL Microsoft Ads]，您需要具有活动的[!DNL Microsoft Advertising]帐户。 有关创建帐户的详细信息，请访问[Microsoft Advertising文档](https://help.ads.microsoft.com/#apex/ads/en/53090/0)。

### 接受客户匹配条款和条件 {#accept-customer-match-terms}

在通过此目标激活受众之前，必须先在您的[!DNL Microsoft Advertising]帐户中手动创建客户匹配列表。 接受客户匹配条款和条件需要这种初始手动创建，这样可自动创建从Experience Platform发送的受众。 未能完成此步骤可能会导致激活受众时出错。

### 帐户配置 {#account-configuration}

配置目标时，必须提供以下信息：

* [!UICONTROL Customer ID]：您的[!DNL Microsoft Ads]客户ID (CID)，采用整数格式。 有关如何查找客户ID的说明，请参阅[Microsoft Advertising文档](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids)。
* [!UICONTROL Customer Account ID]：您的[!DNL Microsoft Ads]客户帐户ID。 有关如何查找客户帐户ID的说明，请参阅[Microsoft Advertising文档](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 填写目标详细信息 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Customer ID"
>abstract="您的Microsoft Advertising客户ID，也称为经理帐户ID。 这是Microsoft Advertising中可拥有多个广告商帐户（客户帐户ID）的顶级标识符。"
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="查找您的客户ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="客户帐户ID"
>abstract="您的Microsoft Advertising客户帐户ID，也称为广告商帐户ID。 这会标识您的客户ID下的特定广告商帐户。"
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="查找您的客户帐户ID"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="成员持续时间"
>abstract="用户在客户匹配列表中保留的天数。 接受的值介于1和390天之间。"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="客户匹配列表可用性"
>abstract="选择客户匹配列表是可用于单个广告商帐户，还是可用于经理帐户下的所有帐户。 选择客户ID以使该列表在您的客户ID下的所有广告商帐户中可用。 选择客户帐户ID以仅列出特定的客户帐户ID。"
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="详细了解Microsoft Advertising中的受众列表共享"

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Customer ID]**：您的[!DNL Microsoft Ads]客户ID (CID) 有关如何查找客户ID的说明，请参阅[Microsoft Advertising文档](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids)。
* **[!UICONTROL Customer Account ID]**：您的[!DNL Microsoft Ads]客户帐户ID。 有关如何查找客户帐户ID的说明，请参阅[Microsoft Advertising文档](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids)。
* **[!UICONTROL Membership Duration]**：用户在客户匹配列表中保留的天数。 接受的值介于1和390天之间。
* **[!UICONTROL Customer Match List Availability]**：选择客户匹配列表的可用性。 在[!DNL Microsoft Advertising]中，一个客户ID下可以有多个客户帐户ID（广告商帐户）。 选择&#x200B;**[!UICONTROL Customer ID (all advertising accounts)]**&#x200B;以使该列表在您的客户ID下的所有广告商帐户中可用，或选择&#x200B;**[!UICONTROL Customer Account ID (single advertising account)]**&#x200B;以将该列表限制为您在上面提供的特定客户帐户ID。 有关更多详细信息，请参阅[Microsoft Advertising文档](https://help.ads.microsoft.com/apex/index/3/en/56727)。

![Platform UI图像显示Microsoft Ads客户匹配目标的目标详细信息字段。](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要将&#x200B;*标识*&#x200B;导出到目标，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

### 映射 {#mapping}

在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，必须将源配置文件的电子邮件标识映射到[!DNL Microsoft Ads Customer Match]中的目标标识。

* **Source字段**：选择`IdentityMap: Email`作为源字段，以从用户档案映射电子邮件身份。 或者，您也可以选择XDM属性（如`personalEmail.address`）作为源字段。
* **目标字段**：选择`Identity: email`作为目标字段。

>[!IMPORTANT]
>
>必须使用未散列（纯文本）源字段。 请勿使用预哈希的源标识，如`Emails (SHA256, lowercased)`。 Experience Platform会在导出时自动对电子邮件地址进行哈希处理，以符合Microsoft的要求。

![UI图像显示了映射步骤，其中IdentityMap电子邮件映射到身份电子邮件。](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Ads Customer Match]目标，请检查您的[!DNL Microsoft Advertising]帐户。 如果激活成功，则会在您的帐户中填充受众作为客户匹配列表。

## 其他资源 {#additional-resources}

请参阅[Microsoft Advertising帮助中心](https://help.ads.microsoft.com/)以获取更多信息。
