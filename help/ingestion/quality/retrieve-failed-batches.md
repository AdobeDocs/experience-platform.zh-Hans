---
keywords: Experience Platform;home;popular topics;retrieve failed batches;failed batches;batch ingestion;Batch ingestion;Failed batches;Get failed batches;get failed batches;Download failed batches;download failed batches;
solution: Experience Platform
title: 检索失败的批
topic: tutorial
type: Tutorial
description: 本教程介绍了使用数据摄取API检索有关失败批次的信息的步骤。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---


# 使用API检索失败的批

Adobe Experience Platform提供两种上传和摄取数据的方法。 您可以使用批处理摄取，它允许您使用各种文件类型（如CSV）插入其数据；或者使用流式摄取，它允许您使用流式端点将 [!DNL Platform] 其数据实时插入。

本教程介绍了使用API检索有关失败批次的信息的 [!DNL Data Ingestion] 步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Data Ingestion]](../home.md):发送数据的方 [!DNL Experience Platform]法

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Schema Registry]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型： `application/json`

### 失败批处理示例

本教程将使用格式不正确的时间戳的示例数据，该时间戳将月值设 **置为** 00，如下所示：

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

由于时间戳格式错误，上述负载无法针对XDM模式进行正确验证。

## 检索失败的批

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批的ID。 |

**请求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

通过上述响应，您可以看到批处理的哪些块成功和失败。 从此响应中，您可以看到文件包 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 含失败的批。

## 下载失败的批

一旦知道批处理中的哪个文件失败，您就可以下载失败的文件并查看错误消息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失败文件的批处理的ID。 |
| `{FAILED_FILE}` | 格式化失败的文件的名称。 |

**请求**

以下请求允许您下载包含摄取错误的文件。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

由于上一个摄取的批次的日期时间无效，因此将显示以下验证错误。

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

阅读本教程后，您学习了如何从失败的批中检索错误。 有关批量摄取的详细信息，请阅读批 [量摄取开发人员指南](../batch-ingestion/overview.md)。 有关流摄取的更多信息，请阅读 [创建流连接教程](../tutorials/create-streaming-connection.md)。

## 附录

本节包含可能发生的其他摄取错误类型的相关信息。

### 格式不正确的XDM

与上一个示例流中的时间戳错误一样，这些错误是由于格式不正确的XDM造成的。 这些错误消息会因问题的性质而异。 因此，不能显示特定错误示例。

### 缺少IMS组织ID或无效

如果有效负荷中缺少IMS组织ID，则显示此错误。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### 缺少XDM模式

如果缺少的 `schemaRef` 错误，则 `xdmMeta` 显示此错误。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 缺少源名称

如果标题中缺少 `source` 此错误，则显示此错误 `name`。

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

如果不存在，则显示此 `xdmEntity` 错误。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
