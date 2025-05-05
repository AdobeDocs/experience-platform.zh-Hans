---
title: 章节详细信息报表数据类型
description: 了解章节详细信息报表Experience Data Model (XDM)数据类型。
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL 章节详细信息]报告数据类型

[!UICONTROL 章节详细信息]报表是一种标准的体验数据模型(XDM)数据类型，用于描述与媒体内容中的章节或区段相关的各种属性。 使用[!UICONTROL 章节详细信息]报表数据类型捕获章节名称、持续时间、位置、ID、播放状态（已开始/已完成）和每个章节逗留时间等详细信息。 媒体报告字段由Adobe服务用于分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。

![报告数据类型的章节详细信息图表。](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实现值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL 章节已完成]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-complete) | `isCompleted` | 布尔 | 章节是否已完成。 |
| [[!UICONTROL 章节ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter) | `ID` | 字符串 | 自动生成的章节ID。 |
| [[!UICONTROL 章节长度或持续时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-length) | `length` | 整数 | 章节的长度，以秒为单位。 |
| [[!UICONTROL 章节名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-name) | `friendlyName` | 字符串 | 章节和/或区段的名称。 |
| [[!UICONTROL 章节偏移]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-offset) | `offset` | 整数 | 内容中章节从开始起的偏移（以秒为单位）。 |
| [[!UICONTROL 章节位置]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-position) | `index` | 整数 | 章节在内容中的位置（索引、整数）。 |
| [[!UICONTROL 章节已开始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-start) | `isStarted` | 布尔 | 章节是否开始。 |
| [[!UICONTROL 已播放章节时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-time-spent) | `timePlayed` | 整数 | 章节花费的时间，以秒为单位。 |
