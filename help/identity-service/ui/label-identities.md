---
keywords: Experience Platform；主页；热门主题；标签标识
title: 在UI中将字段标记为标识
description: 包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值由Identity Service解释为标识。 标识的命名空间将作为标记字段的一部分进行指定。
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 在UI中将字段标记为标识

包含个人身份信息(PII)的字段可以标记为身份字段。 标识字段中提供的值被解释为标识 [!DNL Identity Service]. 标识的命名空间将作为标记字段的一部分进行指定。

要将字段标记为标识，必须满足以下条件：

* 只能将字符串类型字段用于标识
* 身份仅在记录数据和时间序列数据中识别
* 只应将PII字段标记为标识。 选择表示更通用数据的字段会导致关系不太精确，并可能导致从身份图访问相关身份时出现错误

有关如何在UI中标记身份字段的说明，请参阅 [在UI中定义标识字段](../../xdm/ui/fields/identity.md).

## 后续步骤

有关 [!DNL Identity Service]，请参阅 [[!DNL Identity Service] 概述](../home.md).
