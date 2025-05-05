---
title: 标记一致性测试参考
description: 了解Auditor功能如何在Adobe Experience Platform Debugger中测试标记一致性。
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 38%

---

# 标记一致性测试参考

此参考可提供有关Adobe Experience Platform Debugger中的Auditor功能如何测试标记一致性的更多信息。

>[!NOTE]
>
>有关Experience Platform Debugger中Auditor测试的更多信息，请参阅[Auditor功能概述](./overview.md)。

标记一致性测试会查找所有扫描的页面中是否存在不一致的内容。 网站上所有页面中的这些值或配置应该是相同的，只有这样，才能确保数据收集是准确的。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Adobe Analytics — 一致的代码版本 | 5 | 找到多个版本的 Analytics 代码。 | 将 Analytics 的所有实例替换为当前版本。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |

{style="table-layout:auto"}
