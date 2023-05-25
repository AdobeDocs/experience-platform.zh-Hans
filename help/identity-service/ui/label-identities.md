---
keywords: Experience Platform；主页；热门主题；标签标识
title: 在UI中将字段标记为身份
description: 包含个人身份信息(PII)的字段可以标记为标识字段。 标识字段中提供的值由Identity服务解释为标识。 标识的命名空间在标记字段时指定。
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 在UI中将字段标记为身份

包含个人身份信息(PII)的字段可以标记为标识字段。 标识字段中提供的值由解释为标识 [!DNL Identity Service]. 标识的命名空间在标记字段时指定。

字段必须满足以下条件才能标记为标识：

* 只有字符串类型字段可用于标识
* 只能在记录和时间序列数据中识别身份
* 只有PII字段应标记为标识。 选择表示更通用数据的字段会导致关系更不精确，并可能导致从身份图访问相关身份时出现错误

有关如何在UI中标记身份字段的说明，请参阅以下指南： [在UI中定义身份字段](../../xdm/ui/fields/identity.md).

## 后续步骤

有关的详细信息 [!DNL Identity Service]，请参见 [[!DNL Identity Service] 概述](../home.md).
