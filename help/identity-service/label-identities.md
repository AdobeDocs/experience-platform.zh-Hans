---
keywords: Experience Platform；主页；热门主题；标签标识
title: 在UI中将字段标记为身份
description: 包含个人身份信息(PII)的字段可以标记为标识字段。 标识字段中提供的值由Identity Service解释为标识。 标识的命名空间在为该字段设置标签时指定。
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# 在UI中将字段标记为身份

包含个人身份信息(PII)的字段可以标记为标识字段。 [!DNL Identity Service]将标识字段中提供的值解释为标识。 标识的命名空间在为该字段设置标签时指定。

字段必须满足以下条件才能标记为标识：

* 只有字符串类型字段可用于标识
* 仅在记录和时间序列数据中识别身份
* 只有PII字段应标记为标识。 选择表示更通用数据的字段将导致关系更不精确，并且可能会导致从身份图访问相关身份时出现错误

有关如何在UI中标记身份字段的说明，请参阅[在UI中定义身份字段指南](../xdm/ui/fields/identity.md)。

## 后续步骤

有关 [!DNL Identity Service] 的详细信息，请参阅 [[!DNL Identity Service] 概述](./home.md)。
