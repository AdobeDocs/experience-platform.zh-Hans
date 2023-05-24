---
keywords: Experience Platform；首頁；熱門主題；列出可用沙箱；列出沙箱
solution: Experience Platform
title: 可用的沙箱API端點
description: 您可以透過向可用的沙箱端點發出GET請求來列出可供目前使用者使用的沙箱。
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 可用的沙箱端點

>[!NOTE]
>
>與沙箱API中提供的其他端點不同，此端點適用於所有使用者，包括沒有沙箱管理存取許可權的使用者。

您可以透過向可用的沙箱端點發出GET請求來列出可供目前使用者使用的沙箱。

**API格式**

```http
GET /{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 請參閱 [附錄檔案](./appendix.md#query) 以取得可用引數的清單。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功回應會傳回目前使用者可用的沙箱清單，包括詳細資訊，例如 `name`， `title`， `state`、和 `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 沙箱的名稱。 用於API呼叫中的查閱目的。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱目前的處理狀態。 沙箱的狀態可以是下列任一專案： <ul><li>`creating`：沙箱已建立，但系統仍在布建中。</li><li>`active`：沙箱已建立且作用中。</li><li>`failed`：由於發生錯誤，沙箱無法由系統布建，因此已停用。</li><li>`deleted`：沙箱已手動停用。</li></ul> |
| `type` | 沙箱型別：「開發」或「生產」。 |
| `isDefault` | 布林值屬性，指出此沙箱是否為組織的預設生產沙箱。 |
| `eTag` | 特定版本沙箱的識別碼。 用於版本控制和快取效率，每次對沙箱進行變更時都會更新此值。 |
