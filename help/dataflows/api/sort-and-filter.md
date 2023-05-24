---
title: 排序和篩選流程服務API中的回應
description: 本教學課程涵蓋在Flow Service API中使用查詢引數進行排序和篩選的語法，包括一些進階使用案例。
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: ef8db14b1eb7ea555135ac621a6c155ef920e89a
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 3%

---

# 排序和篩選流程服務API中的回應

在中執行清單(GET)請求時 [流程服務API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，您可使用查詢引數來排序和篩選回應。 本指南提供在不同使用案例下如何使用這些引數的參考資料。

## 排序

您可以使用 `orderby` 查詢引數。 下列資源可在API中排序：

* [连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [來源連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [目標連線](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流程](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [執行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

若要使用引數，您必須將其值設為排序依據的特定屬性(例如， `?orderby=name`)。 您可以在值前面加上加號(`+`)作為遞增順序或減號(`-`)以遞減順序排列。 如果未提供排序首碼，清單預設會依遞增順序排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

您也可以使用&quot;and&quot;符號(`&`)。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 正在筛选

您可以使用來篩選回應 `property` 使用索引鍵值運算式的引數。 例如， `?property=id==12345` 只傳回以下專案的資源： `id` 屬性完全等於 `12345`.

只要知曉屬性的有效路徑，篩選功能通常可套用至實體中的任何屬性。

>[!NOTE]
>
>如果屬性巢狀內嵌於陣列專案中，您必須附加方括弧(`[]`)至路徑中的陣列。 請參閱以下小節： [篩選陣列屬性](#arrays) 例如。

**傳回來源表格名稱為的所有來源連線 `lead`：**

```http
GET /sourceConnections?property=params.tableName==lead
```

**傳回特定區段ID的所有流程：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 組合篩選器

多個 `property` 篩選條件必須以「和」字元(`&`)。 組合篩選器時會假設AND關係，這表示實體必須滿足所有篩選器，才能將其包含在回應中。

**傳回區段ID的所有啟用流程：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 篩選陣列屬性 {#arrays}

您可以根據陣列中專案的屬性進行篩選，方法是附加 `[]` 至陣列屬性的名稱。

**與特定來源連線相關聯的傳回流程：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**傳回含有特定選取器值ID之轉換的資料流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**傳回含有具有特定欄的來源連線 `name` 值：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**透過篩選區段ID來查詢目的地的流程執行ID：**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何篩選查詢都可以附加 `count` 值為的查詢引數 `true` 以傳回結果的計數。 API回應包含 `count` 其值代表已篩選專案總數之屬性。 此呼叫中未傳回實際篩選的專案。

**傳回系統中已啟用的資料流的計數：**

```http
GET /flows?property=state==enabled&count=true
```

對上述查詢的回應如下所示：

```json
{
  "count": 95
}
```

### 可依資源篩選的屬性

根據您正在擷取的流量服務實體，可能會使用不同的屬性進行篩選。 下錶針對篩選使用案例中常用的每個資源，劃分根層級欄位。

**`connectionSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## 后续步骤

本指南說明如何使用 `orderby` 和 `property` 查詢引數，用於排序和篩選流程服務API中的回應。 如需如何將API用於Platform中常見工作流程的逐步指南，請參閱 [來源](../../sources/home.md) 和 [目的地](../../destinations/home.md) 說明檔案。
