---
title: Marketo Measure Ultimate目标
description: 了解如何将数据连接和激活到Marketo Measure Ultimate目标。
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Marketo Measure Ultimate目标 {#mmu-destination}

## 概述 {#overview}

Marketo Measure（前身为Bizible）为营销人员提供了insight，在增加收入和最大化公司投资回报方面，营销人员可从中发挥最有效的营销工作。 Marketo Measure是一种营销归因解决方案，可自动跟踪和报告渠道效果，让您可见哪些渠道可带来最大的客户参与度，并允许您相应地优化营销支出。

目标允许企业到企业(B2B)数据从[!DNL Adobe Experience Platform]流到Marketo Measure。 此卡仅供Marketo Measure Ultimate客户使用。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用Marketo Measure目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此目标解决的示例用例。 此集成：

* 满足大型企业复杂的数据和性能报告要求。
* 在多个CRM和营销自动化系统中启用B2B归因报表。
* 便于引入第三方离线接触点数据。

## 先决条件 {#prerequisites}

请注意Marketo Measure目标的以下先决条件：

* 管理员应在Experience Platform设置页面中完成Marketo Measure沙盒映射。 如果没有沙盒映射，您将无法完成工作流以连接到目标保存和激活数据。
* 只能导出B2B XDM类的数据集（例如，请参阅XDM业务帐户和XDM业务机会类）。 无法为给定数据源引入同一B2B XDM类的多个数据集。
* 每个数据集只能包含在一个到Marketo Measure目标的数据流中。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 否 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 否 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 是 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Dataset export]** | 您正在导出未按受众兴趣或资格进行分组或构建的原始数据集。 阅读有关[数据集导出](/help/destinations/destination-types.md#dataset-export-destinations)的更多信息。 |
| 导出频率 | **[!UICONTROL Batch]** | 此批处理目标每两小时会将文件导出到Marketo Measure平台。 阅读有关[计划数据集导出](/help/destinations/ui/export-datasets.md#scheduling)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage and Activate Dataset Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写以下部分中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。

![Marketo Measure目标的“连接到目标”工作流。](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 将数据集导出到此目标 {#export-datasets}

>[!IMPORTANT]
>
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage and Activate Dataset Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将数据集导出到此目标的详细说明，请阅读[导出数据集](/help/destinations/ui/export-datasets.md)教程。

## 验证数据导出 {#exported-data}

要验证是否成功导出数据集，您可以检查数据集是否已成功导出到[Snowflake数据仓库](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=zh-Hans)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
