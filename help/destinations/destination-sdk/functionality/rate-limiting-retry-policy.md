---
description: 了解Experience Platform如何处理流目标返回的各种类型的错误，以及它如何重试将数据发送到目标平台。
title: 使用Destination SDK构建的流目标的速率限制和重试策略
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 使用Destination SDK构建的流目标的速率限制和重试策略

合作伙伴构建的目标可能会返回各种错误，并且具有不同的速率限制策略。 本页介绍Experience Platform如何处理流目标返回的各种类型的错误。

使用Destination SDK配置目标时，您可以在两种聚合类型之间进行选择 — [最大努力聚合](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation)和[可配置的聚合](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)。 根据您选择的聚合类型，请参阅下面的Experience Platform如何处理错误和速率限制。

## 最大努力聚合 {#best-effort-aggregation}

Experience Platform重试返回以下HTTP响应代码的调用： **403、408、409、429、500、502、503、504**。 按以下时间间隔执行两次重试：

* 首次重试尝试： 15秒后
* 第二次重试尝试： 30秒后

Experience Platform会&#x200B;*不*&#x200B;重试返回其他HTTP响应代码的调用，如400（错误请求）。 如果两次重试后调用仍然失败，Experience Platform将停止激活，并且不会重新尝试。

您可以通过联系客户支持来请求针对特定数据流的不同重试策略。

## 可配置的聚合 {#configurable-aggregation}

对于使用可配置聚合设置的目标平台，Experience Platform会区分平台返回的错误类型：

* Experience Platform重试将数据发送到您的平台的错误：
   * HTTP响应代码420和429
   * HTTP响应代码大于500
* Experience Platform *未*&#x200B;重试将数据发送到平台的错误：平台返回的所有其他数据

### 已描述重试方法 {#retry-approach}

下面介绍了用于可配置聚合的Experience Platform方法。 此示例假定Experience Platform向目标平台发送数据，如果每分钟接收的请求超过5万，则该平台开始返回429错误代码：

* 第1分钟：Experience Platform使用要发送到目标平台的用户档案汇总40,000批次数据。 Experience Platform发出40,000个HTTP请求并全部成功。
* 第2分钟：Experience Platform汇总70,000批次的用户档案以发送到目标平台。 Experience Platform发出70,000个HTTP请求，成功50,000个。 其他20k从您的端点收到速率限制错误，将在30分钟后重新尝试。
* 第3分钟：Experience Platform使用要发送到目标平台的用户档案汇总30,000批次数据。 Experience Platform发出30,000个HTTP请求并全部成功。
* ...
* ...
* 第32分钟：Experience Platform重新尝试发送在第2分钟失败的20,000批次。 所有调用均成功。

## 后续步骤 {#next-steps}

您现在知道Experience Platform如何处理来自目标平台的错误和速率限制，具体取决于您在配置流目标时选择的聚合策略。 接下来，您可以查看以下文档：

* [测试目标配置](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [提交在Destination SDK中创作的目标以供审查](../guides/submit-destination.md)
