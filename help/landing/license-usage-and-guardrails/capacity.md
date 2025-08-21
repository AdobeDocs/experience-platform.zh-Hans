---
title: 许可证使用量和容量
description: 了解Adobe Experience Platform中的许可证使用和容量限制。
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: d0b54e15f132d85964d6458da0769548d231a9c4
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 6%

---


# 许可证的使用和容量

>[!AVAILABILITY]
>
>要使用此功能，您必须具有以下权限：
>
>- **查看许可证使用情况仪表板**
>   - 此权限允许您&#x200B;**查看**&#x200B;容量主页。
>- **管理沙盒**
>   - 此权限允许您&#x200B;**编辑**&#x200B;您的容量分配。
>
>有关Experience Platform中权限的更多信息，请参阅[访问控制概述](/help/access-control/home.md#permissions)
>
>此外，如果您购买了“高吞吐量流式分段”，则&#x200B;**将**&#x200B;无法使用容量分配您的容量。 要更新您的功能，请联系Adobe客户关怀部门。

在Adobe Experience Platform中，功能可以让您知道您的组织是否超出了任何护栏，并为您提供有关如何修复这些问题的信息。

有关Experience Platform中护栏的更多信息，请阅读[Real-Time CDP护栏概述](../../rtcdp/guardrails/overview.md)。

## 容量行为 {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="流传输吞吐量"
>abstract="流传输吞吐量值衡量了在您所有生产和开发沙盒中流式摄入到轮廓服务的每秒综合峰值入站事件数。"

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="流传输受众数量"
>abstract="每个沙盒的最大流传输受众数量。此数字包括您沙盒中的边缘受众数量。"

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="边缘受众"
>abstract="每个沙盒的最大边缘受众数量。"

目前， Capacity支持以下服务：

- 流式客户细分
- 流式摄取

在这些服务中，将跟踪以下护栏：

- 流受众的最大数量为500
   - 在这500个流受众中，边缘受众的最大数量为150个
- 流式分段的最大组合吞吐量为每秒1500条记录(rps)

受众容量处于&#x200B;**沙盒**&#x200B;级别。 这意味着，对于您组织中的每个沙盒，您可以拥有500个流受众，其中150个可以是Edge受众。

吞吐量容量为&#x200B;**组织**&#x200B;级别，可以分发到您的各个沙盒。 例如，通过使用流分段吞吐量1500 rps，您可以将生产沙盒设置为1350 rps，将开发沙盒设置为150 rps。

Experience Platform以15分钟滚动间隔计算沙盒的吞吐量。 此吞吐量是实时测量的，每60秒刷新一次数据。

如果您的使用率达到许可容量的80%和90%，Experience Platform将发出警报，通知您已达到指定容量的最大值。 您可以修改设置以自定义接收警报的容量百分比或完全删除警报。

如果您的使用量超过许可容量的100%，则将被视为容量不足。 此时，您将会遇到性能延迟，并且您的服务级别目标(SLT)将&#x200B;**无法保证**。

## 访问 {#access}

要访问容量概述，请选择&#x200B;**[!UICONTROL 许可证使用情况]**，然后选择&#x200B;**[!UICONTROL 容量]**。

![访问“容量”部分的方法已突出显示。](/help/landing/images/capacity/access-capacity.png)

此时将显示“能力概览”页面，其中显示的信息包括预警历史记录以及组织能力的详细信息。

![“容量概述”页面已完整显示，其中显示警报历史记录和容量详细信息部分。](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### 警报历史记录 {#alert-history}

**[!UICONTROL 警报历史记录]**&#x200B;部分显示您组织内最近的容量违规列表。

![将显示警报历史记录部分。](/help/landing/images/capacity/alert-history.png)

| 列名 | 描述 |
| ----------- | ----------- |
| 沙盒 | 发生容量违规的沙盒的名称。 |
| 警报 | 沙盒中已被破坏的容量。 |
| 时间戳 | 违规发生的数据和时间。 |

要查看贵组织警报的完整历史记录，请选择![三个圆点图标](/help/images/icons/more.png)，然后选择&#x200B;**[!UICONTROL 查看全部]**。

![显示组织的完整警报历史记录。](/help/landing/images/capacity/full-alert-history.png)

### 产能详细信息 {#capacity-details}

能力详细信息部分概述了有关您组织能力的信息。 在此部分中，您可以按沙盒进行筛选并更改回顾时间段。

![将突出显示回顾期间的沙盒选择器和日期选择器。](/help/landing/images/capacity/filter-sandbox-and-date.png)

目前，它显示有关流吞吐量、流受众和Edge受众的容量信息。

#### 流传输吞吐量 {#streaming-throughput}

流吞吐量部分显示有关组织沙盒中的流吞吐量的信息。 流吞吐量值测量每秒合并的入站事件峰值，用于将摄取流式传输到配置文件服务。

![显示容量详细信息页面中的流吞吐量部分。](/help/landing/images/capacity/streaming-throughput-section.png)

| 列名 | 描述 |
| ----------- | ----------- |
| 沙盒 | 沙盒的名称。 |
| 服务 | 沙盒使用的服务。 目前，唯一支持的值是Profile。 |
| 使用情况（峰值） | 所选回顾时段内沙盒中数据的流吞吐量峰值。 |
| 容量 | 沙盒的最大流吞吐量峰值。 |
| 违规 | 如果发生违规，则为流吞吐量的违规类型。 |
| 建议的操作 | 描述缓解违规的建议操作的列。 |

您可以选择单个沙盒以查看沙盒流吞吐量的更详细视图。

![在流吞吐量部分中高亮显示了一个沙盒。](/help/landing/images/capacity/select-sandbox.png)

此时将显示“流吞吐量详细信息”页面。 您可以看到一个显示与容量限制相比的请求吞吐量的图形、沙盒及其吞吐量的列表以及用于分配组织容量的按钮。

![显示流吞吐量页面，显示有关所选沙盒的流吞吐量的详细信息。](/help/landing/images/capacity/streaming-capacity-allocation.png)

要更新组织的流吞吐量容量，请选择&#x200B;**[!UICONTROL 分配容量]**。

![流吞吐量详细信息页面中突出显示“分配容量”按钮。](/help/landing/images/capacity/select-allocate.png)

此时将显示分配页面。 在此页面上，您可以为不同的沙盒设置容量。 所有容量的总和&#x200B;**必须**&#x200B;等于组织的容量总计。

![显示容量分配页面。](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>您只能按&#x200B;**100**&#x200B;的顺序设置新容量。 例如，您可以将沙盒的新容量值设置为300或500，但您&#x200B;**不能**&#x200B;将此值设置为450。
>
>如果该值的顺序不是100，则会相应地向上或向下舍入。

更新容量分配后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成更新。 请注意，最多可能需要10分钟才能将更改反映在您的组织中。

#### 受众人数 {#audience-count}

**[!UICONTROL 流式受众数]**&#x200B;和&#x200B;**[!UICONTROL Edge受众数]**&#x200B;部分显示沙盒中流式受众和边缘受众的数量以及沙盒中允许的最大流式受众和边缘受众数量。

![将显示受众计数部分。](/help/landing/images/capacity/audience-count.png)

| 列名 | 描述 |
| ----------- | ----------- |
| 沙盒 | 沙盒的名称。 |
| 服务 | 用于沙盒的服务。 |
| 使用情况 | 沙盒中列出类型的受众数量。 |
| 容量 | 沙盒中允许的最大已列出类型受众数。 |

## 流吞吐量最佳实践 {#suggestions}

您可通过采用以下建议之一来解决流吞吐量违规问题：

1. 增加沙盒的分配容量。
2. 识别[监视仪表板](/help/dataflows/ui/monitor-streaming-profile.md)中的高吞吐量数据流，并根据需要对这些数据流应用限制或筛选。
3. 通过使用批量摄取以降低延迟用例来优化摄取。

此外，您可以查看数据流，看看是否可以优化数据策略。

| 促成因素 | 内容 | 对用例的影响 | 最佳实践 |
| --- | --- | --- | --- |
| 批量到流式转换 | 批量工作负载转换为流式传输会显着增加吞吐量，从而影响性能和资源分配。 例如，在没有速率限制的事件后执行批量配置文件更新。 | 当不需要低延迟处理时，无需对批量用例使用流策略。 | 评估用例要求。 对于批量出站营销，请考虑使用[批量摄取](/help/ingestion/batch-ingestion/overview.md)而不是流式处理来更有效地管理数据摄取。 |
| 不必要的数据摄取 | 引入个性化不需要的数据可在不增加价值的情况下增加吞吐量，从而浪费资源。 例如，无论相关性如何，都将所有Analytics流量摄取到用户档案中。 | 过多的不相关数据会产生噪音，使得识别有影响的数据点变得更困难。 在定义和管理受众和用户档案时，这也会造成摩擦。 | 仅摄取用例所需的数据。 确保过滤掉不必要的数据。<ul><li>**Adobe Analytics**：使用[行级筛选](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile)优化数据摄取。</li><li>**源**：使用[[!DNL Flow Service] API为支持的源（如](/help/sources/tutorials/api/filter.md)和[!DNL Snowflake]）筛选行级数据[!DNL Google BigQuery]。</li></li>**Edge数据流**：配置[动态数据流](/help/datastreams/configure-dynamic-datastream.md)以对来自WebSDK的流量执行行级筛选。</li></ul> |

## 常见问题解答 {#faq}

以下部分概述了有关Capacity功能的常见问题。

### 我的最大组合吞吐量限制总和能否小于目标最大值？

+++ 回答

不会。最大组合吞吐量限制&#x200B;**必须**&#x200B;总计为贵组织的护栏。

+++

### 如果超出最大容量，会发生什么情况？

+++ 回答

这取决于超出哪个容量。

目前，如果超出允许的最大受众数，过多的受众将不受影响。 但是，将来可能会限制创建新受众的能力。

如果超过流吞吐量，您将在摄取和分段中遇到性能延迟。

+++

### 为什么我应该遵循我的最大能力？

+++ 回答

在最大容量内工作可确保数据保持一致并保持数据完整性。

您可以确保在峰值事件期间保持一致的性能，避免可能会对系统性能产生负面影响并影响下游客户体验的技术问题，最终提高数据卫生和整体系统性能。

+++

### 管理流式分段吞吐量的最佳实践是什么？

+++ 回答

为了更好地管理流式分段吞吐量，您应该评估数据集，以确保它们优先考虑个性化所需的数据。


如果不需要实时处理，则应当使用批量摄取，而不是流式摄取。

+++
