---
title: Edge Network服务器API的性能护栏
description: 了解如何在最佳性能护栏中使用服务器API。
keywords: 数据收集；收集；Edge Network；API；SLA；SLT；服务级别
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 0e609ce278af0c93503f05778887ad1bd881524a
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Edge Network服务器API的性能护栏

## 概述 {#overview}

性能护栏定义与服务器API用例相关的使用限制。 超出本文中概述的性能护栏可能会导致性能下降。

Adobe对超出使用限制导致的性能下降不承担任何责任。 始终超过性能护栏的客户可以请求额外的处理容量，以避免性能下降。

## 定义

* **可用性** 每隔五分钟计算一次，计算一次Experience Platform边缘网络处理的请求百分比，这些请求不会因错误而失败，且仅与配置的边缘网络API相关。 如果租户在给定的五分钟间隔内未提出任何请求，则该间隔视为100%可用。
* **每月正常运行时间百分比** 对于给定区域，计算为一个月内所有五分钟间隔的可用性的平均值。
* An **上游** 是Edge Network之后的服务，为特定数据流启用，如Adobe服务器端转发、Adobe Edge Segmentation或Adobe Target。
* A **请求单位** 对应于请求的8 KB片段，以及为数据流配置的一个上游。
* A **请求** 是客户拥有的应用程序发送给 [!DNL Server API]. 请求可以包含一个或多个请求单元。
* An **错误** 是因边缘网络而失败的任何请求 [内部服务错误](error-handling.md).

## 服务限制

所有数据流都强制实施某些使用限制，这些限制主要控制可同时发送的事件数、事件大小和这些请求路由到的上游服务数。

### 请求单位

所有限制都在 **请求单位(RU)**，定义为 **8 KB片段** 请求发送到数据流中配置的一个上游服务。

#### 示例

| 根据数据流配置的上游 | 平均请求大小 | 请求单位 |
| --- | --- | --- |
| 1(Adobe平台) | 8 KB（1个片段） | 1 |
| 2 (Adobe平台，Adobe Target) | 8 KB（1个片段） | 2 |
| 2(Adobe平台、Adobe Target) | 16 KB（2个片段） | 4 |
| 2(Adobe平台、Adobe Target) | 64 KB（8个片段） | 16 |

### 请求单位限制

下表显示了默认限制值。 如果您需要更高的请求单位限制，请联系您的客户代表。

| 端点 | 每秒请求单位数 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### HTTP请求大小限制

| 有效负载格式 | 请求的最大大小 | 最大8 KB请求片段 |
| --- | --- | --- |
| JSON纯文本 | 64KB | 8 |


>[!NOTE]
>
>根据有效负载本身，二进制格式通常比纯文本JSON格式多压缩20-40%，从而允许您推送更多数据。 如果您需要更大的数据流容量，请联系您的客户关怀代表。

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用于各种Experience Platform服务。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P — 主要和最终包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
