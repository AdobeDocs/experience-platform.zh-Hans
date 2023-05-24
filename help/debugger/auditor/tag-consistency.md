---
title: 標籤一致性測試參考
description: 瞭解Auditor功能如何在Adobe Experience Platform Debugger中測試標籤一致性。
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 42%

---

# 標籤一致性測試參考

此參考檔案主要探討Adobe Experience Platform Debugger的Auditor功能如何測試標籤一致性，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

標籤一致性測試會在所有掃描的頁面上尋找不一致之處。 网站上所有页面中的这些值或配置应该是相同的，只有这样，才能确保数据收集是准确的。

| 测试 | 粗細 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Adobe Analytics — 一致的程式碼版本 | 5 | 找到多个版本的 Analytics 代码。 | 将 Analytics 的所有实例替换为当前版本。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |

{style="table-layout:auto"}
