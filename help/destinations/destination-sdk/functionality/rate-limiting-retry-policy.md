---
description: 了解Experience Platform如何处理流式目标返回的各种类型的错误，以及如何重试将数据发送到目标平台。
title: 使用Destination SDK构建的流目标的速率限制和重试策略
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 使用Destination SDK构建的流目标的速率限制和重试策略

合作伙伴构建的目标可能会返回各种错误，并且具有不同的速率限制策略。 本页说明Experience Platform如何处理流目标返回的各种类型的错误。

使用Destination SDK配置目标时，您可以在两种聚合类型之间进行选择 —  [最大努力聚合](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 和 [可配置聚合](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). 根据您选择的聚合类型，请阅读下面的Experience Platform如何处理错误和速率限制。

## 最大努力聚合 {#best-effort-aggregation}

对于向目标发起的失败任何HTTP调用，Experience Platform都会尝试在首次调用后立即再次发起调用。 如果调用在第二次尝试时仍然失败，则Experience Platform将丢弃该调用，并且不会第三次重新尝试它。

## 可配置的聚合 {#configurable-aggregation}

对于使用可配置聚合设置的目标平台，Experience Platform会区分平台返回的错误类型：

* Experience Platform重试将数据发送到您的平台的错误：
   * HTTP响应代码420和429
   * HTTP响应代码大于500
* Experience Platform的错误 *不会* 重试将数据发送到平台：平台返回的所有其他数据

### 已描述重试方法 {#retry-approach}

下面介绍了用于可配置聚合的Experience Platform方法。 此示例假定Experience Platform向目标平台发送数据，如果每分钟收到超过50,000个请求，则该平台开始返回429错误代码：

* 第1分钟：Experience Platform汇总40,000个批次和配置文件，以发送到您的目标平台。 Experience Platform发出40,000个HTTP请求，并且所有请求都成功。
* 第2分钟：Experience Platform汇总70,000个批次和配置文件，以发送到您的目标平台。 Experience Platform发出70,000个HTTP请求，成功50,000个。 其他20k从您的端点收到速率限制错误，将在30分钟后重新尝试。
* 第3分钟：Experience Platform汇总30,000个批次和配置文件，以发送到您的目标平台。 Experience Platform发出30,000个HTTP请求，并且所有请求都成功。
* ...
* ...
* 第32分钟：Experience Platform再次尝试发送在第2分钟失败的20,000批次。 所有调用均成功。

## 后续步骤 {#next-steps}

您现在知道Experience Platform如何处理来自目标平台的错误和速率限制，具体取决于您在配置流目标时选择的聚合策略。 接下来，您可以查看以下文档：

* [测试目标配置](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交在Destination SDK中创作的目标以供审查](../guides/submit-destination.md)
