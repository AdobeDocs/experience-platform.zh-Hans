---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 将字段标记为标识
topic: api guide
translation-type: tm+mt
source-git-commit: 40ce232e39f62f1ee478ef05229dd2fc125ee4c0

---


# 将字段标记为标识

包含个人身份信息(PII)的字段可标记为身份字段。 标识字段中提供的值由标识服务解释为标识。 标识的命名空间指定为标记字段的一部分。

要将字段标记为标识，必须满足以下条件：

- 只有字符串类型字段可用于标识
- 身份仅在记录和时间序列数据中识别
- 只有PII字段应标记为标识。 选择表示更通用数据的字段将导致更不精确的关系和访问标识图中的相关标识的潜在错误

有关如何使用模式注册表API将字段标记为标识的说明，请访 [问创建描述符](../../xdm/api/descriptors.md)。

## 后续步骤

继续执行下一个教程以 [列表群集标识](./list-cluster-identites.md)