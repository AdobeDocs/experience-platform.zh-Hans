---
keywords: Experience Platform；產品推薦配方；資料科學工作區；熱門主題；配方；預先建置配方
solution: Experience Platform
title: 產品推薦配方
description: 產品Recommendations配方可讓您根據客戶的需求和興趣量身打造個人化產品推薦。 有了準確的預測模型，客戶的購買記錄就能讓您深入瞭解他們可能會對哪些產品感興趣。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# 產品推薦配方

產品Recommendations配方可讓您根據客戶的需求和興趣量身打造個人化產品推薦。 有了準確的預測模型，客戶的購買記錄就能讓您深入瞭解他們可能會對哪些產品感興趣。

## 這是專為誰打造的配方？

現今，零售商可以提供多種產品，為客戶提供許多選擇，但也可能阻礙客戶搜尋。 由於時間和精力限制，客戶可能無法找到他們想要的產品，導致購買行為與認知有高度不協調，或根本不會購買。

## 這個配方有什麼作用？

產品Recommendations的配方使用機器學習來分析客戶與過去產品的互動，並快速輕鬆地產生產品推薦的個人化清單。 如此可最佳化產品探索程式，並免除對客戶進行冗長、低效且無關的搜尋。 因此，產品Recommendations配方可以改善客戶的整體購買體驗，進而提高參與度和品牌忠誠度。

## 如何開始使用？

您可以依照Adobe Experience Platform Lab教學課程來開始使用（請參閱下方的Lab連結）。 本教學課程將示範如何遵循下列步驟，在Jupyter Notebook中建立「產品Recommendations」配方 [記事本至配方](../jupyterlab/create-a-model.md) 工作流程，並在中實作配方 [!DNL Experience Platform] [!DNL Data Science Workspace].

* [實驗室：使用資料科學工作區預測未來](https://expleague.azureedge.net/labs/L777/index.html)
* [實驗室資源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 資料結構描述

此配方使用自訂 [XDM結構描述](../../xdm/schema/field-dictionary.md) 若要為輸入和輸出資料建立模型：

### 輸入資料結構描述

| 字段名称 | 类型 |
| --- | --- |
| itemId | 字符串 |
| interactiontype | 字符串 |
| timestamp | 字符串 |
| userId | 字符串 |

### 輸出資料結構描述

| 字段名称 | 类型 |
| --- | --- |
| recommendations | 字符串 |
| userId | 整数 |

## 演演算法

產品Recommendations配方利用合作篩選，為您的客戶產生個人化的產品推薦清單。 協同篩選不同於以內容為基礎的方法，不需要特定產品的相關資訊，而是利用客戶對一組產品的歷史偏好設定。 這項強大的建議技術使用兩個簡單的假設：
* 有些客戶有類似的興趣，且可透過比較其購買和瀏覽行為來分組。
* 根據類似客戶的購買和瀏覽行為，客戶更可能對推薦感興趣。

此程式分為兩個主要步驟。 首先，定義類似客戶的子集。 然後，在該集合中，識別這些客戶中的類似功能，以便為目標客戶傳回建議。
