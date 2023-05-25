---
keywords: Experience Platform；主页；热门主题；流；流摄取；流摄取验证；验证；流摄取验证；验证；同步验证；同步验证；异步验证；异步验证；
solution: Experience Platform
title: 流摄取验证
type: Tutorial
description: 流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流式引入API支持两种验证模式 — 同步和异步。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 3%

---

# 流式摄取验证

流式摄取允许您使用流式端点实时将数据上传到Adobe Experience Platform。 流式引入API支持两种验证模式 — 同步和异步。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md)：将数据发送到的方法之一 [!DNL Experience Platform].

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括那些属于 [!DNL Schema Registry]，与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type: `application/json`

### 验证范围

[!DNL Streaming Validation Service] 包括以下方面的验证：
- Range
- 存在
- 枚举
- 图案
- 类型
- 格式

## 同步验证

同步验证是一种验证方法，可立即反馈引入失败的原因。 但是，失败时，将丢弃验证失败的记录并阻止将其发送到下游。 因此，应仅在开发过程中使用同步验证。 在执行同步验证时，会向调用方通知XDM验证的结果，如果验证失败，还会告知失败的原因。

默认情况下，不会启用同步验证。 要启用此功能，您必须传入可选查询参数 `syncValidation=true` 进行API调用时。 此外，当前仅当您的流端点位于VA7数据中心上时，同步验证才可用。

>[!NOTE]
>
>此 `syncValidation` 查询参数仅适用于单个消息端点，不能用于批处理端点。

如果消息在同步验证过程中失败，则不会将该消息写入输出队列，这会立即向用户提供反馈。

>[!NOTE]
>
>架构更改可能无法立即使用，因为更改已缓存。 最多允许15分钟刷新缓存。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 之前创建的流连接的值。 |

**请求**

提交以下请求，通过同步验证将数据摄取到数据入口：

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

上述响应列出了发现了多少方案违规以及违规内容。 例如，此响应声明 `workEmail` 和 `person` 架构中未定义，因此不允许使用。 它还标记以下项的值： `_id` 不正确，因为架构需要 `string`，但 `long` 被插入了。 请注意，一旦遇到五个错误，验证服务将 **停止** 正在处理该消息。 但是，其他消息将继续被解析。

## 异步验证

异步验证是一种不会立即提供反馈的验证方法。 相反，数据会发送到中的失败批次 [!DNL Data Lake] 以防止数据丢失。 可以稍后检索此失败的数据以进一步分析和重放。 此方法应在生产中使用。 除非另有请求，否则流式摄取在异步验证模式下运行。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 之前创建的流连接的值。 |

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

启用异步验证后，成功响应将返回以下内容：

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

请注意，响应中如何声明已跳过同步验证，因为未明确请求同步验证。

## 附录

本节包含有关各种状态代码对摄取数据的响应有何含义的信息。

### 状态代码

| 状态代码 | 它的含义 |
| ----------- | ------------- |
| 200 | 成功. 对于同步验证，这意味着它已通过验证检查。 对于异步验证，这意味着它仅成功收到消息。 用户可以通过观察数据集来了解最终的消息状态。 |
| 400 | 错误. 您的请求出错。 从流验证服务接收到带有更多详细信息的错误消息。 |
| 401 | 错误. 您的请求未获授权 — 您需要使用持有者令牌进行请求。 有关如何请求访问的更多信息，请查看此 [教程](https://www.adobe.com/go/platform-api-authentication-en) 或此 [博客帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | 错误. 存在内部系统错误。 |
| 501 | 错误. 这意味着同步验证是 **非** 此位置支持。 |
| 503 | 错误. 该服务当前不可用。 客户端应使用指数回退策略至少重试三次。 |
