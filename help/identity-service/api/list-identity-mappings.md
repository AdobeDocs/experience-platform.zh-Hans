---
keywords: Experience Platform；主页；热门主题；身份；身份
solution: Experience Platform
title: 列出身份映射
description: 映射是群集中指定命名空间的所有标识的集合。
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# 列表身份映射

映射是群集中指定命名空间的所有标识的集合。

## 获取单个标识的标识映射

给定一个身份，从与请求中该身份所代表的命名空间相同的命名空间中检索所有相关身份。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**请求**

选项1：以命名空间形式提供身份(`nsId`，按ID)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项2：以命名空间形式提供身份(`ns`，按名称)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项3：以XID形式提供身份(`xid`)。 有关如何获取身份的XID的更多信息，请参阅本文档中涵盖的部分 [获取标识的XID](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 获取多个标识的标识映射

使用 `POST` 方法作为批次等效的 `GET` 上述方法检索多个身份的映射。

>[!NOTE]
>
>请求应指示不超过1000个身份。 请求超过1000个标识将导致400个状态代码。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**请求正文**

选项1：提供要检索映射的XID列表。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

选项2：提供身份列表作为复合ID，其中每个身份均按命名空间ID命名ID值和命名空间。 此示例演示在覆盖缺省值时使用此方法 `graph-type` “专用图”的URL名称。

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

如果未找到具有所提供的输入的相关标识，则 `HTTP 204` 返回响应代码时没有内容。

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

- `lastAssociationTime`：输入身份上次与此身份关联的时间戳。
- `regions`：提供 `regionId` 和 `lastAssociationTime` 身份被发现的地方。

## 后续步骤

继续下一教程以 [列出可用的命名空间](./list-namespaces.md).
