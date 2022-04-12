---
title: 标记存在测试参考
description: 了解auditor如何在Adobe Experience Platform Debugger中测试标记存在的情况。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 34%

---

# 标记存在测试引用

此参考可提供有关Adobe Experience Platform Debugger中的auditor功能如何测试标记存在的更多信息。

>[!NOTE]
>
>有关Platform Debugger中的auditor测试的更多信息，请参阅 [auditor功能概述](./overview.md).

标记存在测试会评估页面上是否存在某些标记，以及这些标记在页面代码中的位置是否正确。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud - 代码存在 | 5 | DOM 中不提供 Advertising Cloud 标记。 | 使用实施Advertising Cloud标记 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已实施区段像素 | 5 | 将您的 Advertising Cloud 区段像素升级为新的 Advertising Cloud 纯图像标记。采用已弃用的 AMO 区段标记可能会导致数据丢失。 | 使用实施Advertising Cloud区段像素 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - 在 DOM 中加载 | 5 | 未检测到 Adobe Analytics 标记。 | 安装最新版本的 Analytics。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |
| Launch - 已加载库 | 5 | A `global _satellite` 在DOM中未找到对象，这表示未安装或无法执行标记库。 | 确认标记库已在页面上实施，且没有遭到后续脚本活动的阻止。 |
| Launch - 没有多个嵌入脚本 | 5 | 生产站点每页只应加载一个嵌入代码。 | 验证页面上是否只加载了生产库。 |
| 启动 —  `pageBottom` 回调存在于 `<body>` | 5 | 必需 `_satellite.pageBottom()` 在 `<body>` 页面的“隐藏主体”。 如果 `pageBottom` 调用在页面上根本找不到，或者如果它位于 `<head>` 标记（或其他一些意外的位置）。 只有在 `pageBottom` 在 `<body>` 标记。 | 在紧接关闭之前添加内联脚本 `</body>` 标记来确保正常的标记功能。<br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| 启动 —  `pageBottom` 异步部署时，不应存在回调 | 5 | 的 `_satellite.pageBottom()` 在页面上找到callback，异步部署标记时，不应该存在callback。 | 删除 `_satellite.pageBottom()` 脚本来启用正确的标记功能。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID 服务 - 代码存在 | 5 | 未找到 Experience Cloud ID 服务代码。强烈建议使用Experience CloudID(ECID)，以确保您能够从Experience Cloud解决方案中获得最大价值，并且这对于跨Experience Cloud解决方案的ID管理至关重要。 | 安装最新版本的ECID。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID 服务 - Cookie 存在 | 5 | 的 `AMCV_` 未找到cookie。 必须从 `VisitorAPI.js` 代码实例化一个访客对象。 | 如果这是标记实施，请确认AdobeOrg ID已正确输入到ECID工具中。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=zh-Hans) |
| Experience Cloud ID 服务 - MID 值存在 | 5 | 在 `AMCV_` cookie。 | 再次测试以检查是否存在任何ECID API延迟。 如果这种情况持续存在，请联系 Adobe 客户关怀团队。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - 代码存在 | 5 | Adobe Target应在DOM中定义。 | 安装最新版本的 Target (at.js)。<br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target — 库已加载到中 `<head>` | 4 | Target库应加载到 `<head>` 标记。 | 检查以确保Target库已加载到 `<head>` 标记。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
