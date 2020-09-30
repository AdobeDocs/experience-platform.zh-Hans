---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;streaming ingestion validation;validation;Streaming ingestion validation;validate;Synchronous validation;synchronous validation;Asynchronous validation;asynchronous validation;
solution: Experience Platform
title: 流式摄取验证
topic: tutorial
type: Tutorial
description: 流摄取允许您使用流端点实时将数据上传到Adobe Experience Platform。 流式摄取API支持两种验证模式——同步和异步。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---


# 流式摄取验证

流摄取允许您使用流端点实时将数据上传到Adobe Experience Platform。 流式摄取API支持两种验证模式——同步和异步。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

- [[!DNL体验数据模型(XDM)系统]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL流摄取]](../streaming-ingestion/overview.md):数据发送方法之一 [!DNL Experience Platform]。

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

### 验证覆盖

[!DNL Streaming Validation Service] 包括以下方面的验证：
- 范围
- 存在
- 枚举
- 图案
- 类型
- 格式

## 同步验证

同步验证是一种验证方法，可提供有关摄取失败原因的即时反馈。 但是，失败后，将删除失败验证的记录，并阻止其向下游发送。 因此，同步验证只应在开发过程中使用。 执行同步验证时，将告知调用方XDM验证的结果，如果验证失败，还将告知失败原因。

默认情况下，不启用同步验证。 要启用它，在进行API调用时必须传入可选 `synchronousValidation=true` 的查询参数。 此外，当前仅在流端点位于VA7数据中心时，同步验证才可用。

如果消息在同步验证期间失败，则消息不会写入输出队列，该队列为用户提供即时反馈。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前 `id` 创建的流连接的值。 |

**请求**

提交以下请求，通过同步验证将数据引入数据入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要收录的数据的JSON主体。 |

**响应**

启用同步验证后，成功的响应在其有效负荷中包含遇到的任何验证错误：

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

上述响应列表发现了多少模式违规，以及哪些违规。 例如，此响应声明在模式 `workEmail` 中 `person` 未定义键和键，因此不允许。 它还将值标记为不 `_id` 正确，因为模式需要 `string`，但 `long` 是插入了。 请注意，遇到五个错误后，验证服务将停 **止处** 理该消息。 但是，其他消息将继续进行解析。

## 异步验证

异步验证是一种验证方法，不提供即时反馈。 相反，数据将发送到失败的批处理，以 [!DNL Data Lake] 防止数据丢失。 此失败的数据稍后可以检索以进一步分析和重放。 该方法应用于生产。 除非另有请求，否则流摄取在异步校验模式下运行。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前 `id` 创建的流连接的值。 |

**请求**

通过异步验证提交以下请求以将数据引入数据入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要收录的数据的JSON主体。 |

>[!NOTE]
>
>不需要额外的查询参数，因为默认情况下启用异步验证。

**响应**

启用异步验证后，成功的响应将返回以下内容：

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

请注意响应如何表示已跳过同步验证，因为尚未明确请求同步验证。

## 附录

本节包含有关各种状态代码对于接收数据的响应意味着什么的信息。

### 状态代码

| 状态代码 | 它意味着什么 |
| ----------- | ------------- |
| 200 | 成功. 对于同步验证，这意味着它已通过验证检查。 对于异步验证，这意味着它仅成功接收了消息。 用户可以通过观察数据集来了解最终消息状态。 |
| 400 | 错误. 你的请求有问题。 从流验证服务中接收包含更多详细信息的错误消息。 |
| 401 | 错误. 您的请求未经授权——您需要使用不记名令牌请求。 有关如何请求访问的更多信息，请阅读本教 [程](../../tutorials/authentication.md) 或本博 [客文章](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。 |
| 500 | 错误. 内部系统错误。 |
| 501 | 错误. 这意味着此位置不 **支持** 同步验证。 |
| 503 | 错误. 服务当前不可用。 客户端应使用指数退避策略至少重试三次。 |