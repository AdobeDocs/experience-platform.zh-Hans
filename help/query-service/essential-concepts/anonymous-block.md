---
title: 查詢服務中的匿名區塊
description: 匿名區塊是Adobe Experience Platform Query Service支援的SQL語法，可讓您有效執行一系列查詢
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 查詢服務中的匿名區塊

Adobe Experience Platform查詢服務支援匿名區塊。 匿名區塊功能可讓您連結一或多個依序執行的SQL敘述句。 它們也允許例外狀況處理的選項。

匿名區塊功能是執行一系列操作或查詢的有效方式。 區塊中的查詢鏈結可以儲存為範本，並排程在特定時間或間隔執行。 這些查詢可用於寫入和附加資料以建立新的資料集，通常用於您有相依性的地方。

>[!IMPORTANT]
>
>使用匿名區塊排程查詢目前只能透過 [!DNL Query Service] API。 請參閱以下檔案： [透過API排程查詢的完整指示](../api/scheduled-queries.md).

此表格提供區塊主要區段的劃分：執行和例外狀況處理。 截面由關鍵字定義 `BEGIN`， `END`、和 `EXCEPTION`.

| 區段 | 描述 |
|---|---|
| 執行 | 可執行區段以關鍵字開頭 `BEGIN` 且結尾是關鍵字 `END`. 內含的任何陳述式集 `BEGIN` 和 `END` 關鍵字將依序執行，並確保後續查詢要等到序列中的上一個查詢完成後才會執行。 |
| 例外狀況處理 | 選用的例外狀況處理區段以關鍵字開頭 `EXCEPTION`. 它包含程式碼，可在執行區段中的任何SQL敘述句失敗時擷取及處理例外狀況。 如果任何查詢失敗，則會停止整個區塊。 |

值得注意的是，區塊是可執行陳述式，因此可以巢狀內嵌於其他區塊中。

>[!NOTE]
>
> 強烈建議您在較小的資料集上測試查詢，並確保它們按預期運作。 如果查詢有語法錯誤，則會擲回例外狀況，並中止整個區塊。 一旦確認了查詢的完整性，您就可以開始將它們鏈結。 這可確保區塊在您投入運作前可如預期般運作。

## 匿名區塊查詢範例

下列查詢顯示鏈結SQL敘述句的範例。 請參閱 [查詢服務中的SQL語法](../sql/syntax.md) 檔案，以取得有關所使用的任何SQL語法的詳細資訊。

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

在以下範例中， `SET` 儲存的結果 `SELECT` 在指定的本機變數中查詢。 變數的範圍設為匿名區塊。

快照ID會儲存為本機變數(`@current_sid`)。 然後用於下一個查詢，以根據相同資料集/表格的SNAPSHOT傳回結果。

資料庫快照集是SQL Server資料庫的唯讀靜態檢視。 更多資訊 [有關快照子句的資訊](../sql/syntax.md#SNAPSHOT-clause) 請參閱SQL語法檔案。

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 后续步骤

閱讀本檔案後，您現在已清楚瞭解匿名區塊及其結構。 [有關查詢執行的詳細資訊](../best-practices/writing-queries.md)，請參閱查詢服務中的查詢執行指南。

您也應該閱讀有關 [匿名區塊如何與增量載入設計模式搭配使用](./incremental-load.md) 以提高查詢效率。
