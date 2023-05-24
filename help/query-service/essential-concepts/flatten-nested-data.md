---
keywords: Experience Platform；查詢服務；查詢服務；巢狀資料結構；巢狀資料；平面化；平面化巢狀資料；
title: 平面化巢狀資料結構以與BI工具一起使用
description: 本檔案說明如何將協力廠商BI工具與查詢服務搭配使用時，在工作階段期間所有表格和檢視的XDM結構描述平面化。
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 平面化巢狀資料結構以搭配協力廠商BI工具使用

Adobe Experience Platform查詢服務支援 `FLATTEN` 透過協力廠商BI工具連線至資料庫時設定。 此功能可平面化協力廠商BI工具中的巢狀資料結構，以改善其可用性並減少擷取、分析、轉換和報告資料所需的工作負載。

許多BI工具如下 [!DNL Tableau] 和 [!DNL Power BI] 不原生支援巢狀資料結構。 此 `FLATTEN` 設定會移除在資料上建立SQL檢視以提供平面版本或使用查詢服務的需要 `CTAS` 或 `INSERT INTO` 使用臨時結構描述時，將資料集複製到平面版本的工作。

此 `FLATTEN` 設定會將每個分葉欄位的結構提取到表格的根中，並將欄位命名在原始名稱空間之後。 這可讓您使用點標籤法來比對欄位與其體驗資料模型(XDM)路徑，同時保留欄位的內容。

## 先决条件

使用 `FLATTEN` 設定需要深入瞭解下列Adobe Experience Platform元件：

* [XDM系統](../../xdm/home.md)：XDM及其在Experience Platform中實作的高層級概觀。

   * [建立臨時結構描述](../../xdm/tutorials/ad-hoc.md)：XDM結構描述中的欄位已命名為只供單一資料集使用，即稱為臨時結構描述。 臨時結構用於各種資料擷取工作流程，以供Experience Platform和建立特定型別的來源連線。

* [沙箱](../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

* [巢狀資料結構](./nested-data-structures.md)：本檔案提供範例，說明如何建立、處理或轉換具有複雜資料型別（包括巢狀資料結構）的資料集。

## 使用FLATTEN設定連線到資料庫 {#connect-with-flatten}

此 `FLATTEN` 設定平面化將巢狀資料結構分成個別的欄，其中屬性名稱會成為保留列值的欄名稱。 在不支援巢狀資料結構的BI工具中使用資料時，此設定可改善臨時結構描述的可用性並減少必要的工作負載。

使用您選擇的協力廠商使用者端連線至查詢服務時，請附加 `FLATTEN` 設定為資料庫名稱。 如需如何連線特定BI工具的詳細資訊，請參閱 [將使用者端連線至查詢服務概述](../clients/overview.md). 連線字串應包含：

* 沙箱名稱。
* 冒號後接 `all` 或特定資料集ID、檢視ID或資料庫名稱。
* 問號(？) 後面接著 `FLATTEN` 關鍵字。

輸入內容應採用以下格式：

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

連線字串範例可能如下所示：

```terminal
prod:all?FLATTEN
```

## 示例 {#example}

本指南中使用的範例結構描述會採用標準欄位群組 [!UICONTROL 商務詳細資料]，會使用 `commerce` 物件結構和 `productListItems` 陣列。 請參閱XDM檔案以瞭解 [有關以下專案的更多資訊： [!UICONTROL 商務詳細資料] 欄位群組](../../xdm/field-groups/event/commerce-details.md). 結構描述結構的代表可以在下圖中看到。

![商務詳細資料欄位群組的結構描述圖，包括 `commerce` 和 `productListItems` 結構。](../images/essential-concepts/commerce-details.png)

如果您的BI工具不支援巢狀資料結構，則可能很難參考巢狀欄位，因為這些欄位包含序列化的值(例如 `commerce` 和 `productListItems` （在範例結構描述中）。 這些值可能會顯示為單一編碼的一部分 `commerce` 字串欄位和並非實際無法使用。

下列值代表 `commerce.order.priceTotal` (3018.0)， `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180)，以及 `commerce.purchases.value`(1.0)在格式不正確的巢狀欄位中。

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

藉由使用 `FLATTEN` 設定，您可以使用點標籤法及其原始路徑名稱，來存取架構內的個別欄位或巢狀資料結構的整個區段。 此格式的範例，使用 `commerce` 欄位群組如下。

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

此 `FLATTEN` 設定在處理其他資料結構時有一定的限制。 完整的詳細資料請參見 [限制區段](#limitations).

### 查詢中的欄位使用引號 {#quotation-marks}

平面化的根欄位現在使用點標籤法來比對其XDM路徑。 在查詢中使用時，欄位需要用引號(「 」)括住。

下列SQL範例顯示巢狀查詢的原始狀態：

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

使用平面化資料欄位時，查詢會使用點標籤法撰寫，並括在引號中，如下所示：

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## 限制 {#limitations}

此 `FLATTEN` 設定目前不會平面化下列資料結構：

| 資料結構 | 限制 |
|---|---|
| 数组 | 使用明確的陣列索引或 `EXPLODE` 函式以存取陣列。 |
| 地图 | 使用字串索引鍵來存取對應下的值，以存取對應。 |

若要解決Map和Array限制，您需要使用BI工具原始SQL編輯，例如Power BI中的[進階選項] -> [SQL陳述式]。

需要原始SQL編輯等BI工具來解決對應和陣列限制。 請參閱操作方法指南 [使用Power BI進階選項輸入自訂SQL查詢](../clients/power-bi.md#import-tables-using-custom-sql) SQL陳述式區段中的。

## 后续步骤

本檔案說明如何平面化巢狀資料結構，以搭配協力廠商BI工具使用。 如果您尚未連線使用者端，請參閱 [使用者端連線概觀](../clients/overview.md) 以取得支援的協力廠商使用者端清單。
