---
keywords: Experience Platform；首頁；熱門主題；
title: 資料準備疑難排解指南
description: 本檔案提供有關Adobe Experience Platform資料準備的常見問題解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] 疑難排解指南

本檔案提供有關Adobe Experience Platform常見問題的解答 [!DNL Data Prep]以及常見錯誤的疑難排解指南。 如需有關Platform API的一般問題和疑難排解資訊，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

## 常见问题解答

以下為常見問題集的相關清單 [!DNL Data Prep] 以及他們的答案。

### 如何解決轉換錯誤？

[!DNL Data Prep] 將所有轉換錯誤當地語系化至其發生的欄。 因此，該欄會變成無效，而列的其餘部分會繼續處理。 這些轉換問題會記錄為 **警告**. 建議您定期檢閱警告，並調整轉換邏輯，以解決轉換問題。 這樣會提高Experience Platform中所擷取的資料品質。

如果欄標籤為 **必填** 會因轉換問題而成為無效，則不會擷取該列。 啟用部分資料擷取時，您可以設定在整個流程失敗之前拒絕的臨界值。 如果無效屬性並未影響任何結構描述層級驗證，則會繼續內嵌列。

即使沒有任何轉換錯誤，任何無效的列也會被拒絕。 例如，資料擷取流程可能會有必要欄位的傳遞對應（無轉換邏輯），且該屬性沒有傳入值。 將拒絕此列。

### 如何在欄位中逸出特殊字元？

您可以使用來逸出欄位中的特殊字元 `${...}`. 不過，包含具有句點(`.`)不受此機制支援。 與階層互動時，如果子屬性有句點(`.`)，則必須使用反斜線(`\`)以逸出特殊字元。 例如， `address` 是包含屬性的物件 `street.name`，則這可以稱為 `address.street\.name` 而非 `address.street.name`.

### 計算欄位的最大長度是多少？

計算欄位的長度上限為4096個字元。