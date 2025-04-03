---
keywords: Experience Platform；主页；热门主题；分段；区段匹配；区段匹配
solution: Experience Platform
title: 区段匹配常见问题解答
description: 区段匹配是Adobe Experience Platform中的区段共享服务，它允许两个或更多Experience Platform用户以安全、受管理和隐私友好的方式交换区段数据。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Segment Match]常见问题解答

本指南提供有关Adobe Experience Platform区段匹配的常见隐私和法律问题解答。

## 在估计重叠期间共享哪些数据，以及Adobe如何确保安全地获取这些指标？

![overlap-report.png](./images/overlap-report.png)

没有在沙盒之间移动客户或区段数据以获取这些重叠估计量度。 任何给定沙盒中客户选择的预哈希适用的身份将添加到概率数据结构中，其中ID本身以哈希格式表示。

这是一个单向过程，这意味着原始的预哈希标识符不会公开，并且无法进行反向工程。

这些数据结构具有独特的特性，即使对信息进行严格压缩或散列处理，工程技术也可以在其之间执行并集和交集操作。 这些操作允许[!DNL Segment Match]从两个不同的沙盒中获取由ID组成的两个数据结构的估计交集，而无需比较实际值。 由于[!DNL Segment Match]仅使用数据结构，因此ID永远不会离开各自组织的配置文件存储来进行估计。 这使Adobe能够满足客户的隐私和安全要求，同时提供高度准确的估计工具来指导数据协作协议。

## 指定哪些身份接收共享区段ID的流程是什么？

[!DNL Segment Match]为客户提供了一个选项，用于配置要在服务中使用的命名空间。 如果客户决定将馈送发布到合作伙伴沙盒，则此选择将应用于上一个问题中描述的估计过程和数据传输过程。

在两个不同组织的加密身份之间的数据传输过程在中性计算环境中执行。 数据传输作业由Adobe拥有，参与伙伴关系的组织无权访问此环境，也无法访问任何可能是数据传输作业结果的日志。

只有区段成员资格会摄取到接收者组织的重叠配置文件片段中，并且不会从发件人组织向接收者组织传输其他身份。 数据传输作业不会读取纯文本的个人身份信息(PII)，因为[!DNL Segment Match]仅允许当数据为PII时在SHA256加密的命名空间（电子邮件/电话）上发生重叠。 结果永远不会存储在计算环境中。
