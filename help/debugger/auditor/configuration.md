---
title: 設定測試參考
description: 瞭解Auditor功能如何測試Adobe Experience Platform Debugger中的設定。
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 67%

---

# 設定測試參考

此參考檔案主要探討Adobe Experience Platform Debugger的Auditor功能如何執行設定測試，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

配置测试会扫描实施中的特定设置、值，或者有无潜在冲突。Platform Auditor 会根据其他规则和推荐的最佳做法来评估标记。

| 测试 | 粗細 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud - 转化名称仅使用字母数字字符 | 3 | 此 `ev_conversion_property_name` 引數應僅包含數值和小數值，但 `ev_transid` 引數，可包含文字或數值。 查找 `everesttech.net` 像素，其中包含以 `ev_` _ 开头的 URL 参数。 | 确保事务属性参数仅包含数值和小数值。<br><br>警告：任何其他值类型都可能会导致数据丢失。 |
| Advertising Cloud - 转化名称使用 URL 安全字符 | 3 | 转化属性名称不应包含 &amp; 符号或问号。 | 确保事务属性参数不包含非编码的 &amp; 符号或问号。这会破坏 URL 格式。<br><br>警告：包含非編碼&amp;符號或問號的屬性引數(例如：  `ev_formComplete?=1` 或  `ev_formComplete&Submit=1`)，可能會導致資料遺失。 |
| Advertising Cloud - 已正确实施事务 ID | 1 | 屬性名稱  `ev_transid=` 不應空白。 | 屬性名稱  `ev_transid=` 不應保留為空白。 如果没有任何值，则可能会丢失事务数据。指派值給 `ev_transid=` 或從畫素中移除引數。 |
| Analytics - 在 DOM 中实例化 | 5 | 未安装或无法执行 Adobe Analytics 代码。在網頁上找不到Analytics程式碼時，會傳回0。 | 验证是否已在页面上实施 Analytics 标记，且没有遭到后续脚本活动的阻止。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |
| Analytics - 实例化一次 | 5 | 在页面上多次检测到 Adobe Analytics 代码。在網頁上找不到A-Analytics程式碼時，會傳回0。 | 确保页面上仅有一个 Analytics 标记。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) |
| Analytics - 最新版本 | 3 | 您的页面没有运行最新版本的 Analytics 代码库。为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。在網頁上找不到Analytics程式碼時，會傳回0。 | 安装最新版本的 Analytics 代码库。<br><br>[其他信息](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans) |
| Launch - DOM就緒後，以非同步方式載入第三方標籤 | 3 | 為了在良好的使用者體驗與收集正確資料之間取得平衡，應在DOM準備就緒時觸發第三方標籤。 这将可以确保执行相关的跟踪脚本，同时又不会影响站点的正常运转。 | 調整所有執行協力廠商畫素的規則，使其在DOM就緒時引發，即可解決此問題。<br><br>[其他信息](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID 服务 - 最新版本 | 2 | 您的页面没有运行最新版本的访客 ID 服务代码库 visitorAPI.js。为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 安装最新版本的访客 ID 服务代码库。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch - 最新版本 | 2 | 這些頁面未執行最新版本的標籤程式碼庫(Turbine)。 为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 重建並發佈標籤程式庫。<br><br>[其他信息](../../tags/quick-start/quick-start.md) |
| Target - 最新版本 | 2 | 您的页面没有运行最新版本的 Target 代码库。为了利用性能改进并提供最新功能，我们会不断地更新和调整旨在支持 Experience Cloud 技术的代码库。 | 安装最新版本的 Target 代码库。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault 先于 mboxCreate | 5 | mboxCreate 的正确用法类似于下面的示例：<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | 請務必包含  `<div class="mboxDefault"></div>` 標籤之前填入。 at.js 并不会为您添加此标记。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/) |
| Target - 有效的 DOCTYPE | 5 | 检测到无效的 DOCTYPE。在这种情况下，将不会触发 mbox。对于 at.js，DOCTYPE 必须处于“标准”模式，否则 Target 将无法正常运作。 | 更新页面上的 DOCTYPE。<br><br>[其他信息](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
