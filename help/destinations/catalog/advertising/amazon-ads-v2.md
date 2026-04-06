---
title: Amazon Ads v2
description: Amazon Ads v2提供了一系列选项，帮助您向注册销售商、供应商、图书供应商、Kindle Direct Publishing (KDP)作者、应用程序开发人员或代理商实现广告目标。 Amazon Ads v2与Adobe Experience Platform的集成提供了与Amazon Ads产品的统包集成。
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: 1e93c78b13159a2aed24d283e3768c670ad14097
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---

# Amazon Ads v2连接 {#amazon-ads-v2}

## 概述 {#overview}

[!DNL Amazon Ads v2]使广告商能够有效地摄取、管理、激活和重用[!DNL Amazon Ads]个产品中的受众数据。

>[!IMPORTANT]
>
>[!DNL Amazon Ads v2]是所有新[!DNL Amazon Ads]连接的当前目标。 如果您现有[（旧版） [!DNL Amazon Ads]](./amazon-ads.md)连接，则它将继续运行，而不需要任何更改。 [!DNL Amazon Ads v2]连接到[!DNL Ads Data Manager]，后者支持扩展身份类型、与地址相关的字段以及跨[!DNL Amazon Ads]产品的数据共享，与[（旧版） [!DNL Amazon Ads]](./amazon-ads.md)相比，提高了定位和受众匹配率。
>
>2026年4月底之后，[!DNL Amazon Ads v2]将重命名为[!DNL Amazon Ads]，旧卡将隐藏，并在目录中保留一个目标卡。 现有的旧数据流将继续工作，并且在该日期之后，您可以在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中管理它们。

与[!DNL Amazon Ads v2]的[!DNL Adobe Experience Platform]集成提供了将受众成员摄取到[!DNL Amazon Ads]的直接连接。 上传的受众可在[!DNL Ads Data Manager (ADM)]内的[!DNL Amazon Ads]控制台中使用。 您可以使用[!DNL Ads Data Manager]控制台在不同的[!DNL Amazon Ads]产品之间共享数据。

要了解有关[!DNL Ads Data Manager]的更多信息，请参阅：

