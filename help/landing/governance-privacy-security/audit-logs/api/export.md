---
title: 稽核事件匯出API端點
description: 瞭解如何使用稽核查詢API以Experience Platform匯出稽核事件。
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# 匯出稽核事件清單

您可以向以下發出GET要求來擷取事件資料： `/audit/export` 端點，指定您要在裝載中擷取的事件。

**API格式**

```http
GET /audit/export
```

| 参数 | 描述 |
| --------- | ----------- |
| `timestamp` | 依時間戳記篩選時，最佳實務是使用>和&lt;運運算元來使用範圍，而不是確切的值。 <br/>示例: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | 動作的狀態。 狀態可以是下列任一專案： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>示例: `?property=status==Deny`. |
| `action` | 為事件記錄的動作型別。 動作可以是下列任一專案： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> 示例：`?property=action==Create`。 |
| `user` | 執行事件的使用者。 |
| `assetType` | 執行動作的Platform資源型別。 <br/>示例: `?property=assetType==<an asset type>`. |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**响应**

結果會產生CSV檔案以供匯出。 成功的回應會傳回HTTP 307，但沒有回應內文。 匯出檔案的連結提供於 `Location` 回應標頭。
