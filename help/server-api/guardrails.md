---
title: Edge Network Server API的性能护栏
description: 了解如何在最佳性能护栏中使用服务器API。
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# Edge Network Server API的性能护栏

## 概述 {#overview}

性能护栏定义与服务器API用例相关的使用限制。 超出本文中概述的性能护栏可能会导致性能下降。

Adobe对超出使用限制导致的性能下降不承担任何责任。 始终超过性能护栏的客户可以请求额外的处理容量，以避免性能下降。

>[!IMPORTANT]
>
>除了此护栏页面外，还检查销售订单中的许可证授权和相应的[产品描述](https://helpx.adobe.com/legal/product-descriptions.html)中的实际使用限制。

本页中介绍的所有性能护栏均适用于IMS组织级别。 对于配置了多个IMS组织的用户，每个组织分别遵循以下性能护栏。 有关[!DNL IMS Organizations]的更多详细信息，请参阅[Experience Platform术语表](../landing/glossary.md)。

## 定义

* **可用性**&#x200B;按照每五分钟间隔计算为Experience Platform Edge Network处理的请求的百分比，这些请求不会因错误而失败，并且仅与配置的Edge Network API相关。 如果租户在给定的五分钟间隔内未提出任何请求，则该间隔视为100%可用。
* **给定区域的每月正常运行时间百分比**&#x200B;计算为一个月内所有五分钟间隔的可用性平均值。
* **上游**&#x200B;是Edge Network背后的服务，为特定数据流启用，如Adobe服务器端转发、Adobe Edge Segmentation或Adobe Target。
* **请求单元**&#x200B;对应于请求的8 KB片段，以及为数据流配置的一个上游片段。
* **请求**&#x200B;是客户拥有的应用程序发送给[!DNL Server API]的单个消息。 请求可以包含一个或多个请求单元。
* **错误**&#x200B;是因Edge Network [内部服务错误](error-handling.md)而失败的任何请求。

## 服务限制

所有数据流都强制实施某些使用限制，这些限制主要控制可同时发送的事件数、事件大小和这些请求路由到的上游服务数。

### 请求单位

所有限制都在&#x200B;**请求单元(RU)**&#x200B;上应用并标准化，该请求单元被定义为一个请求的&#x200B;**8 KB片段**，该请求转到数据流中配置的一个上游服务。

#### 示例

| 根据数据流配置的上游 | 平均请求大小 | 请求单位 |
| --- | --- | --- |
| 1 (Adobe Experience Platform) | 8 KB（1个片段） | 1 |
| 2 (Adobe Experience Platform、Adobe Target) | 8 KB（1个片段） | 2 |
| 2 (Adobe Experience Platform、Adobe Target) | 16 KB（2个片段） | 4 |
| 2 (Adobe Experience Platform、Adobe Target) | 64 KB（8个片段） | 16 |

### 请求单位限制

下表显示了默认限制值。 如果您需要更高的请求单位限制，请联系您的客户代表。

| 终结点 | 每秒请求单位数 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |

### HTTP请求大小限制

| 有效负载格式 | 请求的最大大小 | 最大8 KB请求片段 |
| --- | --- | --- |
| JSON纯文本 | 64 KB | 8 |


>[!NOTE]
>
>根据有效负载本身，二进制格式通常比纯文本JSON格式多压缩20-40%，从而允许您推送更多数据。 如果您需要更大的数据流容量，请联系您的客户关怀代表。

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [各种Experience Platform服务的端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C版本 — Prime和Ultimate包)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate包)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate包)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
