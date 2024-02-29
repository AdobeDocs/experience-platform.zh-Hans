---
keywords: Experience Platform；主页；热门主题；标签标识
solution: Experience Platform
title: 将字段标记为标识
description: 包含个人身份信息(PII)的字段可以标记为标识字段。 标识字段中提供的值由Identity Service解释为标识。 标识的命名空间在为该字段设置标签时指定。
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 将字段标记为标识

包含个人身份信息(PII)的字段可以标记为标识字段。 标识字段中提供的值由解释为标识 [!DNL Identity Service]. 标识的命名空间在为该字段设置标签时指定。

字段必须满足以下条件才能标记为标识：

- 只有字符串类型字段可用于标识
- 仅在记录和时间序列数据中识别身份
- 只有PII字段应标记为标识。 选择表示更通用数据的字段将导致关系更不精确，并且可能会导致从身份图访问相关身份时出现错误

有关如何使用架构注册表API将字段标记为身份的说明，请访问 [描述符端点指南](../../xdm/api/descriptors.md#create).

## 后续步骤

继续下一教程以 [列出群集身份](./list-cluster-identites.md)
