---
title: 服务级别协议和目标
description: 了解如何为边缘网络服务器API配置身份验证
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: 数据收集；收集；边缘网络；API;SLA;SLT；服务级别
hide: true
hidefromtoc: true
source-git-commit: 50a688e2f19f4fda2fc4cca823edb5886ad32bba
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# 护栏

## 概述 {#overview}

Adobe将利用商业上合理的努力来 [!DNL Server API] 在任何月度账单周期内，每个地区在每月正常运行时间百分比内至少为99.9%。

## 定义

* **可用性** 计算为每五分钟的间隔，该间隔是由Experience Adobe Experience Platform边缘网络处理的请求中不会因错误而失败且仅与已配置的Adobe Experience Platform边缘网络API相关的百分比。 如果租户在给定的五分钟间隔内未发出任何请求，则该间隔将被视为100%可用。
* **每月正常运行时间百分比** 对于给定区域，计算为每月所有五分钟间隔的可用性平均值。
* 安 **上游** 是Adobe Edge网络后面的一项服务，为特定数据流(如Adobe服务器端转发、Adobe Edge分段或Adobe Target)启用。
* A **请求** 发送到服务器API的请求单元被定义为一个或多个请求单元。
* A **请求单元** 对应于请求的8 KB片段和为数据流配置的一个上游片段。
* 安 **错误** 是因Adobe Experience Platform边缘网络而失败的任何请求 [内部服务错误](error-handling.md).

## 内部目标

Adobe工程团队部署了接近实时遥测、监控和扩展程序，以确保实现以下目标：

* 返回的HTTP请求少于1% `5xx` 最近五分钟的错误
* 不到1%的上游连接在过去五分钟内返回错误
* 任何租户容量在达到限制后不到10分钟内翻倍。

## 服务级别协议排除

上述服务级别承诺不适用于以下事件导致的任何不可用或性能问题：

* 超出我们合理控制范围的因素，包括Internet访问或Adobe基础设施之外的相关问题。
* 任何 [!DNL Server API]，具体定义如下所列的限制。

## 服务限制

所有数据流都强制实施某些使用限制，这主要控制可并发发送的事件数、事件大小以及这些请求路由到的上游服务数量。

### 请求单位

所有限制都会在 **请求单元(RU)**，定义为 **8 KB片段** 向数据流中配置的一个上游服务发出的请求。

#### 示例

| 按数据流配置的上流 | 平均请求大小 | 请求单位 |
| --- | --- | --- |
| 1(Adobe平台) | 8 KB（1个片段） | 1 |
| 2(Adobe平台，Adobe Target) | 8 KB（1个片段） | 2 |
| 2(Adobe平台，Adobe Target) | 16 KB（2个片段） | 4 |
| 2(Adobe平台，Adobe Target) | 64 KB（8个片段） | 16 |

### 请求单位限制

下表显示了默认限制值。 如果您需要提高请求单位限制，请联系您的客服专员。

| 端点 | 每秒请求数 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### HTTP请求大小限制

| 负载格式 | 请求的最大大小 | 最多8 KB请求片段 |
| --- | --- | --- |
| JSON纯文本 | 64KB | 8 |


>[!NOTE]
>
>根据有效负载本身，二进制格式通常比纯文本JSON格式紧凑20-40%，从而允许您推送更多数据。 如果您需要更大的数据流容量，请联系您的客户关怀代表。

