---
title: 错误处理
description: 了解在对Adobe Experience PlatformEdge Network服务器API执行API请求时可能遇到的错误。
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---

# 错误处理

## 概述 {#overview}

Adobe Experience PlatformEdge Network服务器API中的API错误可能由多种原因引起，包括内部(Edge Network本身)或外部（输入、配置或上游相关）。

## 错误类型 {#error-types}

| 错误 | 类型 | 描述 | 状态代码 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 内部 | Adobe Experience PlatformEdge Network在意外情况下发出的一般用途错误。 | `500` |
| `InputError` | 外部 | 包含由输入格式错误导致的错误以及实体验证错误。 | `4xx` |
| `ConfigurationError` | 外部 | 服务器端配置错误。 | `422` |
| `UpstreamError` | 外部 | 与上游服务的通信错误。 | `207 Multi-Status` |

## 严重性

服务器API错误也可以按严重程度拆分：

* **致命错误**&#x200B;将停止调度管道。
* **非致命错误**&#x200B;可能表示部分处理，而允许继续处理请求。
   * 如果存在，请求的整体状态代码将更改为`207 Multi-Status`。

| 错误 | 类型 | 备注 |
| --- | --- | --- |
| `RequestProcessingError` | 致命 | 请求处理期间的任何时间点都可能发生这种情况。 |
| `InputError` | 致命 | 接受请求时，在将其调度到上游之前发生。 |
| `ConfigurationError` | 致命 | 接受请求时，在将其调度到上游之前发生。 |
| `UpstreamError` | 非致命 | 与上游服务的通信错误。 |

### 致命错误 {#fatal-errors}

致命错误会停止请求处理，并导致返回非2xx响应状态。 查看[错误类型](#error-types)部分以查看与每个错误类型对应的预期状态代码。

错误将随附包含错误对象的响应正文。 在这种情况下，响应正文包含由[RFC 7807 HTTP API的问题详细信息](https://tools.ietf.org/html/rfc7807)定义的问题详细信息。

返回的内容类型是`application/problem+json`媒体类型。 如果存在，则此响应包含与错误相关的计算机可读详细信息。 问题详细信息包括URI类型。

所有错误对象都具有`type`、`status`、`title`、`detail`和`report`消息属性，以便API客户端能够指出问题所在。

| 属性 | 类型 | 描述 |
| -------- | ------ | ----------- |
| `type` | 字符串 | URI引用(RFC3986)，它按照格式`https://ns.adobe.com/aep/errors/<ERROR-CODE>`标识问题类型。 |
| `status` | 数值 | 服务器为此问题的发生生成的HTTP状态代码。 |
| `title` | 字符串 | 易于用户识别的简短问题类型摘要。 |
| `detail` | 字符串 | 易于用户识别的问题类型简短描述。 |
| `report` | 对象 | 有助于进行调试的其他属性的映射，例如请求ID或组织ID。 在某些情况下，它可能包含特定于手头错误的数据，例如验证错误列表。 |

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

非致命错误可进一步细分为：

* 错误：处理请求时出现问题，但未导致整个请求被拒绝(例如， 非关键上游故障)。
* 警告：来自上游服务的消息，这可能表示发生了请求的部分处理。

遇到非致命错误（不包括警告）时，[!DNL Server API]会将响应状态更改为`207 Multi-Status`。

另一方面，警告大多是信息性的，因为它们通常表示潜在的临时情况，不会完全影响请求。 以下示例是分段引擎中读取的部分用户档案，在这种情况下，准确性在一定程度上受到影响，但功能仍然可用。

非致命错误以&#x200B;_问题详细信息_&#x200B;格式表示，但直接嵌入到Edge网关的`application/json`类型的标准响应中。

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

## 处理`4xx`和`5xx`响应

| 错误代码 | 描述 |
|---|---|
| `4xx Bad Request` | 除`429`外，不应代表客户端重试大多数`4xx`错误，如400、403、404。 这些是客户端错误，将不会成功。 客户端必须解决该错误才能重试请求。 |
| `429 Too Many Requests` | `429` HTTP响应代码指示Adobe Experience PlatformEdge Network或上游服务正在限制请求的速率。 在这种情况下，调用方必须遵守`Retry-After`响应标头。 任何回流的响应都必须携带带有特定于域错误代码的HTTP响应代码。 |
| `500 Internal Server Error` | `500`个错误是一般性错误，捕获所有错误。 不得重试`500`个错误，`502`和`503`除外。 中介必须以`500`错误响应，并且可能会以通用错误代码/消息或特定于域的错误代码/消息响应。 |
| `502 Bad Gateway` | 指示Adobe Experience PlatformEdge Network从上游服务器接收到无效的响应。 由于服务器之间的网络问题，可能发生这种情况。 临时网络问题可能会解决，因此重试可能会解决该问题，因此`502`错误的收件人可能会在一段时间后重试该请求。 |
| `503 Service Unavailable` | 此错误代码表示服务暂时不可用。 这可能发生在维护期间。 `503`错误的收件人可以重试请求，但必须遵守`Retry-After`标头。 |
| `504 Gateway Timeout` | 指示对上游服务器的Adobe Experience PlatformEdge Network请求已超时。 这可能是由于服务器之间的网络问题、DNS问题或其他网络问题造成的。 临时网络问题可能会在一段时间后得到解决，重试可能会解决此问题。 |
