---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 预览
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 预览开发人员指南

介绍

- 创建新预览
- 检索特定预览的结果
- 取消或删除特定预览

## 入门指南

本指南中使用的API端点是分段API的一部分。 在继续之前，请查阅分段开 [发人员指南](./getting-started.md)。

特别是，分段开 [发人员指南的入门部分](./getting-started.md#getting-started) ，包括相关主题的链接、在文档中阅读示例API调用的指南，以及成功调用任何Experience Platform API所需的标题的重要信息。

## 创建新预览

您可以通过向端点发出POST请求来创建新预览 `/preview` 。

**API格式**

```http
POST /preview
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

body info

**响应**

成功的响应会返回HTTP状态201（已创建），其中包含您新创建的预览的详细信息。

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

响应信息，x-location不存在。

## 检索特定预览的结果

您可以通过向端点发出GET请求并在请求路径中提供预览值来检索有关 `/preview` 特定预览的 `id` 详细信息。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`:要 `id` 检索的预览的值。

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含有关指定预览的详细信息。

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## 取消或删除特定预览

您可以通过向端点发出DELETE请求并在请求路径中提 `/preview` 供预览值来删除特 `id` 定预览。

**API格式**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` 要 `id` 删除的预览的值。

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并显示以下消息：

```json
{
  "status": true,
  "message": "KILLED"
}
```

## 后续步骤
