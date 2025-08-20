---
title: Adobe Content Analytics扩展的发行说明
description: Adobe Experience Platform中的Content Analytics标记扩展的最新发行说明。
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Adobe Content Analytics扩展发行说明

以下是Content Analytics标记扩展的发行说明列表。

| 版本 | 日期 | 修复 |
|---|---|---|
| <p>1.0.47</p> | <p>2025年7月23日</p> | <ul><li>修复了客户在未启用体验且体验的正则表达式检查失败时遇到的错误。 这会导致无法收集Content Analytics数据。</li><li>修复了导致某些用户在Experience Cloud中未设置其主要默认语言时无法显示标记UI的默认语言错误。</li></ul> |
| <p>1.0.46</p> | <p>2025年6月18日</p> | <ul><li>在尝试保存扩展配置时，如果生产数据流不存在，则添加toast通知。</li><li>临时修复了Content Analytics有效负载可见，但将简化的Content Analytics有效负载内容放入控制台中。</li><li>为扩展UI添加了本地化功能。</li><li>部分修复了扩展UI内容周围有额外填充的CSS问题。</li></ul> |
| <p>1.0.45</p> | <p>2025年4月14日</p> | <ul><li>解决了在等待页面查看事件时保留Content Analytics事件时的一些配置设置错误。 现在，默认情况下，Content Analytics将等待以触发事件，直到“首次页面查看”事件发生为止。</li></ul> |
| <p>1.0.44</p> | <p>2025年3月31日</p> | <ul><li>AppMeasurement集成的首次迭代。</li><li>此版本不支持对特定请求（例如页面查看次数）进行筛选，但可以稍后添加。  此方法还会使用在页面上找到的第一个AppMeasurement实例。</li></ul> |
| <p>1.0.43</p> | <p>2025年3月10日</p> | <ul><li>初始扩展版本。</li></ul> |

