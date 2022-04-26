---
description: 了解Experience Platform如何处理由流目标返回的不同类型错误，以及如何重试将数据发送到目标平台。
title: 针对通过Destination SDK构建的流目标的速率限制和重试策略
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 针对通过Destination SDK构建的流目标的速率限制和重试策略

## 概述 {#overview}

合作伙伴构建的目标可能会返回各种错误，并具有不同的限速策略。 本页介绍Experience Platform如何处理由流目标返回的不同类型的错误。

使用Destination SDK配置目标时，您可以选择两种聚合类型 —  [最佳工作聚合](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) 和 [可配置聚合](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). 根据您选择的聚合类型，阅读下面Experience Platform如何处理错误和速率限制的内容。

## 尽力汇总 {#best-effort-aggregation}

对于对目标进行的任何HTTP调用失败，Experience Platform会尝试在首次调用后立即再次进行调用。 如果第二次尝试时调用仍然失败，则Experience Platform将放弃调用，并且不会第三次重新尝试它。

## 可配置聚合 {#configurable-aggregation}

对于通过可配置聚合设置的目标平台，Experience Platform会区分您的平台返回的错误类型：

* Experience Platform重试将数据发送到平台的错误：
   * HTTP响应代码420和429
   * 大于500的HTTP响应代码
* Experience Platform错误 *不* 重试将数据发送到您的平台：平台返回的所有其他内容

### 描述的重试方法 {#retry-approach}

下面介绍了可配置聚合的Experience Platform方法。 此示例假定Experience Platform每分钟收到超过5万个请求时，会将数据发送到开始返回429个错误代码的目标平台：

* 第1分钟：Experience Platform将40,000批与用户档案聚合，以发送到目标平台。 Experience Platform发出4万个HTTP请求，所有请求都成功。
* 第2分钟：Experience Platform将70,000批与用户档案聚合，以发送到目标平台。 Experience Platform发出70,000个HTTP请求，50,000个请求成功。 其他20k从您的端点收到速率限制错误，将在30分钟后重试。
* 第3分钟：Experience Platform将30,000批与用户档案聚合，以发送到目标平台。 Experience Platform发出3万个HTTP请求，所有请求都成功。
* ...
* ...
* 第32分钟：Experience Platform重新尝试发送在第2分钟失败的20,000批。 所有调用均成功。

## 后续步骤 {#next-steps}

现在，您可以了解Experience Platform如何处理来自目标平台的错误和速率限制，具体取决于您在配置流目标时选择的聚合策略。 接下来，您可以查看以下文档：

* [测试目标配置](/help/destinations/destination-sdk/test-destination.md)
* [提交以供审核在Destination SDK中创作的目标](/help/destinations/destination-sdk/submit-destination.md)
