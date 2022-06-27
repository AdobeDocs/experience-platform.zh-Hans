---
title: 错误处理
description: 了解在对Adobe Experience Platform边缘网络服务器API执行API请求时可能遇到的错误。
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# 错误处理

## 概述 {#overview}

Adobe Experience Platform Edge Network Server API中的API错误可能有多种原因，包括内部（边缘网络本身）或外部（输入、配置或上游相关）。

## 错误类型 {#error-types}

| 错误 | 类型 | 描述 | 状态代码 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 内部 | Adobe Experience Platform边缘网络在意外情况下发出通用错误。 | `500` |
| `InputError` | 外部 | 包括由于输入格式不正确导致的错误以及实体验证错误。 | `4xx` |
| `ConfigurationError` | 外部 | 服务器端配置错误。 | `422` |
| `UpstreamError` | 外部 | 上游服务的通信错误。 | `207 Multi-Status` |

## 严重性

服务器API错误也可按严重性进行拆分：

* **致命错误** 将停止调度管道。
* **非致命错误** 可能会发出部分处理信号，同时允许请求处理继续。
   * 如果存在，请求的整体状态代码将更改为 `207 Multi-Status`.

| 错误 | 类型 | 备注 |
| --- | --- | --- |
| `RequestProcessingError` | 致命 | 在请求处理期间，可以在任意时刻发生。 |
| `InputError` | 致命 | 在上游调度请求之前接受请求时发生。 |
| `ConfigurationError` | 致命 | 在上游调度请求之前接受请求时发生。 |
| `UpstreamError` | 非致命 | 上游服务的通信错误。 |

### 致命错误 {#fatal-errors}

严重错误会停止请求处理并导致返回非2xx响应状态。 查看 [错误类型](#error-types) 部分以查看与每个错误类型对应的预期状态代码。

错误将伴随包含错误对象的响应正文。 在这种情况下，响应主体包含问题详细信息，定义如下 [RFC 7807 HTTP API问题详细信息](https://tools.ietf.org/html/rfc7807).

返回的content-type是 `application/problem+json` 媒体类型。 如果存在，则此响应包含与错误相关的计算机可读详细信息。 问题详细信息包括URI类型。

所有错误对象都具有 `type`, `status`, `title`, `detail` 和 `report` 消息属性，以便API客户端能够判断问题出在何处。

| 属性 | 类型 | 描述 |
| -------- | ------ | ----------- |
| `type` | 字符串 | URI引用(RFC3986)，它按照格式标识问题类型 `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | 数值 | 服务器为此问题生成的HTTP状态代码。 |
| `title` | 字符串 | 问题类型的简短、人类可读的摘要。 |
| `detail` | 字符串 | 问题类型的简短、人类可读的描述。 |
| `report` | 对象 | 有助于进行调试的其他属性的映射，如请求ID或组织ID。 在某些情况下，它可能包含特定于手头错误的数据，如验证错误列表。 |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### 非致命错误 {#non-fatal-errors}

非致命错误可进一步划分为：

* 错误：处理请求时发生的问题，但并未导致整个请求被拒绝(例如 非关键上游故障)。
* 警告：来自上游服务的消息，该消息可能表示请求已进行部分处理。

遇到非致命错误（不包括警告）时， [!DNL Server API] 将响应状态更改为 `207 Multi-Status`.

另一方面，警告大多是信息性的，因为它们通常代表一种可能短暂的情况，不会完全影响请求。 以下示例是在分段引擎中读取的部分配置文件，在这种情况下，准确性会受到一定程度的影响，但功能仍然可以提供。

在 _问题详细信息_ 格式，但直接嵌入到Edge网关的标准响应中，该响应类型为 `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## 处理 `4xx` 和 `5xx` 响应


| 错误代码 | 描述 |
|---|---|
| `4xx Bad Request` | 最多 `4xx` 错误（如400、403、404）不应代表客户端重试，但 `429`. 这些是客户端错误，不会成功。 客户端必须先解决错误，然后才能重试请求。 |
| `429 Too Many Requests` | `429` HTTP响应代码指示Adobe Experience Platform边缘网络或上游服务速率限制请求。 在这种情况下，呼叫者必须遵守 `Retry-After` 响应标头。 返回的任何响应都必须包含具有域特定错误代码的HTTP响应代码。 |
| `500 Internal Server Error` | `500` 错误是通用的、全部捕获的错误。 `500` 除 `502` 和 `503`. 中介机构必须通过 `500` 错误，可能会做出响应，显示通用错误代码/消息，或更多特定于域的错误代码/消息。 |
| `502 Bad Gateway` | 表示Adobe Experience Platform边缘网络收到来自上游服务器的无效响应。 这可能是由于服务器之间存在网络问题所致。 临时网络问题可能会解决，因此重试可能会解决该问题，因此的收件人 `502` 错误可能会在一段时间后重试请求。 |
| `503 Service Unavailable` | 此错误代码表示服务暂时不可用。 在维护期间可能会发生这种情况。 收件人 `503` 错误可能会重试请求，但必须遵循 `Retry-After` 标题。 |
| `504 Gateway Timeout` | 表示对上游服务器的Adobe Experience Platform边缘网络请求已超时。 这可能是由于服务器之间的网络问题、DNS问题或其他网络问题所致。 临时网络问题可能会在一段时间后得到解决，重试可能会解决此问题。 |
