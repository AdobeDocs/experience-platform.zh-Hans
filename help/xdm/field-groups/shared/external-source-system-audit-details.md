---
title: 外部源系统审计详细信息
description: 了解外部Source系统审核详细信息体验数据模型(XDM)字段组。
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# [!UICONTROL 外部Source系统审核详细信息] 字段组

[!UICONTROL 外部Source系统审核详细信息] 是一个标准的体验数据模型(XDM)字段组，该字段组通过引用其属性并添加上下文元数据来扩展核心“外部Source系统审核属性”数据类型。 这样可以进行详细的审核跟踪，并灵活地集成来自外部源的数据。

![外部Source系统审核详细信息字段组的架构图。](../../images/field-groups/shared/external-source-system-audit-details.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL 外部Source系统审核详细信息] | `external-source-system-audit-details` | [[!UICONTROL 外部Source系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | “[!UICONTROL 外部Source系统审核详细信息]”字段组通过引用其属性并添加上下文元数据来扩展核心“外部Source系统审核属性”数据类型。 这有助于对外部源进行详细的审核跟踪和灵活的数据集成，从而适应配置文件摄取的异步性质。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [完整模式](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)