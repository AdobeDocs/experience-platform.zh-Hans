---
title: 資料集範例
description: 查詢服務範例資料集可讓您對大資料執行探索性查詢，並大幅減少處理時間，但代價是查詢準確性。 本指南提供如何管理範例以進行近似查詢處理的資訊
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 資料集範例

Adobe Experience Platform查詢服務提供範例資料集，作為其近似查詢處理功能的一部分。 範例資料集是以現有的均勻隨機範例建立的 [!DNL Azure Data Lake Storage] (ADLS)資料集只會使用原始資料記錄的一個百分比。 此百分比稱為取樣率。 調整取樣率以控制精確度和處理時間的平衡，可讓您對大資料進行探索性查詢，並大幅減少處理時間，但代價是查詢精確度。

由於許多使用者不需要資料集彙總操作的確切答案，因此對大型資料集發出近似查詢以傳回近似答案會更有效率。 由於範例資料集僅包含原始資料集中資料的一個百分比，因此可讓您以查詢正確性換取改善的回應時間。 在讀取時，查詢服務必須掃描的列數較少，產生的結果速度比您查詢整個資料集的速度更快。

為協助您管理近似查詢處理的範例，查詢服務支援下列資料集範例操作：

- [建立統一的隨機資料集範例。](#create-a-sample)
- [選擇性地指定篩選條件](##optional-filter-criteria)
- [檢視ADLS表格的範例清單。](#view-list-of-samples)
- [直接查詢範例資料集。](#query-sample-datasets)
- [刪除範例。](#delete-a-sample)
- 刪除原始ADLS表格時刪除關聯的範例。

## 快速入门 {#get-started}

若要使用本檔案中詳述的建立和刪除近似查詢處理功能，您必須將工作階段標幟設定為 `true`. 從「查詢編輯器」或PSQL使用者端的命令列輸入 `SET aqp=true;` 命令。

>[!NOTE]
>
>每次登入Platform時，都必須啟用工作階段標幟。

![反白顯示「SET aqp=true；」命令的查詢編輯器。](../images/essential-concepts/set-session-flag.png)

## 建立統一的隨機資料集範例 {#create-a-sample}

使用 `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` 命令以資料集名稱，從該資料集建立統一的隨機範例。

取樣率是從原始資料集中取得的記錄百分比。 您可以透過以下方式控制取樣率 `TABLESAMPLE SAMPLERATE` 關鍵字。 在此範例中，5.0的值等於50%的取樣率。 2.5的值將等於25%，以此類推。

>[!IMPORTANT]
>
>系統允許每個資料集最多五個範例。 如果您嘗試建立第六個範例資料集，畫面上會顯示錯誤訊息，指出已達到範例限制。

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## 選擇性地指定篩選條件 {#optional-filter-criteria}

您可以選擇指定統一隨機樣本的篩選條件。 這可讓您根據分析表格的篩選子集建立樣本。

建立範例時，會先套用選用篩選器，然後從資料集的篩選檢視建立範例。 已套用篩選器的資料集範例會遵循下列查詢格式：

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

此型別篩選樣本資料集的實用範例如下：

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

在提供的範例中，表格名稱為 `large_table`，原始表格的篩選條件為 `month(to_timestamp(timestamp)) in ('8', '9')`，而取樣率為（已篩選資料的X%），在這種情況下， `10`.

## 檢視範例清單 {#view-list-of-samples}

使用 `sample_meta()` 函式來檢視與ADLS表格相關聯的範例清單。

```sql
SELECT sample_meta('example_dataset_name')
```

資料集範例清單會以下列範例的格式顯示。

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 查詢範例資料集 {#query-sample-datasets}

使用 `{EXAMPLE_DATASET_NAME}` 以直接查詢範例表格。 或者，新增 `WITHAPPROXIMATE` 關鍵字到查詢及查詢服務結尾會自動使用最近建立的範例。

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## 刪除資料集範例 {#delete-a-sample}

刪除操作可讓您在達到5個資料集範例的最大限制後建立新範例。

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>如果您有多個從原始ADLS資料集衍生的範例資料集，在丟棄原始資料集時，所有關聯的範例也會被刪除。
