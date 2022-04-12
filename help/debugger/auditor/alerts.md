---
title: 警报测试参考
description: 了解auditor如何在Adobe Experience Platform Debugger中测试警报。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 34%

---

# 警报测试参考

此参考可提供有关Adobe Experience Platform Debugger中的auditor功能如何运行警报测试的更多信息。

>[!NOTE]
>
>有关Platform Debugger中的auditor测试的更多信息，请参阅 [auditor功能概述](./overview.md).

警报会显示您应该注意的问题，但是不会影响您的得分。这些是推荐的最佳做法，在某些情况下可能不适用于您的实施。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud - 已实施正确的转化标记 | 0 | 检查是否使用了正确的转化标记。<br><br>**警告**:使用已弃用的TubeMogul转化标记可能会导致数据丢失。 | 将您的转化像素升级为新的 Advertising Cloud 纯图像转化标记。通过 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已使用正确的 JS 标记 | 0 | Advertising Cloud应使用最新的JavaScript标记。 | 将 Advertising Cloud JavaScript 升级到最新版本。使用已弃用的 JavaScript 版本可能会导致功能丧失。通过使用 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 纯图像标记 | 0 | Advertising Cloud 图像像素格式，应当与以下一种推荐的格式匹配： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 将您的 Advertising Cloud 像素升级为新的 Advertising Cloud 纯图像标记，这可以确保您能够充分利用 Advertising Cloud 的完整功能。通过 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已启用区段像素 DSP 同步 | 0 | 检查 TubeMogul 区段像素是否包含 DSP 同步设置，并推荐将该设置添加到这个像素中。“DSP同步”设置由查询字符串参数的使用决定。 总结如下： <ul><li>如果标记被触发到以下任一位置：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>且标记包含URL参数 `sid=`</li><li>然后，检查URL参数是否为 `cs=0` 或 `cs=1` 存在，如果不推荐，则 `cs=1` 添加到这些像素中，以便提高受众匹配率。</li></ul> | 添加URL参数 `cs=1` 到您的Advertising Cloud像素，以便能够进行DSP同步，从而提高受众匹配率。 通过 [Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID 服务 - 仅使用一个 AdobeOrg | 0 | 在常规的ECID实施中，应使用一个AdobeOrg。 | 验证这项实施中是否存在多个 AdobeOrg ID。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| 启动 —  `pageBottom` 回放 | 0 | 的 `_satellite.pageBottom()` 函数才能正常工作。 在紧接关闭之前添加内联脚本 `</body>` 标记来确保DTM正常运行。 注意：最佳做法是将该标记作为 `<body>`. 如果在 `<body>` 标记时，该函数可能会正常运行，但由于这不是最佳做法，因此可能会无法正确运行，或者会出现意外或不希望的结果。 | 在紧接关闭之前添加内联脚本 `</body>` 标记来确保DTM正常运行。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 自托管 | 0 | 标记库托管在Adobe的Akamai实例上( `assets.adobedtm.com`. 推荐采用自托管方法来加载标记，因为这种方法可通过缓存控制、减少第三方脚本依赖项以及增强对发布过程的控制，更好地控制网站的性能。 可以通过您自己的Web托管或CDN来托管和管理标记库。 | 切换到自托管是一种在页面上加载标记的方法。 尽管通过 Akamai CDN 来托管 的方法适用于大多数情况，但是，自托管方法可提升页面性能。<br><br>其他信息:<ul><li>[标记快速入门指南](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[异步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 应当异步部署 | 0 | 为了优化性能，应异步部署标记。 | 包括 `async` 参数来确保正常的标记功能 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target — 中的内容 `mboxDefault` | 0 | 内容应存在于 `mboxDefault` 使用 `at.js`. | 验证内容是否可用。<br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
