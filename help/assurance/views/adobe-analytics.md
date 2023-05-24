---
title: Assurance中的Adobe Analytics檢視
description: 本指南說明如何搭配使用Adobe Analytics與Adobe Experience Platform Assurance。
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# 在Assurance中檢視Adobe Analytics

Adobe Experience Platform保證與Adobe Analytics的整合為使用者提供更豐富的SDK事件檢視，方便他們對Adobe Analytics實作進行偵錯和驗證。 檢視現在會顯示從傳送至Adobe Analytics的生命週期和動作/狀態事件。 [ADOBE EXPERIENCE PLATFORM SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). 此檢視還提供「回應」詳細資料，提供有關應用每個個別報表套裝的處理規則後如何處理事件的資訊。

![](./images/adobe-analytics/overview.png)

## 快速入门

繼續之前，請確認您擁有下列服務：

- 此 [Adobe Experience Platform資料彙集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

若要瞭解如何在應用程式中安裝Assurance，請閱讀 [實作保證指南](../tutorials/implement-assurance.md).

## 後處理狀態

SDK透過Adobe Analytics提出網路要求後，狀態會告訴您Assurance是否能夠擷取Adobe Analytics要求的後處理資訊。

請注意，為了擷取後處理資訊，登入使用者必須擁有對應報表套裝的存取權。

| 状态 | 描述 |
| :----- | :---------- |
| `Queued` | 網路要求正在擷取後處理資訊。 |
| `Processed` | 網路要求成功，並收到後續處理資訊。 |
| `Delayed` | 已超過擷取後處理資訊的重試次數上限。 |
| `Error` | 一個錯誤導致網路要求失敗。 有關錯誤的更多詳細資訊會顯示在事件詳細資料檢視中。 |
| `Unauthorized` | 使用者無權存取Adobe Analytics報表套裝。 |
| `Unavailable` | Adobe Analytics請求沒有對應的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 目前的Adobe Analytics或Assurance SDK版本可能不支援Analytics除錯功能。 如需詳細資訊，請閱讀 [疑難排解指南](../troubleshooting.md). |
| `Expired` | 此 `AnalyticsTrack` 或 `LifecycleStart` 事件超過24小時。 |

## 事件詳細資料檢視

對於Analytics追蹤事件，詳細檢視包含以下重要部分：

- 原始SDK Analytics請求事件。
- 請求的OOTB中繼和內容資料，例如報表套裝ID、SDK擴充功能版本、OOTB內容資料等。
- Analytics事件的後續處理資訊，包含revar、evar、prop等的對應。
