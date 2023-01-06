---
keywords: Experience Platform；主页；热门主题；流；流式引入；流式引入验证；验证；流式引入验证；验证；同步验证；同步验证；异步验证；异步验证；
solution: Experience Platform
title: 流式摄取验证
type: Tutorial
description: 流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流摄取API支持两种验证模式 — 同步和异步。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 3%

---

# 流式摄取验证

流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流摄取API支持两种验证模式 — 同步和异步。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md):将数据发送到的方法之一 [!DNL Experience Platform].

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Schema Registry]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type: `application/json`

### 验证范围

[!DNL Streaming Validation Service] 涵盖以下方面的验证：
- Range
- 存在
- 枚举
- 图案
- 类型
- 格式

## 同步验证

同步验证是一种验证方法，可提供有关摄取失败原因的即时反馈。 但是，失败时，验证失败的记录会被丢弃，并阻止下游发送。 因此，只应在开发过程中使用同步验证。 进行同步验证时，将通知呼叫者XDM验证的结果，如果验证失败，则还将告知失败原因。

默认情况下，不会打开同步验证。 要启用此查询，必须传入可选查询参数 `syncValidation=true` 进行API调用时。 此外，当前，仅当流端点位于VA7数据中心时，才可使用同步验证。

>[!NOTE]
>
>的 `syncValidation` 查询参数仅适用于单个消息端点，不能用于批处理端点。

如果消息在同步验证期间失败，则消息将不会写入输出队列，从而为用户提供即时反馈。

>[!NOTE]
>
>由于已缓存更改，因此架构更改可能不会立即可用。 最长需要15分钟才能刷新缓存。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 之前创建的流连接的值。 |

**请求**

提交以下请求，以通过同步验证将数据摄取到数据入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 要摄取的数据的JSON正文。 |

**响应**

启用同步验证后，成功响应的有效负载中包含遇到的任何验证错误：

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

上述响应列出了发现的架构违规数量以及违规的数量。 例如，此响应声明键 `workEmail` 和 `person` 未在架构中定义，因此不允许。 它还会标记 `_id` 不正确，因为架构需要 `string`，但 `long` 的值。 请注意，遇到5个错误后，验证服务将 **stop** 正在处理该消息。 但是，其他消息将继续进行解析。

## 异步验证

异步验证是一种不提供即时反馈的验证方法。 相反，数据会在 [!DNL Data Lake] 以防止数据丢失。 稍后可以检索此失败数据，以便进一步分析和重播。 此方法应用于生产中。 除非另有请求，否则流摄取在异步验证模式下运行。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 之前创建的流连接的值。 |

**请求**

通过异步验证提交以下请求，将数据摄取到数据入口：

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
>由于默认启用异步验证，因此不需要额外的查询参数。

**响应**

启用异步验证后，成功的响应会返回以下内容：

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

请注意响应如何声明已跳过同步验证，因为尚未明确请求同步验证。

## 附录

本节包含有关各种状态代码对于摄取数据的响应意味着什么的信息。

### 状态代码

| 状态代码 | 这是什么意思 |
| ----------- | ------------- |
| 200 | 成功. 对于同步验证，这意味着它已通过验证检查。 对于异步验证，这意味着它仅成功接收了消息。 用户可以通过观察数据集来查找最终的消息状态。 |
| 400 | 错误. 你的请求有问题。 从流验证服务中接收了包含更多详细信息的错误消息。 |
| 401 | 错误. 您的请求未授权 — 您将需要使用载体令牌请求。 有关如何请求访问权限的更多信息，请参阅此 [教程](https://www.adobe.com/go/platform-api-authentication-en) 或 [博客帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | 错误. 出现内部系统错误。 |
| 501 | 错误. 这意味着同步验证 **not** 支持此位置。 |
| 503 | 错误. 服务当前不可用。 客户端应使用指数回退策略至少重试3次。 |
