---
title: 警示測試參考
description: 瞭解Auditor功能如何在Adobe Experience Platform Debugger中測試警報。
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 34%

---

# 警示測試參考

此參考檔案主要探討Adobe Experience Platform Debugger的Auditor功能如何執行警示測試，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

警报会显示您应该注意的问题，但是不会影响您的得分。这些是推荐的最佳做法，在某些情况下可能不适用于您的实施。

| 测试 | 粗細 | 标准 | 推荐 |
| --- | --- | --- | --- |
| Advertising Cloud - 已实施正确的转化标记 | 0 | 检查是否使用了正确的转化标记。<br><br>**警告**：使用過時的TubeMogul轉換標籤可能會導致資料遺失。 | 将您的转化像素升级为新的 Advertising Cloud 纯图像转化标记。這項工作可以透過以下方式輕鬆完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已使用正确的 JS 标记 | 0 | Advertising Cloud應使用最新的JavaScript標籤。 | 将 Advertising Cloud JavaScript 升级到最新版本。使用已弃用的 JavaScript 版本可能会导致功能丧失。若要輕鬆完成這項工作，請使用 [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 纯图像标记 | 0 | Advertising Cloud 图像像素格式，应当与以下一种推荐的格式匹配： <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | 将您的 Advertising Cloud 像素升级为新的 Advertising Cloud 纯图像标记，这可以确保您能够充分利用 Advertising Cloud 的完整功能。這項工作可以透過以下方式輕鬆完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 已启用区段像素 DSP 同步 | 0 | 检查 TubeMogul 区段像素是否包含 DSP 同步设置，并推荐将该设置添加到这个像素中。DSP同步處理設定取決於查詢字串引數的使用。 總結： <ul><li>如果觸發標籤至下列任一專案：<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>而且標籤包含URL引數 `sid=`</li><li>然後檢視URL引數是否為 `cs=0` 或 `cs=1` 已存在，且若未推薦 `cs=1` 將新增至這些畫素，以便提高對象符合率。</li></ul> | 新增URL引數 `cs=1` 至您的Advertising Cloud畫素，以便進行DSP同步，進而提高對象匹配率。 這項工作最容易透過以下方式完成： [Advertising Cloud標籤擴充功能](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID 服务 - 仅使用一个 AdobeOrg | 0 | 在一般ECID實作中，應使用單一AdobeOrg。 | 验证这项实施中是否存在多个 AdobeOrg ID。<br><br>[其他信息](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| 啟動 —  `pageBottom` 回呼位置 | 0 | 此 `_satellite.pageBottom()` 函式必須存在，標籤才能運作。 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤以確保DTM可正常運作。 注意：最佳實務是讓該標籤成為 `<body>`. 若其位於 `<body>` 標籤時，此變數可能會正常運作，但由於這並非最佳實務，因此可能會無法正確運作，或產生非預期或不適當的結果。 | 在結尾的前面加上緊鄰的內嵌指令碼 `</body>` 標籤以確保DTM可正常運作。 <br><br>[其他信息](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 自托管 | 0 | 標籤程式庫在Adobe的Akamai執行個體上受到託管： `assets.adobedtm.com`. 自行託管是載入標籤的建議方法，因為此方法可讓您透過快取控制進一步掌控網站效能、減少對第三方指令碼的依賴，且更能掌握發佈程式。 您可以透過自己的網站託管或CDN來託管及管理標籤程式庫。 | 切換至自行託管，即是在頁面上載入標籤的方法。 尽管通过 Akamai CDN 来托管 的方法适用于大多数情况，但是，自托管方法可提升页面性能。<br><br>其他信息:<ul><li>[標籤快速入門手冊](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[异步部署](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 应当异步部署 | 0 | 標籤應以非同步方式部署，以發揮最佳效能。 | 包含 `async` 內嵌指令碼中的引數，以確保標籤功能正確 <br><br>[其他資訊](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target — 中的內容 `mboxDefault` | 0 | 內容應存在於中 `mboxDefault` 使用時 `at.js`. | 验证内容是否可用。<br><br>[其他信息](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
