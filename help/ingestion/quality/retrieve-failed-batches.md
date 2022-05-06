---
keywords: Experience Platform；主页；热门主题；检索失败的批次；失败的批次；批量摄取；失败的批次；获取失败的批次；获取失败的批次；下载失败的批次；下载失败的批次；
solution: Experience Platform
title: 使用数据访问API检索失败的批次
topic-legacy: tutorial
type: Tutorial
description: 本教程介绍了使用数据摄取API检索有关失败批次的信息的步骤。
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# 使用数据访问API检索失败的批次

Adobe Experience Platform提供了两种上传和摄取数据的方法。 您可以使用批量摄取(允许您使用各种文件类型（如CSV）插入其数据)，或使用流式摄取(允许您将其数据插入到 [!DNL Platform] 实时使用流端点。

本教程介绍使用 [!DNL Data Ingestion] API。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
- [[!DNL Data Ingestion]](../home.md):将数据发送到的方法 [!DNL Experience Platform].

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Schema Registry]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- `Content-Type: application/json`

### 失败的批次示例

本教程将使用格式不正确的时间戳的示例数据，该时间戳将月值设置为 **00**，如下所示：

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

由于时间戳格式错误，上述负载无法针对XDM架构进行正确验证。

## 检索失败的批处理

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批次的ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

通过上述响应，您可以看到批处理中的哪些区块成功和失败。 从此响应中，您可以看到该文件 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 包含失败的批次。

## 下载失败的批处理

在知道批处理中哪个文件失败后，您可以下载失败的文件并查看错误消息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失败文件的批处理的ID。 |
| `{FAILED_FILE}` | 格式失败的文件的名称。 |

**请求**

以下请求允许您下载存在摄取错误的文件。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

由于上一个摄取的批处理的日期时间无效，因此将显示以下验证错误。

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## 后续步骤

阅读本教程后，您学习了如何从失败的批次中检索错误。 有关批量摄取的更多信息，请阅读 [批量获取开发人员指南](../batch-ingestion/overview.md). 有关流式摄取的更多信息，请阅读 [创建流连接教程](../tutorials/create-streaming-connection.md).

## 附录

此部分包含可能发生的其他摄取错误类型的信息。

### 格式不正确的XDM

与上一个示例流中的时间戳错误一样，这些错误是由于XDM格式不正确所致。 这些错误消息会因问题的性质而异。 因此，无法显示任何特定错误示例。

### 缺少或无效的IMS组织ID

如果有效负载中缺少IMS组织ID，则会显示此错误。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### 缺少XDM架构

如果 `schemaRef` 对于 `xdmMeta` 缺少。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 缺少源名称

如果 `source` 标题中缺少 `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### 缺少XDM实体

如果没有 `xdmEntity` 礼物。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
