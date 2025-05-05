---
title: 章节详细信息收藏集数据类型
description: 了解章节详细信息收集Experience Data Model (XDM)数据类型。
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL 章节详细信息]收藏集数据类型

[!UICONTROL 章节详细信息]收藏集是标准的体验数据模型(XDM)数据类型，用于描述与媒体内容中的章节或区段相关的各种属性。 使用[!UICONTROL 章节详细信息]集合数据类型捕获章节名称、偏移、持续时间和章节索引等详细信息。 媒体收集字段会捕获数据并将其发送到其他Adobe服务以供进一步处理。

![章节详细信息集合数据类型的图表。](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实现值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL 章节长度或持续时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-length) | `length` | 整数 | 是 | 章节的长度，以秒为单位。 |
| [[!UICONTROL 章节名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-name) | `friendlyName` | 字符串 | 否 | 章节和/或区段的名称。 |
| [[!UICONTROL 章节偏移]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-offset) | `offset` | 整数 | 是 | 内容中章节从开始起的偏移（以秒为单位）。 |
| [[!UICONTROL 章节位置]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hans#chapter-position) | `index` | 整数 | 是 | 章节在内容中的位置（索引、整数）。 |

{style="table-layout:auto"}
