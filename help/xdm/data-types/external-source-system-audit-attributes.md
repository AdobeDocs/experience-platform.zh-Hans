---
title: 外部Source系统审计属性数据类型
description: 了解外部Source系统审核属性Experience Data Model (XDM)数据类型。
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 18%

---

# [!UICONTROL 外部Source系统审核属性]数据类型

[!UICONTROL 外部来源系统审计属性]是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

![](../images/data-types/external-source-system-audit-attributes.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B Source]](./b2b-source.md) | 用于审核的源的复合标识符。 |
| `createdBy` | 字符串 | 创建此记录的用户的名称。 |
| `createdDate` | 日期时间 | 创建此记录的日期。 |
| `externalID` | 字符串 | 源的外部唯一标识符。 如果需要，此值用于帮助识别和删除重复数据。 |
| `lastActivityDate` | 日期时间 | 源系统的上次活动日期。 |
| `lastReferencedDate` | 日期时间 | 源系统的最后引用日期。 |
| `lastUpdatedBy` | 字符串 | 上次更新此记录的人员的姓名。 |
| `lastUpdatedDate` | 日期时间 | 源系统的上次更新日期。 [属性合并策略](../../profile/api/merge-policies.md#attribute-merge)使用此值来确定发生合并冲突时的优先级。 |
| `lastViewedDate` | 日期时间 | 源系统的上次查看日期。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
