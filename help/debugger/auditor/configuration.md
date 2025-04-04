---
title: 配置测试参考
description: 了解Auditor功能如何测试Adobe Experience Platform Debugger中的配置。
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 50%

---

# 配置测试参考

此参考可提供有关Adobe Experience Platform Debugger中的Auditor功能如何运行配置测试的更多信息。

>[!NOTE]
>
>有关Experience Platform Debugger中Auditor测试的更多信息，请参阅[Auditor功能概述](./overview.md)。

配置测试会扫描实施中的特定设置、值，或者有无潜在冲突。Experience Platform Auditor会根据其他规则和建议的最佳实践来评估标记。

| 测试 | 粗细 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud — 转化名称仅使用字母数字字符 | 3 | 除`ev_transid`参数可以包含文本或数值外，`ev_conversion_property_name`参数应当只包含数值和小数值。 查找包含URL参数（以`ev_`开头）的`everesttech.net`像素。 | 确保事务属性参数仅包含数值和小数值。<br><br>警告：任何其他值类型都可能导致数据丢失。 |
| Advertising Cloud — 转化名称使用URL安全字符 | 3 | 转化属性名称不应包含 &amp; 符号或问号。 | 确保事务属性参数不包含非编码的 &amp; 符号或问号。这会破坏 URL 格式。<br><br>警告：包含非编码的&amp;符号或问号的属性参数（例如： `ev_formComplete?=1`或`ev_formComplete&Submit=1`）可能会导致数据丢失。 |
| Advertising Cloud — 已正确实施交易ID | 1 | 属性名称`ev_transid=`不应为空。 | 属性名称`ev_transid=`不应没有任何值。 如果没有任何值，则可能会丢失事务数据。为`ev_transid=`分配值或从像素中删除参数。 |
| Analytics — 在DOM中实例化 | 5 | 未安装或无法执行 Adobe Analytics 代码。在网页上找不到Analytics代码时，返回0。 | 验证是否已在页面上实施 Analytics 标记，且没有遭到后续脚本活动的阻止。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics — 实例化一次 | 5 | 在页面上多次检测到 Adobe Analytics 代码。在网页上找不到A-Analytics代码时返回0。 | 确保页面上仅有一个 Analytics 标记。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics — 最新版本 | 3 | 您的页面没有运行最新版本的 Analytics 代码库。为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。在网页上找不到Analytics代码时，返回0。 | 安装最新版本的 Analytics 代码库。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans) |
| Launch - DOM就绪后，异步加载第三方标记 | 3 | 为了在良好的用户体验与收集准确的数据之间取得平衡，应在DOM准备就绪时触发第三方标记。 这将可以确保执行相关的跟踪脚本，同时又不会影响站点的正常运转。 | 解决此问题的方法是：调整所有执行第三方像素的规则，使其在DOM就绪时触发。<br><br>[其他信息](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID服务 — 最新版本 | 2 | 您的页面没有运行最新版本的访客ID服务代码库visitorAPI.js。 为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 安装最新版本的访客 ID 服务代码库。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch — 最新版本 | 2 | 这些页面未运行最新版本的标记代码库(Turbine)。 为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 重建并发布标记库。<br><br>[其他信息](../../tags/quick-start/quick-start.md) |
| Target — 最新版本 | 2 | 您的页面没有运行最新版本的 Target 代码库。为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 安装最新版本的 Target 代码库。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault先于mboxCreate | 5 | mboxCreate的正确用法类似于下面的示例：<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | 调用mboxCreate()之前，请务必包含`<div class="mboxDefault"></div>`标记。 at.js 并不会为您添加此标记。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/) |
| Target — 有效的DOCTYPE | 5 | 检测到无效的 DOCTYPE。在这种情况下，将不会触发mbox。  对于 at.js，DOCTYPE 必须处于“标准”模式，否则 Target 将无法正常运作。 | 更新页面上的 DOCTYPE。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
