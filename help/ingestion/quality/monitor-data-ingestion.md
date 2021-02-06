---
keywords: Experience Platform；主题；主题；监控；监控；数据流；监控摄取；数据摄取；视图记录；视图批；
solution: Experience Platform
title: 监视数据摄取
topic: overview
description: 本用户指南提供如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# 监控数据摄取

数据摄取允许您将数据摄取到Adobe Experience Platform。 您可以使用批处理摄取，它允许您使用各种文件类型（如CSV）插入数据；或者使用流摄取，它允许您使用流端点实时将数据摄取到[!DNL Platform]。

本用户指南提供如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。

## 监控端到端的流数据摄取

在[Experience PlatformUI](https://platform.adobe.com)中，单击左侧导航菜单上的&#x200B;**[!UICONTROL 监视]**，然后单击&#x200B;**[!UICONTROL 端到端流]**。

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

将显示&#x200B;**[!UICONTROL 端到端流]**&#x200B;监视页面。 此工作区提供一个图表，显示[!DNL Platform]接收流事件的速率，一个图表，显示[[!DNL Real-time Customer Profile]](../../profile/home.md)成功处理的流事件的速率，以及传入数据的详细列表。

![](../images/quality/monitor-data-flows/list-streams.png)

默认情况下，顶部图表显示过去七天的摄取率。 单击高亮显示的按钮可调整此日期范围以显示不同时间段。

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

下图显示了过去七天内[!DNL Profile]成功处理流事件的速率。 单击高亮显示的按钮可调整此日期范围以显示不同时间段。

>[!NOTE]
>
>要使数据显示在此图上，数据必须为[!DNL Profile]显式&#x200B;**启用。**&#x200B;要了解如何为[!DNL Profile]启用流数据，请阅读[数据集用户指南](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

图形下面是所有流式摄取记录的列表，这些记录与上面显示的日期范围相对应。 每个列出的批次显示其ID、数据集名称（上次更新时）、批次中的记录数以及错误数（如果有）。 您可以单击任何记录以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### 查看流记录

在查看成功流式传输记录的详细信息时，会显示所摄取的记录数、文件大小、摄取开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

失败的流记录的详细信息显示与成功记录相同的信息。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的记录提供了有关处理批处理时出现的错误的详细信息。 在以下示例中，验证目录中的datasetId时出现系统错误。

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## 监控批量端对端数据获取

在[[!DNL Experience Platform UI]](https://platform.adobe.com)中，单击左侧导航菜单上的&#x200B;**[!UICONTROL 监视]**。

![](../images/quality/monitor-data-flows/click-monitoring.png)

出现&#x200B;**[!UICONTROL 批端到端]**&#x200B;监视页，显示先前摄取的批的列表。 您可以单击任何批以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/list-batches.png)

### 查看批

查看成功批的详细信息时，会显示所摄取的记录数、文件大小、摄取开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-batch.png)

失败批处理的详细信息显示与成功批处理相同的信息，添加失败的记录数。

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

此外，失败的批提供了有关处理批时出现的错误的详细信息。 在以下示例中，摄取的批次出错，因为它使用了未知字段`_experience`。

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)