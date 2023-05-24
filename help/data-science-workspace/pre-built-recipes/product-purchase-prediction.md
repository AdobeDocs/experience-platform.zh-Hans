---
keywords: Experience Platform；產品購買配方；資料科學工作區；熱門主題；配方；預先建置配方
solution: Experience Platform
title: 產品購買預測配方
description: 「產品購買預測」配方可讓您預測特定客戶購買事件型別（例如，產品購買）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 產品購買預測配方

「產品購買預測」配方可讓您預測特定客戶購買事件型別（例如，產品購買）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下檔案將回答下列問題：
* 這是專為誰打造的配方？
* 這個配方有什麼作用？

## 這是專為誰打造的配方？

您的品牌尋求透過對客戶的有效和有針對性的促銷來提升產品線的季度銷售。 不過，並非所有客戶都一樣，而且您想要物有所值。 您會鎖定誰？ 您的哪些客戶最有可能回應，而不會發現您的促銷活動造成干擾？ 如何針對每位客戶自訂您的促銷活動？ 您應依賴哪些管道，以及何時應傳送促銷活動？

## 這個配方有什麼作用？

「產品購買預測」配方使用機器學習來預測客戶的購買行為。 其做法是套用自訂的隨機森林分類器和雙層體驗資料模型(XDM)來預測購買事件的機率。 此模型運用輸入資料，結合客戶設定檔資訊和過往購買記錄，並預設為資料科學家決定的預先設定引數，以提高預測準確性。

## 資料結構描述

此配方使用 [XDM結構描述](../../xdm/home.md) 以模型化資料。 用於此配方的結構描述如下所示：

| 字段名称 | 类型 |
| --- | --- |
| userId | 字符串 |
| genderRatio | 数值 |
| ageY | 数值 |
| ageM | 数值 |
| optinEmail | 布尔值 |
| optinMobile | 布尔值 |
| optinAddress | 布尔值 |
| 已建立 | 整数 |
| totalOrder | 数值 |
| totalitems | 数值 |
| orderDate1 | 数值 |
| shippingDate1 | 数值 |
| totalPrice1 | 数值 |
| tax1 | 数值 |
| orderDate2 | 数值 |
| shippingDate2 | 数值 |
| totalPrice2 | 数值 |


## 演演算法

首先，此範本中的訓練資料集 *ProductPrediction* 結構描述已載入。 從此處，模型會使用 [隨機森林分類器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). 隨機森林分類器是一種整合的演演算法，它參考將多個演演算法結合起來以獲得改進預測效能的演演算法。 演演算法背後的想法是隨機森林分類器會建置多個決策樹，並將其合併以建立更精確且穩定的預測。

此程式會先建立一組決策樹，隨機選取訓練資料的子集。 之後，會平均每個決策樹的結果。