* [广告数据管理器 — 控制台概述](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
* [使用广告数据管理器控制台](https://advertising.amazon.com/API/docs/en-us/adm/2_ads-data-manager-console)
* 广告数据管理器中的[帐户设置](https://advertising.amazon.com/API/docs/en-us/adm/2a_ads-data-manager_account_setup)

>[!IMPORTANT]
>
>此目标连接器和文档页面由&#x200B;*[!DNL Amazon Ads]*&#x200B;团队创建和维护。 如有任何查询或更新请求，请直接通过&#x200B;*`amc-support@amazon.com`.*&#x200B;与他们联系

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Amazon Ads v2]目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此目标解决的示例用例。

### Audience Ingestion and Activation {#activation-and-targeting}

运动服装品牌希望通过[!DNL Amazon Ads]中的相关广告触及其现有客户。 品牌可以将客户电子邮件地址从其CRM摄取到[!DNL Adobe Experience Platform]，使用其第一方离线数据构建受众，并通过[!DNL Amazon Ads]目标将这些受众激活到[!DNL Amazon Ads v2]。 激活后，您可以使用这些受众通过[!DNL Amazon Ads]库存向这些客户定位广告，帮助品牌重新吸引已知客户并促进重复购买。 若要了解详细信息，请参阅[管理数据](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data)。

## 先决条件 {#prerequisites}

若要使用[!DNL Amazon Ads v2]与[!DNL Adobe Experience Platform]的连接，您必须有权使用&#x200B;**[!DNL Amazon Ads Data Manager]**&#x200B;经理帐户[访问](https://advertising.amazon.com/help/G69CDSR9MNSWJH95)。 有关详细信息，请参阅[Amazon广告数据管理器入门](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)。

### 接受Amazon Ads Data Manager条款和条件 {#accept-terms}

在配置[!DNL Amazon Ads v2]目标之前，请登录到您的[!DNL Amazon Ads]帐户并接受[!DNL Ads Data Manager]条款和条件。 导航到[!DNL Ads Data Manager]中的[!DNL Amazon Ads]控制台，并在出现提示时接受条款。 如果不接受条款和条件，则不会在[!DNL Amazon Ads]中创建受众。

## 支持的身份 {#supported-identities}

[!DNL Amazon Ads v2]目标支持激活以下标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `phone` | 使用SHA256算法散列的电话号码 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `email` | 使用SHA256算法进行哈希处理的电子邮件地址（小写） | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `firstname` | 用户的名字 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希处理的名字。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `lastname` | 用户的姓氏 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希处理的姓氏。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `address` | 用户的街道地址 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希街道。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `city` | 用户的城市 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希城市。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `state` | 用户的省/市/自治区 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希状态。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `zip` | 用户的邮政编码 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希ZIP。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `countryCode` | 用户的国家/地区（2字符ISO代码） | 支持纯文本输入。 |
| `experianId` | 由[!DNL Experian]分配的标识符 | 支持纯文本输入。 |
| `kantarId` | 由[!DNL Kantar]分配的标识符 | 支持纯文本输入。 |
| `liveRampId` | 由[!DNL LiveRamp]分配的标识符 | 支持纯文本输入。 |
| `maId` | 移动应用程序分配的标识符 | 支持纯文本输入。 |
| `merkleId` | 由[!DNL Merkle]分配的标识符 | 支持纯文本输入。 |
| `neustarId` | 由[!DNL Neustar]分配的标识符 | 支持纯文本输入。 |
| `realId` | 由真实ID身份图分配的标识符 | 支持纯文本输入。 |
| `sambaTvId` | 由[!DNL Samba TV]分配的标识符 | 支持纯文本输入。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过[!DNL Experience Platform] [分段服务](/help/segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](/help/segmentation/ui/audience-portal.md#import-audience)，[!DNL Experience Platform]</li><li> 相似的受众， </li><li> 联合受众， </li><li> 在其他[!DNL Experience Platform]应用（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

下表描述了目标导出类型和频率。

| 项目 | 类型 | 注释 |
| ---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有[!DNL Amazon Ads]支持的标识符的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 [!DNL Experience Platform]中的受众更新将立即发送到[!DNL Ads Data Manager]。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](/help/destinations/ui/connect-destination.md)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Account name]**：输入有助于识别此目标帐户的名称。 如果您与同一个目标有多个连接，这个名称将特别有用。
* **[!UICONTROL Description]**（可选）：添加有助于您或您的团队区分帐户的详细信息，例如连接的目的或相关的业务上下文。

![在Experience Platform中为Amazon Ads连接到Destination对话框](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-connect-to-destination.png)

您将被重定向到[!DNL Amazon Ads v2]界面。 选择&#x200B;**[!UICONTROL Allow]**&#x200B;以登录到您的Amazon帐户。

![Amazon Ads OAuth授权提示询问用户是否允许](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-allow.png)

身份验证后，您将使用新连接重定向回[!DNL Adobe Experience Platform]。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

Experience Platform中的![Amazon Ads v2目标配置字段](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-configure-destination.png)

* **[!UICONTROL Name]**：用于识别此目标的名称。
* **[!UICONTROL Description]**：帮助您识别此目标的描述。
* **[!UICONTROL Manager Account]**：下拉列表中的目标管理器帐户ID。
* **[!UICONTROL All audience members sent to Amazon are consented for use for Advertising]**：指定数据使用的同意（`GRANTED`或`DENIED`）。
* **[!UICONTROL Ads data manager Terms & Conditions]**：接受[!DNL Amazon Ads]数据管理器条款和条件。 有关详细信息，请阅读[接受条款](#accept-terms)部分。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请阅读有关使用UI订阅目标警报[的指南](/help/destinations/ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出身份，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 强制映射 {#map}

[!DNL Amazon Ads v2]目标要求您配置以下映射才能成功激活数据。

| 源字段 | 目标字段 | 描述 |
|---------|----------|---------|
| `IdentityMap: Email_LC_SHA256` 或 `IdentityMap: Email` | `Identity: email` | 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `xdm: homeAddress.countryCode` | `Identity: countryCode` | 用户的国家/地区（2字符ISO代码） |

Amazon Ads v2目标的![标识字段映射配置](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-mapping.png)

### 映射最佳实践 {#mapping-best-practices}

将第一方标识符（如电话号码和地址）与合作伙伴提供的标识符相结合。 这允许[!DNL Amazon Ads]在受众匹配期间使用多个标识信号，从而提高匹配率。

仅在源数据中填充合作伙伴提供的标识符时才使用。 如果给定用户档案的映射合作伙伴标识符字段为空或不存在，则在受众匹配期间会忽略该字段，并且不会影响匹配率。

### 示例 {#examples}

* 激活使用`kantarId`身份数据构建或扩充的受众时，请使用[!DNL Kantar]。
* 当您的受众数据来自`merkleId`管理的标识解决方案时，请使用[!DNL Merkle]。
* 当您的数据通过`neustarId`身份解析链接时，请使用[!DNL Neustar]。
* 将`experianId`用于使用[!DNL Experian]身份数据扩充的受众。
* 激活依赖`liveRampId`身份解析的受众时使用[!DNL LiveRamp]。
* 使用`sambaTvId`提供的受众数据时，请使用[!DNL Samba TV]。

这些标识符通常由各自的合作伙伴以纯文本标识符的形式提供，并且不需要进行哈希处理。

## 验证数据导出 {#exported-data}

激活后，在&#x200B;**[!DNL Ads Data Manager]控制台**&#x200B;中验证受众摄取。

导航到&#x200B;**[!UICONTROL Audiences]** → **[!UICONTROL Uploaded Sources]**。 检查您的受众摄取状态、大小和任何错误日志。 [文档中的](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data)管理数据[和](https://advertising.amazon.com/API/docs/en-us/adm/7_adm-destinations)目标[!DNL Amazon Ads]页面提供了进一步的验证指导。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

有关[!DNL Amazon Ads Data Manager]的详细信息，请参阅以下资源：

* [Amazon广告数据管理器概述](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
