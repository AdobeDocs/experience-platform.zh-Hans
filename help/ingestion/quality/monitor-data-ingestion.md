---
keywords: Experience Platform；主页；热门话题；监控；监控；数据流；监控摄取；数据摄取；视图记录；视图批；
solution: Experience Platform
title: 监控数据摄取
topic-legacy: overview
description: 本用户指南提供了如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 6bedd5ec0865e858a337155deb80309a54e30892
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# 监控数据摄取

数据摄取允许您将数据摄取到Adobe Experience Platform。 您可以使用批处理摄取(允许您使用各种文件类型（如CSV）插入数据)或流摄取（允许您使用流端点将数据实时摄取到[!DNL Platform]）。

本用户指南提供了如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。

## 监控端对端数据流摄取

在[Experience PlatformUI](https://platform.adobe.com)中，选择左侧导航菜单中的&#x200B;**[!UICONTROL Monitoring]**，然后选择&#x200B;**[!UICONTROL Streaming end-to-end]**。

将显示&#x200B;**[!UICONTROL Streaming end-to-end]**&#x200B;监视页面。 此工作区提供一个图表，显示[!DNL Platform]接收流事件的速率，一个图表，显示[[!DNL Real-time Customer Profile]](../../profile/home.md)成功处理的流事件的速率，以及传入数据的详细列表。

![](../images/quality/monitor-data-flows/list-streams.png)

默认情况下，顶部图表显示过去七天的摄取率。 通过选择高亮显示的按钮，可以调整此日期范围以显示各种时间段。

![](../images/quality/monitor-data-flows/events-received.png)

下图显示了过去七天内[!DNL Profile]成功处理流事件的速率。 通过选择高亮显示的按钮，可以调整此日期范围以显示各种时间段。

>[!NOTE]
>
>要使数据显示在此图表上，数据必须为[!DNL Profile]启用显式&#x200B;**。**&#x200B;要了解如何为[!DNL Profile]启用流数据，请阅读[数据集用户指南](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

图形下方是所有流式摄取记录的列表，这些记录与上面显示的日期范围相对应。 每个列出的批次在上次更新时显示其ID、数据集名称、批次中的记录数以及错误数（如果有）。 您可以选择任何记录以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/streams.png)

### 查看流记录

查看成功流式传输记录的详细信息时，会显示诸如所摄取的记录数、文件大小、摄取开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失败的流记录的详细信息显示与成功记录相同的信息。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的记录提供了有关处理批时发生的错误的详细信息。 在以下示例中，转换或验证数据时发生了分析错误。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 监控批处理端对端数据获取

在[[!DNL Experience Platform UI]](https://platform.adobe.com)中，选择左侧导航菜单上的&#x200B;**[!UICONTROL Monitoring]**。

将显示&#x200B;**[!UICONTROL Batch end-to-end]**&#x200B;监视页，其中显示以前摄取的批的列表。 您可以选择任何批以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批

查看成功批处理的详细信息时，会显示所摄取的记录数、文件大小、摄取开始和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-batch.png)

失败批处理的详细信息显示与成功批处理相同的信息，添加失败的记录数。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的批次提供有关处理批次时发生的错误的详细信息。 在以下示例中，摄取的批次出错，因为它具有该人员的最大身份数。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
