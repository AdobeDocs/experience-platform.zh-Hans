---
title: Adobe Content Analytics扩展的发行说明
description: Adobe Experience Platform中的Content Analytics标记扩展的最新发行说明。
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 057d1ad8d61ed386a777175026a3f01f21541389
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Adobe Content Analytics扩展发行说明

以下是Content Analytics标记扩展的发行说明列表。

| 版本 | 日期 | 修复 |
|---|---|---|
| 1.0.52 | 2026年4月27日 | <ul><li>为CSS在DOM中元素的背景中加载图像的资产添加了跟踪。</li><li>添加了一个硬编码的`permanentlyBlockedURLs`数组，其中包含[maps.googleapis.com](https://maps.googleapis.com)和[mapsresources-pa.googleapis.com](https://mapsresources-pa.googleapis.com)。 默认情况下，Content Analytics库始终阻止这些URL。</li><li>已将`idSource`和`channel`字段添加到XDM数据收集请求。</li></ul> |
| 1.0.51 | 2026年3月13日 | <ul><li>修复了可能导致在页面之间导航时缓存`experienceIDs`的次要错误。</li><li>修复了Experience Querystring参数捕获的问题。 查询参数的功能如下所示：<ul><li>查询参数字段为空：体验ID中未捕获任何查询字符串参数。</li><li>查询参数是明确定义的（例如，1、2、3）：体验ID中仅捕获查询字符串参数和值。</li><li>查询参数设置为通配符(`.*`)：整个document.location.search字符串包含在URL中。</li></ul></li></ul> |
| 1.0.49 | 2025年9月12日 | <ul><li>修复了一个小错误，如果用户没有数据流权限，该错误会导致标记扩展UI完全无法加载。 UI现在将在&#x200B;**[!UICONTROL Choose from list]**&#x200B;数据流选项中显示权限警告，并且仍允许用户手动输入值。</li><li>更新了l10n的路径问题。</li><li>修复了属于非图像父元素的某些图像未正确捕获这些子图像元素的资产点击量的问题。</li><li>如果用户在`alloy`以外的其他实例名称的标记中配置了WebSDK，则Content Analytics库将检测WebSDK库的第一个实例，并使用它发送Content Analytics事件。</li></ul> |
| 1.0.48 | 2025年8月25日 | <ul><li>添加了对跟踪文档影子根DOM元素中资源的支持。</li></ul> |
| 1.0.47 | 2025年7月23日 | <ul><li>修复了未启用体验时发生的错误，该错误会导致体验的正则表达式检查失败。 此问题会导致无法收集Content Analytics数据。</li><li>解决了默认语言设置存在的一个问题，该问题导致无法向某些未在Experience Cloud中设置主要默认语言的用户显示标记UI。</li></ul> |
| 1.0.46 | 2025年6月18日 | <ul><li>在尝试保存扩展配置时添加了Toast通知（如果生产数据流不存在）。</li><li>通过改为将字符串化的有效负载内容置于控制台，临时修复了Content Analytics有效负载的可见性问题。</li><li>为扩展UI添加了本地化支持。</li><li>部分修复了导致扩展UI内容周围有额外填充的CSS问题。</li></ul> |
| 1.0.45 | 2025年4月14日 | <ul><li>解决了与等待页面查看事件时保留Content Analytics事件相关的配置设置中的几个错误。 默认情况下，Content Analytics现在会等待以触发事件，直到“首次页面查看”事件发生为止。</li></ul> |
| 1.0.44 | 2025年3月31日 | <ul><li>AppMeasurement集成的首次迭代。</li><li>此版本尚不支持筛选特定请求（例如，页面查看次数），但可以在以后的更新中添加此功能。 它当前使用在页面上找到的第一个AppMeasurement实例。</li></ul> |
| 1.0.43 | 2025年3月10日 | <ul><li>初始扩展版本。</li></ul> |
