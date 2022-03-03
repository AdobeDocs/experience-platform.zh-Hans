---
title: 金融帐户数据类型
description: 本文档概述了金融帐户XDM数据类型。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 8%

---

# [!UICONTROL 财务帐户] 数据类型

[!UICONTROL 财务帐户] 是一种标准的XDM数据类型，用于描述财务帐户的详细信息，包括其类型、所有者和当前余额。

![](../images/data-types/financial-account.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 货币]](./currency.md) | 帐户的当前余额。 |
| `financialAccountId` | [!UICONTROL 字符串] | 帐户的唯一ID。 |
| `financialAccountName` | [!UICONTROL 字符串] | 分配给帐户的名称。 |
| `financialAccountType` | [!UICONTROL 字符串] | 财务帐户的类型，如支票、储蓄或退休。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
