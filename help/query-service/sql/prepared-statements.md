---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；準備的陳述式；準備的；sql；
solution: Experience Platform
title: 查詢服務中的準備陳述式
description: 在SQL中，準備的敘述句用於範本類似的查詢或更新。 Adobe Experience Platform Query Service使用引數化的查詢支援準備陳述式。
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# 準備的陳述式

在SQL中，準備的敘述句用於範本化類似的查詢或更新。 Adobe Experience Platform [!DNL Query Service] 使用引數化查詢支援準備陳述式。 這可最佳化效能，因為您不再需要重複地重新剖析查詢。

## 使用準備的陳述式

使用預準備陳述式時，支援下列語法：

- [準備](#prepare)
- [執行](#execute)
- [解除配置](#deallocate)

### 準備準備準備的陳述式 {#prepare}

此SQL查詢會將寫入的SELECT查詢儲存為名稱 `PLAN_NAME`. 您可以使用變數，例如 `$1` 代替實際值。 這個準備好的陳述式將會在目前的工作階段期間儲存。 請注意，計畫名稱是 **not** 區分大小寫。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 範例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 執行準備的陳述式 {#execute}

此SQL查詢使用先前建立的準備陳述式。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 範例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 解除配置準備的陳述式 {#deallocate}

此SQL查詢用於刪除已命名的準備陳述式。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 範例SQL

```sql
DEALLOCATE test;
```

## 使用準備陳述式的範例流程

最初，您可以有SQL查詢，例如以下查詢：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查詢將傳回下列回應：

| id | firstname | 姓氏 | 生日 | 电子邮件 | city | 國家/地區 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | davis | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 10001 | antoine | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 恭子 | 櫻花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 彼得松 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 10004 | 更容易 | waithaka | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 10005 | 費爾南多 | rios | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

您可以使用下列準備的陳述式將此SQL查詢引數化：

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

現在，可以使用以下呼叫執行準備好的陳述式：

```sql
EXECUTE getIdRange(10000, 10005);
```

呼叫此專案時，您會看到與之前完全相同的結果：

| id | firstname | 姓氏 | 生日 | 电子邮件 | city | 國家/地區 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | davis | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 10001 | antoine | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 恭子 | 櫻花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 彼得松 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 10004 | 更容易 | waithaka | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 10005 | 費爾南多 | rios | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

使用完預先準備的陳述式後，您可以使用下列呼叫來解除配置它：

```sql
DEALLOCATE getIdRange;
```
