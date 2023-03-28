---
keywords: Experience Platform；主页；热门主题；流程服务；
title: 使用流服务API草拟数据流
description: 了解如何使用流服务API将数据流设置为草稿状态。
badge: label="New Feature" type="Poritive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 使用流服务API草拟数据流

在使用流量服务API时，通过提供 `mode=draft` 查询参数。 草稿稍后可以更新为新信息，准备就绪后即可发布。 本教程介绍了使用流服务API将数据流设置为草稿状态的步骤。

## 快速入门

本教程要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 先决条件

本教程要求您已经生成创建数据流所需的资产。 这包括：

* 已验证的基连接
* 源连接
* 目标XDM架构
* 目标数据集
* 目标连接
* 映射

如果您还没有这些值，请从 [源概述中的目录](../../home.md). 然后，按照给定源的说明生成起草数据流所需的资产。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 将数据流设置为草稿状态

以下各节概述了将数据流设置为草稿、更新数据流、发布数据流以及最终删除数据流的过程。

### 起草数据流

要将数据流设置为草稿，请向 `/flows` 端点 `mode=draft` 作为查询参数。 这允许您创建数据流并将其另存为草稿。

**API格式**

```http
POST /flows?mode=draft
```

| 参数 | 描述 |
| --- | --- |
| `mode` | 用户提供的查询参数，用于确定数据流的状态。 要将数据流设置为草稿，请设置 `mode` to `draft`. |

**请求**

以下请求将创建草稿数据流。

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**响应**

成功的响应会返回 `id` 和对应的 `etag` 数据流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 更新数据流

要更新草稿，请向 `/flows` 端点，同时提供要更新的数据流的ID。 在此步骤中，您还必须提供 `If-Match` 标头参数，与 `etag` 要更新的数据流。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下请求将映射转换添加到起草的数据流。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**响应**

成功的响应会返回您的流ID和 `etag`. 要验证更改，您可以向 `/flows` 端点。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 发布数据流

草稿准备好发布后，向POST `/flows` 端点，同时提供要发布的草稿数据流的ID以及用于发布的操作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 参数 | 描述 |
| --- | --- |
| `op` | 更新查询数据流状态的操作操作。 要发布草稿数据流，请设置 `op` to `publish`. |

**请求**

以下请求会发布您的草稿数据流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回ID和相应的 `etag` 数据流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 删除数据流

要删除数据流，请向 `/flows` 端点。 有关如何使用流服务API删除数据流的详细步骤，请阅读 [在API中删除数据流](./delete-dataflows.md).