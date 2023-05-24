---
title: BrightCove影片追蹤擴充功能概觀
description: 瞭解Adobe Experience Platform中的BrightCove影片追蹤標籤擴充功能。
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 37%

---

# BrightCove影片追蹤擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 先决条件

Adobe Experience Platform中的每個標籤屬性都需要在「擴充功能」畫面中安裝並設定下列擴充功能：

* Adobe Analytics
* Experience Cloud 访客 ID 服务
* 已安装的核心扩展

在影片播放器預計運行的每個網頁的HTML中，使用「頁面內嵌程式碼（進階）」程式碼片段。 「頁面內嵌程式碼（進階）」HTML片段可在以下網址找到： [Brightcove檔案](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). 以下連結提供以下專案的詳細資訊： [如何產生預覽和已發佈視訊播放器的內嵌程式碼](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

此1.1.0版擴充功能支援在單一網頁內嵌多個BrightCove影片。 如果有多個 `id` 進階內嵌標籤中的屬性，請確定每個屬性都有唯一值。 例如， `player1`， `player2`、等等。

>[!NOTE]
>
>在含有多個影片的頁面上，每個影片都使用在該頁面上執行的標籤規則中設定的相同設定。 例如，如果创建的规则规定在视频播放完 50% 时触发某个事件，则页面上的每个视频都将在 50% 提示点触发该规则。

如果在相關指令碼完全載入之前，使用此擴充功能的網頁與視訊互動，您可以採取兩個動作來修正問題。 首先，標籤程式庫可同步載入，其次，放置 `<script type="text/javascript">\_satellite.pageBottom();\</script\>` 元素嵌入頁面上的視訊之前。

請參閱 [BrightCove API檔案](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) 如需此擴充功能中所使用元件方法與事件的詳細資訊。

## 数据元素

该扩展中有七个可用的数据元素，这些数据元素都不需要进行配置。

* **播放點位置：** 在標籤規則中呼叫此資料元素時，它會以秒為單位記錄播放點在視訊時間軸上的位置。
* **视频帐户 ID：**&#x200B;此数据元素记录发布视频的 BrightCove 帐户 ID。
* **视频持续时间：**&#x200B;此数据元素记录视频内容的总持续时间（以秒为单位）。此外，可在 Analytics 内创建一个计算量度，将以秒为单位的数字转换为以分钟或小时为单位。
* **視訊廣告支援：** 此資料元素會指定視訊中是否支援廣告。
* **视频 ID：**&#x200B;此数据元素指定与视频关联的 BrightCove ID。
* **视频名称：**&#x200B;此数据元素指定视频的描述性或友好名称。
* **影片標籤：** 此資料元素會指定與視訊相關的特定指令碼。

## 事件

扩展中有七个可用事件，只有“自定义提示点跟踪”需要配置。

* **自定义提示点跟踪：**&#x200B;当视频达到指定的视频阈值百分比时，将触发此事件。例如，如果影片長度為60秒，而指定的提示點為50%，則事件會在30秒標籤處觸發。

>[!NOTE]
>
>请注意，每次达到此提示点时，都会触发此事件。例如，如果用户达到 50% 标记，在 50% 标记之前搜索视频，然后再次达到 50% 标记，则触发器将再次触发。

* **已完成影片：** 影片播放完畢時會觸發此事件。
* **視訊載入的中繼資料：** 播放器收到初始的長度和維度資訊時，就會觸發此事件。
* **视频暂停：**&#x200B;当视频暂停时，将触发此事件。
* **视频恢复：**&#x200B;在暂停事件后恢复视频内容时，将触发此事件。
* **視訊畫面變更：** 影片進入或退出全熒幕模式時，就會觸發此事件。
* **视频开始：**&#x200B;当视频内容首次启动时，将触发此事件。

## 使用情况

您可以為每個視訊事件（即上方列出的七個事件）設定一個標籤規則。 為您要追蹤的每個事件建立特定的標籤規則。 如果您不想追蹤事件，只需省略以為其建立規則即可。

规则包含三个操作：

1. 设置 Adobe Analytics 变量。（為上方列出的所有或部分資料元素建立資料元素。）
1. 发送 Adobe Analytics 信标。
1. 清除 Adobe Analytics 变量。

## 「影片開始」的標籤規則範例

需包括以下影片擴充功能物件：

* **事件**

   1. “视频开始”：此事件将在访客开始播放 BrightCove 视频时触发规则。

* **条件**

   1. None

* **操作**

   1. 在 Analytics“设置变量”操作中，设置：

      * **视频开始**&#x200B;事件（示例：event17）
      * 的prop/eVar **視訊名稱** 資料元素(範例：eVar10)
      * 的prop/eVar **視訊持續時間** 資料元素(範例：eVar11)
      * 的prop/eVar **目前的視訊位置** 資料元素(範例：eVar12)
   1. Analytics“发送信标”操作 (`s.tl`)
   1. Analytics“清除变量”操作


>[!TIP]
>
>若是不想為每個視訊元素布建多個eVar或prop，資料元素值會串連為替代方法。 接下來，系統會使用「分類規則產生器」工具將它們剖析為分類報表。 請參閱 [分類規則產生器工具](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) 說明檔案以取得詳細資訊。 最後，這些區段會套用為Analysis Workspace中的區段。
>
>若要這麼做，請建立「Video MetaData」之類的新資料元素，並將其設定為提取所有影片資料元素（如上所列），接著將其串連。

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
