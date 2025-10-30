---
keywords: Experience Platform；主页；热门主题；流；流式摄取；流式摄取验证；验证；流式摄取验证；验证；同步验证；同步验证；异步验证；异步验证；
solution: Experience Platform
title: 流式摄取验证
type: Tutorial
description: 流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流式引入API支持两种验证模式 — 同步和异步。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 15%

---

# 流式摄取验证

流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流式引入API支持两种验证模式 — 同步和异步。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md)：将数据发送到[!DNL Experience Platform]的方法之一。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) [!DNL Experience Platform]。

### 收集所需标头的值

为调用 [!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Schema Registry]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- 内容类型： `application/json`

### 验证范围

[!DNL Streaming Validation Service]包括以下方面的验证：

- Range
- 存在
- 枚举
- 模式
- 类型
- 格式

## 同步验证

同步验证是一种验证方法，可提供有关摄取失败原因的即时反馈。 但是，失败时，将丢弃验证失败的记录并阻止将其发送到下游。 因此，同步验证只应在开发过程中使用。 在执行同步验证时，会向调用方通知XDM验证的结果，如果验证失败，还会通知失败原因。

默认情况下，同步验证未打开。 要启用此功能，您必须在进行API调用时传入可选的查询参数`syncValidation=true`。 此外，当前仅当您的流端点位于VA7数据中心时，同步验证才可用。

>[!NOTE]
>
>`syncValidation`查询参数仅适用于单个消息终结点，不能用于批处理终结点。

如果消息在同步验证过程中失败，则不会将该消息写入输出队列，这将为用户提供即时反馈。

>[!NOTE]
>
>架构更改可能并非立即可用，因为已缓存更改。 最多留出15分钟时间刷新缓存。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 之前创建的流连接的`id`值。 |

**请求**

提交以下请求，通过同步验证将数据摄取到您的数据入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 要摄取的数据的JSON正文。 |

**响应**

启用同步验证后，成功的响应会在其有效负载中包含任何遇到的验证错误：

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

上述响应列出了发现了多少方案违规以及违规内容。 例如，此响应声明未在架构中定义键`workEmail`和`person`，因此不允许使用。 它还将`_id`的值标记为不正确，因为架构需要`string`，但插入的是`long`。 请注意，一旦遇到五个错误，验证服务将&#x200B;**停止**&#x200B;处理该消息。 但是，将继续解析其他消息。

## 异步验证

异步验证是一种不会立即提供反馈的验证方法。 而是将数据发送到[!DNL Data Lake]中的失败批次，以防止数据丢失。 可以稍后检索此失败数据以便进一步分析和重放。 此方法应在生产中使用。 除非另有请求，否则流式摄取在异步验证模式下运行。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 之前创建的流连接的`id`值。 |

**请求**

提交以下请求，通过异步验证将数据摄取到您的数据入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 要摄取的数据的JSON正文。 |

>[!NOTE]
>
>无需额外的查询参数，因为默认情况下启用异步验证。

**响应**

启用异步验证后，成功的响应将返回以下内容：

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

请注意，响应中指出已跳过同步验证，因为未明确请求该响应。

## 附录

本节包含有关各种状态代码对摄取数据的响应有何含义的信息。

### 状态代码

| 状态代码 | 它的含义 |
| ----------- | ------------- |
| 200 | 成功。 对于同步验证，这意味着它已经通过了验证检查。 对于异步验证，这意味着它仅成功接收了消息。 用户可以通过观察数据集找到最终的消息状态。 |
| 400 | 错误。 您的请求存在问题。 从流验证服务接收带有更多详细信息的错误消息。 |
| 401 | 错误。 您的请求未获授权 — 您需要使用持有者令牌进行请求。 有关如何请求访问的详细信息，请查看此[教程](https://www.adobe.com/go/platform-api-authentication-en)或此[博客帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。 |
| 500 | 错误。 存在内部系统错误。 |
| 501 | 错误。 这意味着此位置不支持同步验证&#x200B;**&#x200B;**。 |
| 503 | 错误。 该服务当前不可用。 客户端应使用指数回退策略至少重试三次。 |
