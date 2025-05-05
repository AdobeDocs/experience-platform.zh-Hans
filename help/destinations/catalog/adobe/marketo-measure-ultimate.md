---
title: Marketo Measure Ultimate目标
description: 了解如何将数据连接和激活到Marketo Measure Ultimate目标。
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---

# Marketo Measure Ultimate目标 {#mmu-destination}

## 概述 {#overview}

Marketo Measure（前身为Bizible）让营销人员能够洞悉哪些营销工作在为公司增加收入和最大化投资回报方面最有效。 Marketo Measure是一种营销归因解决方案，可自动跟踪和报告渠道效果，让您可见哪些渠道可带来最大的客户参与度，并允许您相应地优化营销支出。

该目标支持企业到企业(B2B)数据从Adobe Experience Platform流入Marketo Measure。 此卡仅供Marketo Measure Ultimate客户使用。

## 用例 {#use-cases}

为了帮助您更好地了解应当如何以及何时使用Marketo Measure目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。 此集成：

* 满足大型企业复杂的数据和性能报告要求。
* 在多个CRM和营销自动化系统中启用B2B归因报表。
* 便于引入第三方离线接触点数据。

## 先决条件 {#prerequisites}

请注意Marketo Measure目标的以下先决条件：

* 管理员应在Marketo Measure设置页面中完成Experience Platform沙盒映射。 如果没有沙盒映射，您将无法完成工作流以连接到目标保存和激活数据。
* 只能导出B2B XDM类的数据集（例如，请参阅XDM业务帐户和XDM业务机会类）。 无法为给定数据源引入同一B2B XDM类的多个数据集。
* 每个数据集只能包含在一个到Marketo Measure目标的数据流中。

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 数据集导出]** | 您正在导出未按受众兴趣或资格进行分组或构建的原始数据集。 阅读有关[数据集导出](/help/destinations/destination-types.md#dataset-export-destinations)的更多信息。 |
| 导出频率 | **[!UICONTROL 批次]** | 此批处理目标每两小时会将文件导出到Marketo Measure平台。 阅读有关[计划数据集导出](/help/destinations/ui/export-datasets.md#scheduling)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写以下部分中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

![Marketo Measure目标的“连接到目标”工作流。](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 将数据集导出到此目标 {#export-datasets}

>[!IMPORTANT]
> 
>要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将数据集导出到此目标的详细说明，请阅读[导出数据集](/help/destinations/ui/export-datasets.md)教程。

## 验证数据导出 {#exported-data}

要验证是否成功导出数据集，您可以检查数据集是否已成功导出到[Snowflake数据仓库](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=zh-Hans)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
