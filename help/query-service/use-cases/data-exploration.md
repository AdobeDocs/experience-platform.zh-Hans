---
title: 使用SQL浏览、排除和验证批量摄取
description: 了解如何在Adobe Experience Platform中了解和管理数据摄取过程。 本文档包括如何验证批次和查询摄取的数据。
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# 使用SQL浏览、排除和验证批量摄取

本文档说明如何使用SQL验证和验证摄取的批次中的记录。 本文档教您如何：

- 访问数据集批次元数据
- 通过查询批处理排除故障并确保数据完整性

>[!NOTE]
>
>本指南中的某些屏幕截图取自[!DNL DBVisualizer]。 要了解如何[将查询服务与DBVisualizer](../clients/dbvisulaizer.md)或其他[第三方BI工具](../clients/overview.md)连接，请参阅链接的文档。

## 先决条件

为了帮助您了解本文档中讨论的概念，您应该了解以下主题：

- **数据摄取**：请参阅[数据摄取概述](../../ingestion/home.md)，了解将数据摄取到Experience Platform的基础知识，包括涉及的各种方法和流程。
- **批次摄取**：请参阅[批次摄取API概述](../../ingestion/batch-ingestion/overview.md)，了解批次摄取的基本概念。 具体而言，“批处理”是什么以及它在Experience Platform的数据摄取过程中如何发挥作用。
- **数据集中的系统元数据**：请参阅[目录服务概述](../../catalog/home.md)，了解如何使用系统元数据字段跟踪和查询摄取的数据。
- **体验数据模型(XDM)**：请参阅[架构UI概述](../../xdm/ui/overview.md)和架构组合的[&#39;基础知识&#39;](../../xdm/schema/composition.md)，了解XDM架构以及它们如何表示和验证摄取到Experience Platform的数据的结构和格式。

## 访问数据集批次元数据 {#access-dataset-batch-metadata}

要确保查询结果中包含系统列（元数据列），请在查询编辑器中使用SQL命令`set drop_system_columns=false`。 这会配置SQL查询会话的行为。 如果启动新会话，则必须重复此输入。

接下来，要查看数据集的系统字段，请执行SELECT all语句以显示数据集中的结果，例如`select * from movie_data`。 结果在右侧`_acp_system_metadata`和`_ACP_BATCHID`包含两个新列。 元数据列`_acp_system_metadata`和`_ACP_BATCHID`可帮助识别已摄取数据的逻辑分区和物理分区。

![显示并突出显示movie_data表及其元数据列的DBVisualizer UI。](../images/use-cases/movie_data-table-with-metadata-columns.png)

当数据被摄取到Experience Platform中时，会根据传入数据为其分配一个逻辑分区。 此逻辑分区由`_acp_system_metadata.sourceBatchId`表示。 此ID有助于在处理和存储数据批次之前对其进行逻辑分组和识别。

在处理数据并将其引入数据湖后，将为其分配一个由`_ACP_BATCHID`表示的物理分区。 此ID反映摄取的数据所在的数据湖中的实际存储分区。

### 使用SQL了解逻辑分区和物理分区 {#understand-partitions}

为了帮助了解数据在引入后如何分组和分发，请使用以下查询对每个逻辑分区(`_acp_system_metadata.sourceBatchId`)的不同物理分区(`_ACP_BATCHID`)的数量进行计数。

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

此查询的结果如下图所示。

![查询结果显示每个逻辑分区的不同物理分区数。](../images/use-cases/logical-and-physical-partition-count.png)

这些结果表明，输入批次的数量与输出批次的数量并不一定匹配，因为系统决定了将数据分批并存储在数据湖中的最有效方式。

在本例中，假定您已将CSV文件摄取到Experience Platform并创建了一个名为`drug_checkout_data`的数据集。

`drug_checkout_data`文件是35,000条记录的深度嵌套集。 使用SQL语句`SELECT * FROM drug_orders;`预览基于JSON的`drug_orders`数据集中的第一组记录。

下图显示了文件及其记录的预览。

![基于JSON的drug_orders数据集中的第一组记录预览。](../images/use-cases/drug-orders-preview.png)

### 使用SQL生成有关批处理摄取过程的见解 {#sql-insights-on-batch-ingestion}

使用下面的SQL语句深入分析数据摄取过程如何将输入记录分组并分批处理。

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

查询结果如下图所示。

![显示输入批次如何按记录计数一次进行掌握的分布的表。](../images/use-cases/distribution-of-input-batches.png)

结果表明，该方法能够快速有效地获取海量数据。 尽管创建了三个输入批次(每个输入批次包含2000、24000和9000条记录)，但在合并记录并消除重复项时，只保留了一个唯一批次。

>[!NOTE]
>
>数据集中可见的所有记录都是已成功摄取的记录。 成功的批量摄取并不意味着从源输入发送的所有记录都存在。 您必须检查数据摄取是否失败，以查找未在中获取数据的批次/记录。

## 使用SQL验证批处理 {#validate-a-batch-with-SQL}

接下来，使用SQL验证并验证已摄取到数据集中的记录。

>[!TIP]
>
>要检索批次ID并查询与该批次ID关联的记录，您必须首先在Experience Platform中创建批次。 如果您希望自己测试该过程，则可以将CSV数据摄取到Experience Platform。 阅读有关如何使用AI生成的推荐[&#128279;](../../ingestion/tutorials/map-csv/recommendations.md)将CSV文件映射到现有XDM架构的指南。

摄取批次后，您必须导航到将数据摄取到的数据集的[!UICONTROL 数据集活动选项卡]。

在Experience Platform UI中，在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以打开[!UICONTROL 数据集]仪表板。 接下来，从[!UICONTROL 浏览]选项卡中选择数据集的名称以访问[!UICONTROL 数据集活动]屏幕。

![左侧导航中突出显示了数据集的Experience Platform UI数据集仪表板。](../images/use-cases/datasets-workspace.png)

将显示[!UICONTROL 数据集活动]视图。 此视图包含选定数据集的详细信息。 它包括以表格式显示的任何摄取的批次。

从可用批次列表中选择一个批次，然后从右侧的详细信息面板中复制[!UICONTROL 批次ID]。

![Experience Platform数据集UI显示已摄取记录，批次ID突出显示。](../images/use-cases/batch-id.png)

接下来，使用以下查询检索作为该批次的一部分包含在数据集中的所有记录：

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

`_ACP_BATCHID`关键字用于筛选[!UICONTROL 批次ID]。

>[!TIP]
>
>如果要限制显示的行数，则`LIMIT`子句很有用，但更需要筛选条件。

在查询编辑器中执行此查询时，结果将被截断为100行。 查询编辑器专为快速预览和调查而设计。 要检索多达50,000行，可以使用第三方工具，如DBVisualizer或DBeaver。

## 后续步骤 {#next-steps}

通过阅读本文档，您已了解在数据摄取过程中验证和验证摄取批次中的记录的重要性。 此外，您还可以深入了解如何访问数据集批处理元数据、了解逻辑分区和物理分区以及使用SQL命令查询特定批处理。 此知识可帮助您确保数据完整性并优化Experience Platform上的数据存储。

接下来，您应该练习数据摄取，以应用所学到的概念。 使用提供的示例文件或您自己的数据将示例数据集摄取到Experience Platform中。 如果您尚未这样做，请阅读关于如何[将数据摄取到Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md)的教程。

或者，您可以学习如何[连接和验证查询服务以及各种桌面客户端应用程序](../clients/overview.md)，以增强您的数据分析功能。
