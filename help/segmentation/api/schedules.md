---
keywords: Experience Platform；首頁；熱門主題；細分；細分；細分服務；排程；排程；API；API；
solution: Experience Platform
title: 排程API端點
description: 排程是一種工具，可用來每天自動執行一次批次細分工作。
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2009'
ht-degree: 3%

---

# 排程端點

排程是一種工具，可用來每天自動執行一次批次細分工作。 您可以使用 `/config/schedules` 端點可擷取排程清單、建立新排程、擷取特定排程的詳細資訊、更新特定排程，或刪除特定排程。

## 快速入门

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 擷取排程清單 {#retrieve-list}

您可以透過向以下網站發出GET請求，擷取組織的所有排程清單： `/config/schedules` 端點。

**API格式**

此 `/config/schedules` 端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用它們來協助減少昂貴的額外負荷。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有排程。 可包含多個引數，以&amp;符號(`&`)。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{START}` | 指定位移的起始頁面。 預設情況下，此值將為0。 |
| `{LIMIT}` | 指定傳回的排程數。 根據預設，此值將為100。 |

**请求**

下列請求將擷取您組織內公佈的最後10個排程。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回HTTP狀態200，其中包含指定組織的排程清單，格式為JSON。

>[!NOTE]
>
>下列回應已截斷空格，且只顯示傳回的第一個排程。

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
| -------- | ------------ |
| `_page.totalCount` | 傳回的排程總數。 |
| `_page.pageSize` | 排程頁面的大小。 |
| `children.name` | 字串形式的排程名稱。 |
| `children.type` | 字串形式的作業型別。 兩種支援的型別為「batch_segmentation」和「export」。 |
| `children.properties` | 包含與排程相關之其他屬性的物件。 |
| `children.properties.segments` | 使用 `["*"]` 可確保納入所有區段。 |
| `children.schedule` | 包含工作排程的字串。 工作只能排程一天執行一次，這表示您不能將工作排程在24小時的期間內執行超過一次。 如需cron排程的詳細資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 * *」表示此排程將在每天凌晨1:00執行。 |
| `children.state` | 包含排程狀態的字串。 兩種支援的狀態為「作用中」和「非作用中」。 依預設，狀態會設為「非使用中」。 |

## 建立新排程 {#create}

您可以透過向以下傳送POST請求來建立新排程： `/config/schedules` 端點。

**API格式**

```http
POST /config/schedules
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| 属性 | 描述 |
| -------- | ------------ |
| `name` | **必需。** 字串形式的排程名稱。 |
| `type` | **必需。** 字串形式的作業型別。 兩種支援的型別為「batch_segmentation」和「export」。 |
| `properties` | **必需。** 包含與排程相關之其他屬性的物件。 |
| `properties.segments` | **下列情況需要： `type` 等於「batch_segmentation」。** 使用 `["*"]` 可確保納入所有區段。 |
| `schedule` | *可选.* 包含工作排程的字串。 工作只能排程一天執行一次，這表示您不能將工作排程在24小時的期間內執行超過一次。 如需cron排程的詳細資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 * *」表示此排程將在每天凌晨1:00執行。 <br><br>如果未提供此字串，則會自動產生系統產生的排程。 |
| `state` | *可选.* 包含排程狀態的字串。 兩種支援的狀態為「作用中」和「非作用中」。 依預設，狀態會設為「非使用中」。 |

**响应**

成功的回應會傳回HTTP狀態200以及您新建立排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## 擷取特定排程 {#get}

您可以透過向以下網站發出GET請求，擷取有關特定排程的詳細資訊： `/config/schedules` 端點，並提供您要在請求路徑中擷取之排程的ID。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要擷取之排程的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

| 属性 | 描述 |
| -------- | ------------ |
| `name` | 字串形式的排程名稱。 |
| `type` | 字串形式的作業型別。 兩種支援的型別為 `batch_segmentation` 和 `export`. |
| `properties` | 包含與排程相關之其他屬性的物件。 |
| `properties.segments` | 使用 `["*"]` 可確保納入所有區段。 |
| `schedule` | 包含工作排程的字串。 工作只能排程一天執行一次，這表示您不能將工作排程在24小時內執行超過一次。 如需cron排程的詳細資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 * *」表示此排程將在每天凌晨1:00執行。 |
| `state` | 包含排程狀態的字串。 兩種支援的狀態為 `active` 和 `inactive`. 依預設，狀態會設為 `inactive`. |

## 更新特定排程的詳細資料 {#update}

您可以透過向發出PATCH請求來更新特定排程 `/config/schedules` 端點並在請求路徑中提供您嘗試更新的排程ID。

PATCH請求可讓您更新 [state](#update-state) 或 [cron排程](#update-schedule) 適用於個別排程。

### 更新排程狀態 {#update-state}

您可以使用JSON修補程式操作來更新排程的狀態。 若要更新狀態，您需宣告 `path` 屬性為 `/state` 並設定 `value` 為 `active` 或 `inactive`. 如需JSON修補程式的詳細資訊，請參閱 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 說明檔案。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的排程值。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 您要修補的值的路徑。 在此情況下，由於您正在更新排程的狀態，因此您必須將值設為 `path` 至「/state」。 |
| `value` | 排程狀態的更新值。 此值可設為「作用中」或「非作用中」，以啟用或停用排程。 請注意 **無法** 如果組織已啟用串流，請停用排程。 |

**响应**

成功的回應會傳回HTTP狀態204 （無內容）。

### 更新cron排程 {#update-schedule}

您可以使用JSON修補程式操作來更新cron排程。 若要更新排程，您需要宣告 `path` 屬性為 `/schedule` 並設定 `value` 至有效的cron排程。 如需JSON修補程式的詳細資訊，請參閱 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 說明檔案。 如需cron排程的詳細資訊，請閱讀 [cron運算式格式](#appendix).

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的排程值。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 您要更新的值的路徑。 在此情況下，由於您正在更新cron排程，因此您需要將 `path` 至 `/schedule`. |
| `value` | cron排程的更新值。 此值必須採用cron排程的形式。 在此範例中，排程會在每月的第二日執行。 |

**响应**

成功的回應會傳回HTTP狀態204 （無內容）。

## 刪除特定排程

您可以透過向以下網站發出DELETE請求，請求刪除特定排程： `/config/schedules` 端點並在請求路徑中提供您要刪除之排程的ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要刪除之排程的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）。

## 后续步骤

閱讀本指南後，您現在已更瞭解排程的運作方式。

## 附录 {#appendix}

下列附錄說明排程中使用的cron運算式格式。

### 格式

cron運算式是包含6或7個欄位的字串。 運算式看起來類似下列：

`0 0 12 * * ?`

在cron運算式字串中，第一個欄位代表秒，第二個欄位代表分鐘，第三個欄位代表小時，第四個欄位代表一月中的日，第五個欄位代表月，第六個欄位代表一週中的日。 您也可以選擇加入代表年份的第七個欄位。

| 字段名称 | 必需 | 可能的值 | 允許的特殊字元 |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | 是 | 0-59 | `, - * /` |
| Minutes | 是 | 0-59 | `, - * /` |
| 小時 | 是 | 0 时至 23 时 | `, - * /` |
| 月中几号 | 是 | 1 日至 31 日 | `, - * ? / L W` |
| 月 | 是 | 1-12、2012年1月12日 | `, - * /` |
| 每周的某一日 | 是 | 1-7，星期日 | `, - * ? / L #` |
| 年 | 否 | 空白，1970-2099 | `, - * /` |

>[!NOTE]
>
>月份名稱和一週中的日期名稱為 **not** 區分大小寫。 因此， `SUN` 等於使用 `sun`.

允許的特殊字元代表下列含義：

| 特殊字元 | 描述 |
| ----------------- | ----------- |
| `*` | 此值用於選取 **全部** 欄位中的值。 例如， `*` 在「小時」欄位中會表示 **每** 小時。 |
| `?` | 此值表示不需要特定值。 這通常用於在一個允許字元的欄位中指定內容，但不能在另一個欄位中指定。 例如，如果您想要在每月的3日觸發事件，但並不在乎星期幾，您可能會將 `3` 在「日期」欄位和 `?` 在「星期」欄位中。 |
| `-` | 此值用於指定 **包含** 欄位範圍。 例如，如果您將 `9-15` 在「小時」欄位中，這表示小時將包含9、10、11、12、13、14和15。 |
| `,` | 此值用於指定其他值。 例如，如果您將 `MON, FRI, SAT` 在「星期」欄位中，這表示一週的天數包括星期一、星期五和星期六。 |
| `/` | 此值用於指定增量。 放置在「 」之前的值 `/` 會決定從何處遞增，而值會放在 `/` 會決定其增加多少。 例如，如果您將 `1/7` 在「分鐘」欄位中，這表示分鐘會包含1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用於指定 `Last`和的意義因使用的欄位而異。 如果搭配月份欄位使用，則代表該月的最後一天。 如果單獨與「星期」欄位一起使用，則它表示一週的最後一天，即星期六(`SAT`)。 如果與「星期」欄位搭配使用，並搭配其他值，則代表該月該型別的最後一天。 例如，如果您將 `5L` 在一週中的第幾天，它會 **僅限** 包括當月的最後一個星期五。 |
| `W` | 此值用於指定最接近指定日期的工作日。 例如，如果您將 `18W` 在月份欄位的日期中，當月18日是星期六，則會在17日（星期五）觸發，這是最接近的工作日。 如果該月18日是星期日，則會在19日（最接近的工作日）的星期一觸發。 請注意，如果您將 `1W` 在「日期」欄位中，如果最近的工作日是上個月，則事件仍會在最近的工作日觸發 **目前** 月。</br></br>此外，您也可以結合 `L` 和 `W` 製作 `LW`，會指定該月的最後一個工作日。 |
| `#` | 此值用於指定某月中一週的第n天。 放置在「 」之前的值 `#` 表示一週中的第幾天，而值放在以下日期之後： `#` 代表當月發生的次數。 例如，如果您將 `1#3`，事件便會在當月第三個星期日觸發。 請注意，如果您將 `X#5` 而且該月沒有該周第五個發生日期，該事件將 **not** 觸發。 例如，如果您將 `1#5`，而且該月沒有第五個星期日，該事件將 **not** 觸發。 |

### 示例

下表顯示cron運算式字串範例，並說明其意義。

| 表达式 | 解释 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 事件將於每天下午1點引發。 |
| `0 30 9 * * ? 2022` | 該活動將於2022年每日上午9:30觸發。 |
| `0 * 18 * * ?` | 此事件會每分鐘引發一次，從下午6點開始，一直到每天下午6:59結束。 |
| `0 0/10 17 * * ?` | 事件會從每天下午5點開始，下午6點結束，每10分鐘引發一次。 |
| `0 13,38 5 ? 6 WED` | 此活動將於每週三6月凌晨5:13及5:38引發。 |
| `0 30 12 ? * 4#3` | 事件將於每月第三個星期三中午12:30引發。 |
| `0 30 12 ? * 6L` | 事件將於每月最後一個星期五中午12:30引發。 |
| `0 45 11 ? * MON-THU` | 事件將於每個星期一、星期二、星期三和星期四上午11:45引發。 |