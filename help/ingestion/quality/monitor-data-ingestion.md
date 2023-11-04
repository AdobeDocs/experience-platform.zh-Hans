---
keywords: Experience Platform；主页；热门主题；监测；监测；数据流；监测摄取；数据摄取；数据摄取；查看记录；查看批次；
solution: Experience Platform
title: 监控数据摄取
description: 本用户指南提供了有关如何在Adobe Experience Platform用户界面中监视数据的步骤。 本指南要求您拥有Adobe ID并有权访问Adobe Experience Platform。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 9399a242b855e151e5822035bc952efa89fe4bf0
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 4%

---

# 监控数据摄取

通过数据摄取，您可以将数据摄取到Adobe Experience Platform。 您可以使用批量摄取，这允许您使用各种文件类型（如CSV）插入数据；也可以使用流式摄取，这允许您将数据摄取到 [!DNL Platform] 实时使用流式端点。

本用户指南提供了有关如何在Adobe Experience Platform用户界面中监视数据的步骤。 本指南要求您拥有Adobe ID并有权访问Adobe Experience Platform。

## 监控流式处理端到端数据摄取 {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="摄取率"
>abstract="每秒成功处理的事件的数目。"
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html" text="在 UI 中监控源的数据流"

>[!TIP]
>
>要计算特定日期的总事件数，请使用以下表达式： `total events / day = ingestion rate * 60 * 60 * 24`.

在 [EXPERIENCE PLATFORMUI](https://platform.adobe.com)，选择 **[!UICONTROL 监控]** 左侧导航菜单，后面是 **[!UICONTROL 端到端的流式传输]**.

此 **[!UICONTROL 端到端的流式传输]** 此时会显示“监视”页面。 此工作区提供了一个图表，该图表显示接收流式事件的速率 [!DNL Platform]，该图显示了由成功处理的流式处理事件的速率 [[!DNL Real-Time Customer Profile]](../../profile/home.md)以及传入数据的详细列表。

![](../images/quality/monitor-data-flows/list-streams.png)

默认情况下，顶部图表显示过去七天的摄取速率。 通过选择高亮显示的按钮，可以调整此日期范围以显示各种时间段。

![](../images/quality/monitor-data-flows/events-received.png)

下面的图表显示按如下方式成功处理流式事件的速率 [!DNL Profile] 在过去七天里。 通过选择高亮显示的按钮，可以调整此日期范围以显示各种时间段。

>[!NOTE]
>
>为了让数据显示在此图表上，数据必须 **明确** 已启用 [!DNL Profile]. 了解如何为以下对象启用流数据 [!DNL Profile]，阅读 [数据集用户指南](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

图形下方是与上述日期范围对应的所有流摄取记录的列表。 每个列出的批次都会显示其ID、数据集名称、上次更新时间、批次中的记录数以及错误数（如果存在）。 您可以选择任何记录，以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/streams.png)

### 查看流记录

查看成功流式传输记录的详细信息时，会显示所摄取的记录数、文件大小以及摄取的开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失败的流记录的详细信息将显示与成功记录相同的信息。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败记录提供了有关处理批次时发生的错误的详细信息。 在下面的示例中，在转换或验证数据时发生了解析错误。

>[!NOTE]
>
>如果摄取的行中存在错误，则这些行将 **非** 将被丢弃，除非生成的消息导致无效的XDM。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 监控批量端到端数据摄取

在 [[!DNL Experience Platform UI]](https://platform.adobe.com)，选择 **[!UICONTROL 监控]** 左侧导航菜单上。

此 **[!UICONTROL 批次端到端]** 此时将显示“监视”页面，其中显示了先前摄取的批的列表。 您可以选择任何批次，以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批次

查看成功批次的详细信息时，会显示所摄取的记录数、文件大小以及摄取的开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-batch.png)

失败批次的详细信息显示与成功批次相同的信息，以及失败记录数的增加。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的批次会提供有关处理批次时发生的错误的详细信息。 在下面的示例中，摄取的批次出错，因为它具有最大数量的人员身份。

>[!NOTE]
>
>如果摄取的行中存在错误，则这些行将 **非** 将被丢弃，除非生成的消息导致无效的XDM。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
