---
solution: Experience Platform
title: Edge Network与中心比较
description: 了解可在Adobe Experience Platform上使用的各种处理路径。
source-git-commit: 08a63fb854fe1c2aa83e7a7f74df4c02580e4d4c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---


# Edge Network与中心比较

Adobe Experience Platform是市场上功能最强大、最灵活、最开放的系统，用于构建和管理可改善客户体验的完整解决方案。 您可以使用Experience Platform来集中和标准化来自任何系统的客户数据和内容，并应用数据科学和机器学习来显着改进丰富个性化体验的设计和交付。 因此，Platform提供了多种方法来处理您的数据，让您可以以最好的方式评估您的数据。

## 服务器类型

在Platform上，可通过两种不同的路径处理数据：用于批处理工作流和流式工作流的Adobe Experience Platform中心以及用于实时体验的Edge Network。

### Adobe Experience Platform中心

中心是一个位于中心位置的主要数据中心，包含已在Adobe Experience Platform中收集的所有历史数据和丰富的配置文件上下文。 这样，您就可以向下游服务发送和接收更可靠且更完整的数据。 因此，中心应用于数据的&#x200B;**完整性**&#x200B;更重要的场合。

中心上的可用服务包括：

- 批次分段
- 流式客户细分
- 轮廓
- 目标
- 身份标识图
- 数据Distiller — 查询服务
- Source连接器

### Experience Platform Edge Network

Edge Network是一台物理位置更靠近不同地理位置的服务器。 这些数据中心会处理通过SDK扩展和Edge Network API收集的所有数据。 Edge Network上存在的唯一数据是受众成员资格、配置文件身份和个性化所需的属性。

由于Edge Network距离最终用户更近，因此可让您更快地向客户发送和接收数据。 此外，您可以使用Edge Network处理事件转发请求和标签管理请求。 但是，Edge Network仅处理&#x200B;**行为**&#x200B;数据。 因此，应在数据的&#x200B;**速度**&#x200B;更重要的情况下使用Edge Network。

Edge Network上的可用服务包括：

- 边缘分段
- Edge配置文件
- Edge目标
- 数据收集
- SDK扩展

## 位置

以下部分列出了中心和Edge Network的位置。

![列出了中心服务器和Edge Network服务器的不同位置的关系图。](./images/servers/platform-server-locations.png)

**中心**

- VA7 （美国弗吉尼亚州）
- NLD2（荷兰）
- AUS5 （澳大利亚）
- CAN2 （加拿大）
- GBR9 （英国）
- IND1 （印度）

**Edge Network**

- OR2 （美国俄勒冈州）
- VA6 （美国弗吉尼亚州）
- IRL1（爱尔兰）
- IND1 （印度）
- SGP3 （新加坡）
- AUS3 （澳大利亚）
- JPN3（日本）

有关可用服务器位置的更多详细信息可在[多云概述](./multi-cloud.md#available-cloud-regions)中找到。

## 后续步骤

阅读本概述后，您现在了解了在Adobe Experience Platform中心处理数据与Adobe Experience Platform Edge Network处理数据的区别。

## 附录

以下部分列出了有关在Adobe Experience Platform上处理数据的补充信息。

### 常见问题解答

以下部分列出了有关Hub和Edge Network的常见问题解答：

#### 哪些方案最适用于网络中心？

中心最适合数据的&#x200B;**完整性**&#x200B;更重要的情况。 例如，假设您要创建一个营销活动，以定位已放弃购物车的所有客户。 在该用例中，您可以使用批量分段，创建与放弃的购物车用户匹配的受众，并将其导出到批量目标。

#### 哪些方案最适合Edge Network？

Edge Network最适合数据的&#x200B;**速度**&#x200B;更重要的情况。 例如，假设您需要创建一个有限的闪购，以定位在购物车中浏览您的网站并出售产品的客户。 在该用例中，您可以使用边缘分段，让您立即定位并向用户发送个性化通知，其中用户购物车中带有“闪购”产品。

#### 哪些数据从中心传输到Edge Network？

只有在Edge上提供实时体验所需的数据才会从Hub加载到Edge Network。 此数据会自动从中心发送到Edge Network，以使其最终保持一致，并且最多只能保留14天。 但是，这并&#x200B;**不**&#x200B;意味着数据与Hub中的数据保持完全同步。 因此，中心服务器和Edge Network之间的可用数据可能存在差异。
