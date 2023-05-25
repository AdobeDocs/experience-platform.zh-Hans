---
title: 财务帐户数据类型
description: 本文档概述了财务帐户XDM数据类型。
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 5%

---

# [!UICONTROL 财务帐户] 数据类型

[!UICONTROL 财务帐户] 是一个标准XDM数据类型，描述财务帐户的详细信息，包括其类型、所有者和当前余额。

![](../images/data-types/financial-account.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 货币]](./currency.md) | 帐户的当前余额。 |
| `financialAccountId` | [!UICONTROL 字符串] | 帐户的唯一ID。 |
| `financialAccountName` | [!UICONTROL 字符串] | 分配给帐户的名称。 |
| `financialAccountType` | [!UICONTROL 字符串] | 财务帐户的类型，如支票、储蓄或退休。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
