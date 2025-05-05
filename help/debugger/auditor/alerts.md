---
title: 警报测试参考
description: 了解Auditor功能如何在Adobe Experience Platform Debugger中测试警报。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 12%

---

# 警报测试参考

此参考可提供有关Adobe Experience Platform Debugger中的Auditor功能如何运行警报测试的更多信息。

>[!NOTE]
>
>有关Experience Platform Debugger中Auditor测试的更多信息，请参阅[Auditor功能概述](./overview.md)。

警报会显示您应该注意的问题，但是不会影响您的得分。这些是推荐的最佳做法，在某些情况下可能不适用于您的实施。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud — 已实施正确的转化标记 | 0 | 检查是否使用了正确的转化标记。<br><br>**警告**：使用已弃用的TubeMogul转换标记可能会导致数据丢失。 | 将您的转化像素升级为新的Advertising Cloud纯图像转化标记。 使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可以非常轻松地实现这一目标。 |
| Advertising Cloud — 已使用正确的JS标记 | 0 | Advertising Cloud应使用最新的JavaScript标记。 | 将 Advertising Cloud JavaScript 升级到最新版本。使用已弃用的JavaScript版本可能会导致功能丧失。 通过使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)，可以更轻松地实现这一目标。 |
| Advertising Cloud — 纯图像标记 | 0 | Advertising Cloud 图像像素格式，应当与以下一种推荐的格式匹配： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 将您的Advertising Cloud像素升级为新的Advertising Cloud纯图像标记，这可以确保您能够充分利用Advertising Cloud的完整功能。 使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可以非常轻松地实现这一目标。 |
| Advertising Cloud — 已启用区段像素DSP同步 | 0 | 检查TubeMogul区段像素是否包含DSP同步设置，并推荐将该设置添加到该像素。 DSP同步设置取决于查询字符串参数的使用。 总结一下： <ul><li>如果标记被触发到以下任意位置：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>标记包含URL参数`sid=`</li><li>然后检查URL参数`cs=0`或`cs=1`是否存在，如果不存在，则建议将`cs=1`添加到这些像素中，以便提高受众匹配率。</li></ul> | 将URL参数`cs=1`添加到您的Advertising Cloud像素中，以便可以实现DSP同步，从而增加受众匹配率。 使用[Advertising Cloud标记扩展](../../destinations/catalog/advertising/adobe-advertising-cloud.md)可以非常轻松地实现这一目标。 |
| Experience Cloud ID服务 — 仅使用一个AdobeOrg | 0 | 在正常实施ECID时，应使用单个AdobeOrg。 | 验证此实施是否存在多个AdobeOrg ID。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=zh-Hans) |
| 启动 — `pageBottom`回调位置 | 0 | 必须存在`_satellite.pageBottom()`函数才能使标记正常工作。 为了确保DTM正常运行，请在紧接着闭合的`</body>`标记之前添加内联脚本。 注意：最佳做法是将该标记作为`<body>`中的最后一个标记。 如果在`<body>`标记中找到了该函数，则表明存在正常运行的机率，然而由于这不是最佳的做法，所以可能会无法正确运行，或者会出现意外或不希望的结果。 | 为了确保DTM正常运行，请在紧接着闭合的`</body>`标记之前添加内联脚本。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch — 自托管 | 0 | 标记库托管在`assets.adobedtm.com`的Adobe Akamai实例上。 推荐采用自托管方法来加载标记，因为这种方法可通过缓存控制、减少第三方脚本依赖项以及增强对发布过程的控制，更好地控制网站的性能。 您可以通过自己的Web托管或CDN来托管标记库。 | 切换到自托管是在页面上加载标记的方法。 尽管通过Akamai CDN进行托管在多数情况下都是可行的，但自托管可以提升页面性能。 <br><br>其他信息：<ul><li>[标记快速入门指南](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[异步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch — 应当异步部署 | 0 | 标记应异步部署以实现最佳性能。 | 在内联脚本中包含`async`参数以确保标记功能正常<br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| 目标 — `mboxDefault`中的内容 | 0 | 使用`at.js`时`mboxDefault`中应有内容。 | 验证内容是否可用。 <br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=zh-Hans) |

{style="table-layout:auto"}
