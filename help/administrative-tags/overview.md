---
keywords: Experience Platform；主页；热门主题；统一标签；标签；
title: （测试版）统一标记概述
description: 本文档提供了有关Adobe Experience Platform中统一标记的信息
source-git-commit: 6f9787909b8155d2bf032b4a42483f2cb4d44eb4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# （测试版）统一标记概述

>[!IMPORTANT]
>
>统一标记处于测试阶段。 如果您想提供反馈，请选择“标记管理”页面顶部的按钮。

标记是Adobe Experience Platform的一项功能，它使管理员能够管理元数据分类，以便对业务对象进行分类，从而更便于发现和分类。 标记是元数据，可以将其视为可附加到区段、数据集、历程或其他对象的关键字，以便搜索功能查找该对象和相关对象。 标记分为两种类型：已分类和未分类。

为了提供更多上下文并定义标记的目的，类别将标记组织成有用的集。 管理员定义哪些分类标记可供用户添加到对象中。 此外，还可以在应用标记的工作流中内联创建不包含类别的新标记。 这些标记将显示在标记清单的未分类部分中。 标记可以由管理员和用户应用，无论其创建者如何。 在指定给对象、搜索或筛选时，所有类型的标记都可供选择。

## 标记术语

标记涉及以下组件：

| 术语 | 定义 |
| --- | --- |
| 已存档 | 标记的状态，它保持当前与对象的关联，但限制标记无法应用于其他对象。  已存档的标记在标记选取器中处于隐藏状态。 |
| 对象 | 可应用标记的Experience Cloud项目。  示例：区段、历程、数据集。 |
| 标记 | 标记是元数据，可视为可附加到区段、数据集、历程或其他对象的关键字，以便搜索功能查找该对象和相关对象。 |
| 标记类别 | 标记类别可将标记分组为有意义的集，以提供更大的上下文或描述标记的目的。  管理员管理标记类别和类别中的标记。 |
| 未分类的标记 | 在已应用标记的内联中创建的新标记。 这些标记可由任何用户创建和应用，但它们未绑定到类别。  管理员可以将这些标记移动到某个类别，以便与其他类似标记保持一致。 |

## 标记库存

在Experience Platform和Journey Optimizer导航中，可以使用标记清单进行标记类别和标记管理。 对清单中的标记所做的更改会反映在支持标记的所有对象中。 所有用户都能够访问和浏览标记清单，但标记管理仅限于系统和产品管理员。

标记清单具有三个层级，允许用户管理标记类别、类别中的标记和单个标记。 管理单个标记时，用户可以查看和导航到当前应用该标记的任何对象。

### 标记类别

类别可将标记分组为有意义的集，以提供更大的上下文或描述标记的目的。 在包含类别的任何标记上，类别名称前跟一个冒号。

使用标记类别时，可以执行以下操作：

* [创建标记类别](./ui/tags-categories.md#create-tag-category)
* [编辑标记类别](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [删除标记类别](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理类别中的标记

>[!NOTE]
>
>要管理Experience Cloud的标记，您必须是贵组织的系统管理员或Adobe Experience Platform产品管理员，贵组织已订阅Experience Cloud。

在类别（或默认的“未分类”组）中，您可以创建和管理标记。 可在管理标记时执行以下操作：

* [创建标记](./ui/managing-tags.md#create-a-tag-create-tag)
* [编辑标记](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在类别之间移动标记](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [将标记存档](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [恢复已存档的标记](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [删除标记](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [查看标记的对象](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
