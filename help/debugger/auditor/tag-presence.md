---
title: 标记存在测试参考
description: 了解Auditor功能如何在Adobe Experience Platform Debugger中测试标记是否存在。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 33%

---

# 标记存在性测试参考

此参考可提供有关Adobe Experience Platform Debugger中的Auditor功能如何测试标记存在的更多信息。

>[!NOTE]
>
>有关Platform Debugger中Auditor测试的更多信息，请参阅 [auditor功能概述](./overview.md).

标记存在测试评估特定标记是否存在于页面上，以及它们在页面代码中的位置是否正确。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud - 代码存在 | 5 | DOM 中不提供 Advertising Cloud 标记。 | 使用实施Advertising Cloud标记 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已实施区段像素 | 5 | 将您的 Advertising Cloud 区段像素升级为新的 Advertising Cloud 纯图像标记。采用已弃用的 AMO 区段标记可能会导致数据丢失。 | 使用实施Advertising Cloud区段像素 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - 在 DOM 中加载 | 5 | 未检测到 Adobe Analytics 标记。 | 安装最新版本的 Analytics。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |
| Launch - 已加载库 | 5 | A `global _satellite` 在DOM中未找到对象，这意味着未安装标记库或无法执行标记库。 | 验证是否已在页面上实施标记库，且没有遭到后续脚本活动的阻止。 |
| Launch - 没有多个嵌入脚本 | 5 | 生产网站应仅为每个页面加载一个嵌入代码。 | 验证页面上是否只加载了生产库。 |
| 启动 —  `pageBottom` 回调存在于 `<body>` | 5 | 必需 `_satellite.pageBottom()` 在中未找到回调 `<body>` 页面的。 此测试在以下情况下失败： `pageBottom` 在页面上完全未找到调用，或者如果调用位于 `<head>` 标签（或其他一些意外的位置）。 只有在 `pageBottom` 在以下位置找到： `<body>` 标记之前。 | 在紧接着闭合的之前添加内联脚本 `</body>` 标记以确保标记正常运行。<br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| 启动 —  `pageBottom` 异步部署时不应存在回调 | 5 | 此 `_satellite.pageBottom()` 在页面上找到callback，但异步部署标记时不应出现这种情况。 | 删除 `_satellite.pageBottom()` 用于启用正确标记功能的脚本。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID 服务 - 代码存在 | 5 | 未找到 Experience Cloud ID 服务代码。强烈建议使用Experience CloudID (ECID)，以确保您能够充分利用Experience Cloud解决方案，并且这对于跨Experience Cloud解决方案的ID管理至关重要。 | 安装最新版本的ECID。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID 服务 - Cookie 存在 | 5 | 此 `AMCV_` 未找到Cookie。 必须从 `VisitorAPI.js` 代码实例化一个访客对象。 | 如果这是标记实施，请确认已在ECID工具中正确输入AdobeOrg ID。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=zh-Hans) |
| Experience Cloud ID 服务 - MID 值存在 | 5 | 在中找不到MID值 `AMCV_` Cookie。 | 再次测试以检查任何ECID API延迟。 如果这种情况持续存在，请联系 Adobe 客户关怀团队。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=zh-Hans) |
| Target - 代码存在 | 5 | Adobe Target应在DOM中定义。 | 安装最新版本的 Target (at.js)。<br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target — 库已加载到中 `<head>` | 4 | Target库应加载到 `<head>` 标记之前。 | 检查以确保Target库已加载到 `<head>` 标记之前。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
