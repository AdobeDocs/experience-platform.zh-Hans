---
keywords: Experience Platform；主页；热门主题；管理标签；标记；
title: 管理标记概述
description: 本文档提供了有关Adobe Experience Platform中管理标记的信息
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# 标记概述

标记是Adobe Experience Platform的一项功能，它允许管理员管理元数据分类，以便对业务对象进行分类，从而更轻松地进行发现和分类。 标记是元数据，可以将其视为可附加到区段、数据集、历程或其他对象的关键字，以便搜索以查找该对象和相关对象。 标记分为两种类型：已分类和未分类。

为了提供更多上下文并定义标记的用途，类别会将标记组织为有用的集。 管理员可定义哪些分类标记可供用户添加到对象。 也可以在应用标记的工作流中串联创建不包含类别的新标记。 这些标记将显示在标记库存的未分类部分中。 无论是由谁创建标记，管理员和用户都可以应用标记。 为对象分配、搜索或筛选时，所有类型的标记都可供选择。

## 标记术语

标记涉及以下组件：

| 术语 | 定义 |
| --- | --- |
| 已存档 | 标记的状态，可保持当前与对象的关联，但限制将标记应用于其他对象。  存档的标记在标记选取器中处于隐藏状态。 |
| 对象 | 可以应用标记的Experience Cloud项目。  示例：区段、历程、数据集。 |
| 标记 | 标记是元数据，可以将其视为可附加到区段、数据集、历程或其他对象的关键字，以便能够搜索以查找该对象和相关对象。 |
| 标记类别 | 标记类别将标记分组为有意义的集，以提供更好的上下文或描述标记的用途。  管理员可管理类别中的标记类别和标记。 |
| 未分类的标记 | 在行内创建并应用标记的新标记。 这些标记可由任何用户创建和应用，但不会绑定到类别。  管理员可以将这些标记移动到类别中，以便与其他类似的标记保持一致。 |

## 标记库存

在Experience Platform和Journey Optimizer导航中，可以使用标记库存的标记类别和标记管理。 库存中标记的更改将反映在支持标记的所有对象中。 所有用户都可以访问和浏览标记库存，但标记管理仅限系统和产品管理员。

标记库存具有三层层次结构，允许用户管理标记类别、类别中的标记和单个标记。 在管理单个标记时，用户可以查看并导航到当前应用该标记的任何对象。

### 标记类别

将标记分组为有意义的集，以提供更好的上下文或描述标记的用途。 在任何具有类别的标记上，类别名称后跟冒号后面的标记名称前面。

使用标记类别时，可以执行以下操作：

* [创建标记类别](./ui/tags-categories.md#create-tag-category)
* [编辑标记类别](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [删除标记类别](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理类别中的标记

>[!NOTE]
>
>要管理Experience Cloud的标记，您必须是贵组织的Adobe Experience Platform系统管理员或产品管理员，该组织已订阅Experience Cloud。

在类别（或默认的“未分类”群组）中，您可以创建和管理标记。 在管理标记时，可以执行以下操作：

* [创建标记](./ui/managing-tags.md#create-a-tag-create-tag)
* [编辑标记](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在类别之间移动标记](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [存档标记](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [恢复已存档的标记](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [删除标记](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [查看标记对象](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
