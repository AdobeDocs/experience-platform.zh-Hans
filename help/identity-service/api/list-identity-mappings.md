---
keywords: Experience Platform；主页；热门主题；标识；标识
solution: Experience Platform
title: 列表身份映射
topic: API guide
description: 映射是指定命名空间的群集中所有标识的集合。
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# 列表身份映射

映射是指定命名空间的群集中所有标识的集合。

## 获取单个标识的标识映射

给定身份，从请求中由身份表示的同一命名空间检索所有相关身份。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**请求**

选项1:将标识作为命名空间（`nsId`，按ID）和ID值(`id`)提供。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项2:将标识作为命名空间（`ns`，按名称）和ID值(`id`)提供。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项3:提供XID身份(`xid`)。 有关如何获取身份的XID的详细信息，请参阅此文档中覆盖[获取身份的XID的部分](./list-native-id.md)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 获取多个身份的身份映射

将`POST`方法用作上述`GET`方法的批处理等效项，以检索多个标识的映射。

>[!NOTE]
>
>请求应最多指明1000个身份。 超过1000个身份的请求将生成400个状态代码。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**请求主体**

选项1:提供要检索映射的XID列表。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

选项2:提供身份列表作为复合ID，其中每个ID都按命名空间ID命名ID值和命名空间。 此示例演示如何在覆盖“专用图”的默认`graph-type`时使用此方法。

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
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
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

如果没有找到与提供的输入相关的标识，则返回没有内容的`HTTP 204`响应代码。

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

- `lastAssociationTime`:输入标识上次与此标识关联的时间戳。
- `regions`:提供 `regionId` 身 `lastAssociationTime` 份的显示位置。

## 后续步骤

进入下一个教程，学习[列表可用命名空间](./list-namespaces.md)。
