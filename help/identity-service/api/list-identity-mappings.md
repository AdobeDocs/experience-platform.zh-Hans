---
keywords: Experience Platform；首頁；熱門主題；身分；身分
solution: Experience Platform
title: 清單身分對應
description: 對應是叢集中指定名稱空間之所有身分識別的集合。
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---

# 清單身分對應

對應是叢集中指定名稱空間之所有身分識別的集合。

## 取得單一身分的身分對應

指定身分後，從要求中身分所代表的名稱空間擷取所有相關身分。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**请求**

選項1：以名稱空間形式提供身分(`nsId`，依ID)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項2：以名稱空間形式提供身分(`ns`，依名稱)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項3：以XID提供身分(`xid`)。 如需如何取得身分識別的XID的詳細資訊，請參閱本檔案涵蓋的章節 [取得身分的XID](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 取得多個身分的身分對應

使用 `POST` 方法當作 `GET` 上述方法可擷取多個身分的對應。

>[!NOTE]
>
>要求不應超過最多1000個身分。 超過1000個身分的要求會產生400個狀態代碼。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**要求內文**

選項1：提供要擷取對應的XID清單。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

選項2：提供身分清單作為複合ID，其中每個名稱依名稱空間ID命名ID值和名稱空間。 此範例示範在覆寫預設值時使用此方法 `graph-type` 「私密圖表」的。

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**请求**

**使用XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**使用UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

如果提供的輸入找不到相關身分， `HTTP 204` 傳回的回應代碼沒有內容。

**响应**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`：輸入身分最後一次與此身分關聯的時間戳記。
- `regions`：提供 `regionId` 和 `lastAssociationTime` 檢視身分的位置。

## 后续步骤

繼續下一教學課程，前往 [列出可用的名稱空間](./list-namespaces.md).
