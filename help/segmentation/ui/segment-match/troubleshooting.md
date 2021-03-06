---
keywords: Experience Platform；主页；热门主题；分段；区段匹配；区段匹配
solution: Experience Platform
title: 区段匹配常见问题解答
description: 区段匹配是Adobe Experience Platform中的一项区段共享服务，允许两个或更多Platform用户以安全、受管理和隐私友好的方式交换区段数据。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] 常见问题解答

本指南提供了有关Adobe Experience Platform区段匹配的隐私和法律问题的解答。

## 在估计重叠期间共享哪些数据，如何Adobe确保安全地获取这些量度？

![overlap-report.png](./images/overlap-report.png)

不会跨沙盒移动客户或区段数据以获取这些重叠的估计量度。 任何给定沙箱中由客户选择且经过预哈希处理的适用身份将添加到概率数据结构中，在该数据结构中，ID本身以哈希格式表示。

这是一个单向过程，这意味着原始经过预哈希处理的标识符不会公开，并且无法进行反向设计。

这些数据结构具有独特的属性，使工程人员能够在它们之间执行并集和交集操作，即使编码的信息被严重压缩或经过哈希处理。 这些操作允许 [!DNL Segment Match] 从两个不同的沙箱中获取由ID组成的两个数据结构的估计交集，而无需比较实际值。 自 [!DNL Segment Match] ID只使用数据结构，永远不会出于估算目的而离开其各自的IMS组织的配置文件存储。 这使Adobe能够满足客户的隐私和安全要求，同时提供用于指导数据协作协议的高度准确的评估工具。

## 指定哪些标识接收共享的区段ID是什么过程？

[!DNL Segment Match] 为客户提供了一个选项，用于配置要在服务中使用的命名空间。 如果客户决定将信息源发布到合作伙伴沙箱，则此选择将应用于上一个问题中描述的估算流程和数据传输流程。

在两个不同组织的加密身份之间的数据传输过程在中性计算环境中执行。 数据传输作业由Adobe拥有，并且参与合作伙伴关系的组织无权访问此环境，也无权访问任何可能是数据传输作业结果的日志。

只有区段成员资格会被摄取到接收者IMS组织重叠的配置文件片段中，并且不会从发送者IMS组织向接收者IMS组织转移任何其他身份。 数据传输作业不会读取纯文本个人身份信息(PII)，因为 [!DNL Segment Match] 仅当数据为PII时，才允许与SHA256加密的命名空间（电子邮件/电话）重叠。 结果从不存储在计算环境中。
