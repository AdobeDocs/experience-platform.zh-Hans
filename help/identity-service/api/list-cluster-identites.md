---
keywords: Experience Platform；主页；热门主题；列表身份；列表群集
solution: Experience Platform
title: 列出群集中的所有标识
description: 在身份图表中关联的身份（无论是否具有命名空间）被视为该身份图表中同一“集群”的一部分。 以下选项提供了访问所有群集成员的方法。
role: Developer
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 列出群集中的所有身份

在身份图表中关联的身份（无论是否具有命名空间）被视为该身份图表中同一“集群”的一部分。 以下选项提供了访问所有群集成员的方法。

## 获取单个标识的关联标识

检索单个标识的所有群集成员。

您可以使用可选的 `graph-type` 指示从中获取集群的身份图的参数。 选项包括：

- 无 — 不执行身份拼接。
- 专用图 — 根据专用身份图执行身份拼接。 如果否 `graph-type` （这是默认设置）。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**请求**

选项1：以命名空间形式提供身份(`nsId`，按ID)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项2：以命名空间形式提供身份(`ns`，按名称)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

选项3：以XID形式提供身份(`xid`)。 有关如何获取身份的XID的更多信息，请参阅本文档中涵盖的部分 [获取标识的XID](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## 获取多个标识的关联标识

使用 `POST` 作为批次等效项 `GET` 上述方法用于返回多个身份群集中的身份。

>[!NOTE]
>
>请求应指示不超过1000个身份。 请求超过1000个标识将导致400个状态代码。

**API格式**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**请求**

以下请求演示了如何提供要检索群集成员的XID列表。

**存根请求**

使用 `x-uis-cst-ctx: stub` 标头将返回存根响应。 这是一个临时解决方案，可在服务完成时帮助早期集成开发进度。 当不再需要时，此选项将被弃用。

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**使用XID调用**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}' | json_pp
```

**使用UID调用**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
    "graph-type": "Private Graph"
}' | json_pp
```

**响应**

**“已存根”响应**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**完整响应**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>对于请求中提供的每个XID，响应将始终有一个对应的条目，而不管请求的XID是否属于同一集群，或者是否有一个或多个集群根本没有关联。

## 后续步骤

继续下一教程以 [列出标识的群集历史记录](./list-cluster-history.md)
