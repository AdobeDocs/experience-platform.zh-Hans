---
keywords: Experience Platform；首頁；熱門主題；資料型別；資料型別；資料型別；資料型別；分段資料型別；分段；分段；分段服務；分段服務資料型別；
solution: Experience Platform
title: 分段服務中支援的資料型別
description: Adobe細分服務支援所有Experience Data Model (XDM)資料型別。 構成區段定義的規則會依下列資料型別進行內容化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 分段服務中支援的資料型別

Adobe Experience Platform Segmentation Service支援所有Experience Data Model (XDM)資料型別。 構成區段定義的規則會依下列資料型別進行內容化。

## 字串資料

區段定義會使用字串資料來定義區段對象的非數值限制，例如「國家/地區名稱」或「忠誠計畫等級」。

字串資料會使用邏輯、包含/排除和比較陳述式包含在區段定義中。 將字串屬性新增至區段定義後，您可以使用字串相關陳述式，根據其他字串欄位評估該屬性。

| 陳述式型別 | 示例 |
| -------------- | -------- |
| 邏輯 | `and`、`or`、`not` |
| 包含/排除 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`、`does not equal`、`contains`、`starts with` |

## 日期資料

日期資料可讓您透過使用特定開始/結束日期或使用日期相關陳述式，將基於時間的內容指派給區段定義，如下表所示。 其中一項實作可能是建立隨時與您的品牌互動的客戶受眾 *今年* 並且也一直處於活動狀態 *範圍* 過去幾天。

| 範例欄位 | 日期相關陳述式 | 时间线 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`、`yesterday`、`this month`、`this year` | 與建立區段的日期相關。 |
| person.lastPurchase | `in last`、`during`、`before`、`after`、`within` | 在任何指定周/月內皆相關。 |

## 體驗事件

身為Adobe Experience Platform結構描述， [!DNL XDM ExperienceEvents] 紀錄以下專案的明確和隱含客戶互動： [!DNL Platform] — 整合的應用程式，包括進行互動時的系統快照。 [!DNL ExperienceEvents] 是事實記錄。 因此，區段是您在區段定義期間可用的資料來源。

如下表所示，事件資料會使用關鍵字呈現，以協助調整事件行為並指定事件屬性。

| 關鍵字 | 使用 |
| ------- | --- |
| 包括/排除 | 透過包含或遺漏資料來說明事件的行為。 |
| 任何/全部 | 協助判斷合格區段的數量。 |
| 「套用時間規則」切換按鈕 | 合併日期資料。 |
| 等於、不等於、開頭為、開頭為、結尾為、結尾為、包含、不包含、存在、不存在 | 合併字串資料。 |

### 受众共享

外部受眾也可作為新區段定義的元件，將其屬性規則新增至新區段。

目前僅支援Adobe Audience Manager作為外部對象，未來會啟用其他來源。 如需有關搭配Platform使用Adobe Audience Manager對象的詳細資訊，請參閱 [Adobe Audience Manager檔案中的對象共用指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### 區段共用

在Platform中建立的區段可以用在其他 [Adobe Experience Cloud核心服務](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). 若要啟用此功能，您需要連絡解決方案架構師或顧問。

## 其他資料型別

除了上述的資料型別之外，支援的資料型別清單也包含：

- 統一資源識別碼(URI)
- 列舉
- 数值
- 長
- 整数
- 短
- 位元組
- 布尔值
- 陣列
- 对象
- 地图
