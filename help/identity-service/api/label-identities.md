---
keywords: Experience Platform；主页；热门主题；标签标识
solution: Experience Platform
title: 将字段标记为标识
description: 包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值由Identity Service解释为标识。 标识的命名空间将作为标记字段的一部分进行指定。
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 为字段设置标签以作为标识

包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值被解释为标识 [!DNL Identity Service]. 标识的命名空间将作为标记字段的一部分进行指定。

要将字段标记为标识，必须满足以下条件：

- 只能将字符串类型字段用于标识
- 身份仅在记录数据和时间序列数据中识别
- 只应将PII字段标记为标识。 选择表示更通用数据的字段会导致关系不太精确，并可能导致从身份图访问相关身份时出现错误

有关如何使用架构注册表API将字段标记为身份的说明，请访问 [描述符终结点指南](../../xdm/api/descriptors.md#create).

## 后续步骤

继续下一个教程以 [列表聚类标识](./list-cluster-identites.md)
