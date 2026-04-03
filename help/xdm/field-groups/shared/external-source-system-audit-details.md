---
title: 外部Source系统审核详细信息
description: 了解外部Source系统审核详细信息体验数据模型(XDM)字段组。
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 4%

---

# [!UICONTROL External Source System Audit Details]字段组

[!UICONTROL External Source System Audit Details]是一个标准体验数据模型(XDM)字段组，可通过引用其属性并添加上下文元数据来扩展核心“外部Source系统审核属性”数据类型。 这样可以进行详细的审核跟踪，并灵活地集成来自外部源的数据。

![外部Source系统审核详细信息字段组的架构图。](../../images/field-groups/shared/external-source-system-audit-details.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | “[!UICONTROL External Source System Audit Details]”字段组通过引用其属性并添加上下文元数据来扩展核心“外部Source系统审核属性”数据类型。 这有助于对外部源进行详细的审核跟踪和灵活的数据集成，从而适应配置文件摄取的异步性质。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [完整架构](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)
