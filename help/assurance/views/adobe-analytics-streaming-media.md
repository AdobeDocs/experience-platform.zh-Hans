---
title: Assurance中的適用於流媒體的 Adobe Analytics檢視
description: 本指南說明如何搭配使用適用於流媒體的 Adobe Analytics與Adobe Experience Platform Assurance。
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# 在Assurance中檢視適用於流媒體的 Adobe Analytics

透過適用於流媒體的 Adobe Analytics與Adobe Experience Platform Assurance的整合，您現在可以在行動應用程式中驗證Media Analytics實施。 Media Analytics檢視會顯示媒體工作階段中追蹤的內容，例如：

- 工作階段開始事件，包含所有內容核心、標準中繼資料和自訂中繼資料屬性，以及工作階段結束和工作階段完成事件。
- 具有所有附加廣告屬性的廣告插播開始和廣告開始事件，以及兩者的略過和完成事件。
- 章節開始時會附加所有屬性，以及章節略過和章節完成事件。
- 所有播放變更事件（播放、暫停、緩衝、錯誤、位元速率變更）。
- 所有播放器狀態變更追蹤事件（開始、結束）。

在Analytics中處理資料後，後續處理的狀態和資料（例如媒體逗留時間和總暫停期間）也可在事件詳細資料檢視中使用。

## 快速入门

繼續之前，請確認您擁有下列服務：

- 此 [Adobe Experience Platform資料彙集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

若要瞭解如何在應用程式中安裝Assurance，請閱讀 [實作保證指南](../tutorials/implement-assurance.md).

## 透過適用於流媒體的 Adobe Analytics使用Assurance

在您連線並設定Adobe Analytics的應用程式後，就能為Streaming Media Analytics設定它了。 在左側面板底部，選取 **[!UICONTROL 設定]** 新增Media Analytics事件檢視和 **儲存** it.

![配置](./images/adobe-analytics-streaming-media/configure.png)

新增後，選取 **[!UICONTROL Media Analytics事件]** 在中檢視 **[!UICONTROL Adobe Analytics]** 區段來驗證工作階段追蹤。

![选择](./images/adobe-analytics-streaming-media/select.png)

在 **[!UICONTROL Media Analytics事件]** 檢視，您可以依工作階段ID (VSID)進行搜尋和篩選，以檢視特定的媒體工作階段。 若要檢視其他事件詳細資訊，請選取特定事件。

![媒体事件](./images/adobe-analytics-streaming-media/media-events.png)

如需更簡潔的API呼叫檢視，您也可以透過選取 **[!UICONTROL 隱藏播放點更新事件]** 篩選。

![隱藏播放點](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>檢視後續處理的媒體分析資料需要使用SDK版本： Android Media 2.1.2和iOS AEPMedia 3.0.1 （或以上版本）

若要檢視後續處理的資料，請尋找工作階段開始事件，並在狀態列中驗證工作階段已完成。 如果完成，請按一下事件以在事件詳細資料檢視中檢視媒體工作階段摘要。 如需詳細資訊，請向下捲動以尋找後續處理的詳細資訊。

![處理後檢視](./images/adobe-analytics-streaming-media/post-processed-view.png)
