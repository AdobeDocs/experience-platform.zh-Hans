---
title: 标记存在测试参考
description: 了解Auditor功能如何在Adobe Experience Platform Debugger中测试标记存在。
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 17%

---

# 标记存在测试参考

此参考可提供有关Adobe Experience Platform Debugger中的Auditor功能如何测试标记存在的更多信息。

>[!NOTE]
>
>有关Experience Platform Debugger中Auditor测试的更多信息，请参阅[Auditor功能概述](./overview.md)。

标记存在测试评估特定标记是否存在于页面上，以及它们在页面代码中的位置是否正确。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud — 代码存在 | 5 | DOM 中不提供 Advertising Cloud 标记。 | 使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)实施Advertising Cloud标记。 |
| Advertising Cloud — 已实施区段像素 | 5 | 将您的 Advertising Cloud 区段像素升级为新的 Advertising Cloud 纯图像标记。采用已弃用的 AMO 区段标记可能会导致数据丢失。 | 使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)实施Advertising Cloud区段像素。 |
| Analytics — 在DOM中加载 | 5 | 未检测到 Adobe Analytics 标记。 | 安装最新版本的Analytics。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Launch — 已加载库 | 5 | 在DOM中未找到`global _satellite`对象，这意味着未安装或无法执行标记库。 | 验证是否已在页面上实施标记库，且没有遭到后续脚本活动的阻止。 |
| Launch — 没有多个嵌入脚本 | 5 | 生产站点应当每页仅加载一个嵌入代码。 | 验证页面上是否只加载了生产库。 |
| 启动项 — `<body>`中存在`pageBottom`回调 | 5 | 在页面的`<body>`内未找到所需的`_satellite.pageBottom()`回调。 如果根本在页面上找不到`pageBottom`调用，或者如果它位于`<head>`标记中（或其他一些意外的位置），测试则会失败。 只有在`pageBottom`位于`<body>`标记内的某处时，测试才会通过。 | 为了确保标记正常运行，请在紧接着闭合的`</body>`标记之前添加内联脚本。<br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch — 异步部署时`pageBottom`回调不应存在 | 5 | 在页面上找到`_satellite.pageBottom()`回调，异步部署标记时不应出现这种情况。 | 删除`_satellite.pageBottom()`脚本以启用正确的标记功能。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID服务 — 代码存在 | 5 | 未找到 Experience Cloud ID 服务代码。强烈推荐使用Experience Cloud ID (ECID)，以确保您能够充分利用Experience Cloud解决方案，并且这对于跨Experience Cloud解决方案的ID管理至关重要。 | 安装最新版本的ECID。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans) |
| Experience Cloud ID服务 — Cookie存在 | 5 | 未找到`AMCV_` Cookie。 必须从`VisitorAPI.js`代码实例化一个访客对象。 | 如果这是标记实施，请验证AdobeOrg ID是否正确输入到ECID工具中。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID服务 — MID值存在 | 5 | 在`AMCV_` Cookie中未找到MID值。 | 再次测试以检查是否存在任何ECID API延迟。 如果这种情况持续存在，请联系Adobe客户关怀团队。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target — 代码存在 | 5 | Adobe Target应在DOM中定义。 | 安装最新版本的Target (at.js)。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - `<head>`中加载的库 | 4 | Target库应加载到`<head>`标记中。 | 检查以确保Target库已加载到`<head>`标记中。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
