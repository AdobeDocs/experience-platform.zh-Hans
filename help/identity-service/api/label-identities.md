---
keywords: Experience Platform；主页；热门主题；标签标识
solution: Experience Platform
title: 将字段标记为标识
topic-legacy: api guide
description: 包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值由标识服务解释为标识。 标识的命名空间指定为标记字段的一部分。
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 将字段标记为标识

包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值由[!DNL Identity Service]解释为标识。 标识的命名空间指定为标记字段的一部分。

要标记为标识的字段必须满足以下条件：

- 只有字符串类型字段可用于标识
- 身份仅在记录和时间序列数据中识别
- 应仅将PII字段标记为标识。 选择表示更通用数据的字段会导致关系不那么精确，并可能导致从身份图访问相关身份时出错

有关如何使用模式注册表API将字段标记为标识的说明，请访问[描述符终结点指南](../../xdm/api/descriptors.md#create)。

## 后续步骤

转到下一个教程[列表群集标识](./list-cluster-identites.md)
