---
title: YouTube影片追蹤擴充功能概觀
description: 瞭解Adobe Experience Platform中的YouTube影片追蹤標籤擴充功能。
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 40%

---

# YouTube影片追蹤擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

**先决条件**

Adobe Experience Platform中的每個標籤屬性都需要從「擴充功能」畫面安裝並設定下列擴充功能：

* Adobe Analytics
* Experience Cloud 访客 ID 服务
* 核心扩展

使用 [「使用\內嵌播放器&lt;iframe> 標籤」](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) 每個影片播放器要呈現的網頁的HTML中，Google開發人員檔案的程式碼片段。

此2.0.1版擴充功能可透過插入「 」，支援在同一網頁內嵌一或多部YouTube影片。 `id` iframe指令碼標籤中具有唯一值的屬性，並附加 `enablejsapi=1` 和 `rel=0` 到結尾 `src` 屬性值（若尚未包含）。 例如：

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

此擴充功能也可用來動態檢查唯一的ID屬性值，例如 `player1`，不論 `enablejsapi` 和 `rel` 查詢字串引數存在，而且其預期值是否正確。 因此，可以將YouTube指令碼標籤新增至網頁，無論是否使用 `id` 屬性以及是否 `enablejsapi` 和 `rel` 是否包含查詢字串引數。

>[!NOTE]
>
>在含有多個視訊的頁面上，每個視訊都使用在該頁面上執行的標籤規則中設定的相同設定。 例如，如果创建的规则规定在视频播放完 50% 时触发某个事件，则页面上的每个视频都将在 50% 提示点触发该规则。

擴充功能需仰賴下列邏輯來重寫iFrame：

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

因此，頁面載入後會出現輕微閃爍。 此行为是符合预期的。

## 数据元素

擴充功能中有6個可用的資料元素，且皆不需要設定。

* **播放點位置：** 當在標籤規則中呼叫播放點位置時，會以秒為單位記錄播放點在視訊時間軸上的位置。
* **视频 ID：**&#x200B;指定与视频关联的 YouTube ID。
* **视频名称：**&#x200B;指定视频的描述性或友好名称。
* **视频 URL：**&#x200B;返回当前已加载/正在播放视频的 YouTube.com URL。
* **视频持续时间：**&#x200B;记录视频内容的总持续时间（以秒为单位）。
* **擴充功能版本：** 此資料元素會記錄YouTube追蹤擴充功能版本，例如「Video Tracking_YouTube_2.0.0」。

## 事件

扩展中有八个可用事件，只有“自定义提示点跟踪”需要配置。

* **视频就绪：**&#x200B;提示并准备播放视频时触发。
* **视频开始：**&#x200B;视频首次开始播放，并且 `player.getCurrentTime() === 0` 时触发。
* **视频重播：**&#x200B;提示并在初始开始后重播视频时触发。此触发器将在每次重播视频时触发。
* **视频暂停：**&#x200B;视频暂停时触发。
* **视频恢复：**&#x200B;视频恢复，并且 `player.getCurrentTime() !== 0` 时触发。
* **自定义提示跟踪：**&#x200B;视频达到指定的视频阈值百分比时触发。例如，如果影片長度為60秒，而指定的提示點為50%，則播放點位置等於30秒時會觸發此事件。 提示点跟踪适用于初次播放和重播。請注意，如果使用者在提示點上尋找，則不會觸發事件。 唯有當播放點越過時間軸上計算的提示點位置，且視訊播放器正在播放時，才會觸發提示點事件。
* **视频缓冲：**&#x200B;当播放器在开始播放视频之前下载一定数量的数据时触发。
* **视频结束：**&#x200B;视频完全结束时触发。

## 使用情况

您可以為每個視訊事件（即上方列出的七個事件）設定一個標籤規則。 為您要追蹤的每個事件建立特定的標籤規則。 如果您不想追蹤事件，只需省略以為其建立規則即可。

规则包含三个操作：

* **设置变量：**&#x200B;设置 Adobe Analytics 变量（映射到所有或部分包含的数据元素）。
* **发送信标：**&#x200B;作为自定义链接跟踪调用发送 Adobe Analytics 信标，并提供“链接名称”值。
* **清除变量：**&#x200B;清除 Adobe Analytics 变量。

## 「影片開始」的標籤規則範例

需包括以下影片擴充功能物件。

* **事件**：「影片開始」(此事件會在訪客開始播放YouTube影片時觸發規則)。

* **条件**：无

* **操作**： 使用 **Analytics擴充功能** 至「設定變數」動作，對應：

   * 影片開始事件，
   * 视频持续时间数据元素的 prop/eVar
   * 视频 ID 数据元素的 prop/eVar
   * 视频名称数据元素的 prop/eVar
   * 视频 URL 数据元素的 prop/eVar

   接著，加入「傳送信標」動作(`s.tl`)，連結名稱為「影片開始」，接著會執行「清除變數」動作。

>[!TIP]
> 
>對於無法對每個視訊元素使用多個eVar或prop的實作，可在Platform中串連資料元素值，並使用「分類規則產生器」工具剖析為分類報表，如中所述 [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)，然後套用為Analysis Workspace中的區段。

要连接视频信息值，请创建一个名为“视频元数据”的新数据元素，然后对其进行编程，以拉入以上列出的所有视频数据元素并将它们组合在一起。例如：

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
