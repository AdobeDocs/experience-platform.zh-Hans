---
keywords: Experience Platform；主页；热门主题；监控；监控；数据流；监控摄取；数据摄取；数据摄取；查看记录；查看批次；
solution: Experience Platform
title: 监控数据摄取
topic-legacy: overview
description: 本用户指南提供了有关如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: 3fadf7006c8ea058e469067b61950ed2d2d12e3f
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 监控数据摄取

数据摄取允许您将数据摄取到Adobe Experience Platform。 您可以使用批量摄取(允许您使用各种文件类型（如CSV）插入数据)，或使用流式摄取（允许您使用流式端点将数据实时摄取到[!DNL Platform]）。

本用户指南提供了有关如何在Adobe Experience Platform用户界面中监控数据的步骤。 本指南要求您拥有Adobe ID并访问Adobe Experience Platform。

## 监控端到端数据流摄取

在[Experience PlatformUI](https://platform.adobe.com)中，选择左侧导航菜单中的&#x200B;**[!UICONTROL 监视]**，然后选择&#x200B;**[!UICONTROL 端到端流]**。

出现&#x200B;**[!UICONTROL 流端到端]**&#x200B;监控页面。 此工作区提供了一个图表，用于显示[!DNL Platform]接收的流式事件的速率，一个图表，用于显示[[!DNL Real-time Customer Profile]](../../profile/home.md)成功处理的流式事件的速率，以及传入数据的详细列表。

![](../images/quality/monitor-data-flows/list-streams.png)

默认情况下，顶部图表显示过去七天的摄取率。 通过选择突出显示的按钮，可以调整此日期范围以显示各种时间段。

![](../images/quality/monitor-data-flows/events-received.png)

下图显示了过去七天内[!DNL Profile]成功处理流式处理事件的速率。 通过选择突出显示的按钮，可以调整此日期范围以显示各种时间段。

>[!NOTE]
>
>要在此图表上显示数据，数据必须为[!DNL Profile]显式&#x200B;**启用。**&#x200B;要了解如何为[!DNL Profile]启用流数据，请阅读[数据集用户指南](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)。

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

图表下方是与上面显示的日期范围对应的所有流摄取记录的列表。 列出的每个批次都会显示其ID、数据集名称、上次更新时的数据集名称、该批次中的记录数以及错误数（如果有）。 您可以选择任何记录以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/streams.png)

### 查看流记录

在查看成功流式处理记录的详细信息时，会显示摄取的记录数、文件大小、摄取开始时间和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-streaming.png)

失败的流记录的详细信息显示与成功记录相同的信息。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的记录会提供有关处理批处理时发生的错误的详细信息。 在以下示例中，转换或验证数据时发生解析错误。

>[!NOTE]
>
>如果摄取的行中存在错误，则这些行将&#x200B;**不**&#x200B;被删除，除非生成的消息导致无效的XDM。

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## 监控批量端到端数据摄取

在[[!DNL Experience Platform UI]](https://platform.adobe.com)的左侧导航菜单中，选择&#x200B;**[!UICONTROL 监视]**。

此时会显示&#x200B;**[!UICONTROL 批量端到端]**&#x200B;监控页面，其中显示了先前摄取的批次的列表。 您可以选择任意批，以了解有关该记录的更多详细信息。

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### 查看批次

查看成功批的详细信息时，会显示摄取的记录数、文件大小、摄取开始时间和结束时间等信息。

![](../images/quality/monitor-data-flows/successful-batch.png)

失败批次的详细信息显示与成功批次相同的信息，并添加失败记录数。

![](../images/quality/monitor-data-flows/failed-batch.png)

此外，失败的批次会提供有关处理批次时发生的错误的详细信息。 在以下示例中，摄取的批次出错，因为它具有人员的最大身份数。

>[!NOTE]
>
>如果摄取的行中存在错误，则这些行将&#x200B;**不**&#x200B;被删除，除非生成的消息导致无效的XDM。

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
