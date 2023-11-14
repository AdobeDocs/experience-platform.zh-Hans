---
keywords: Experience Platform；首页；热门话题；统一标记；标记；
title: 统一标记概述
description: 本文档提供有关 Adobe Experience Platform 中的统一标记的信息
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 6977438d57dc8e1390812e58bf039ebc60cb830d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 100%

---

# 统一标记概述

标记是 Adobe Experience Platform 提供的一项功能，该功能使管理员能够管理元数据分类法，以便对业务对象进行分类，从而更轻松地对其进行查找和分类。标记是可以被视为关键字的元数据，它们可以附加到区段、数据集、历程或其他对象上，以便在搜索时能够找到该对象和相关对象。标记分为两种类型：已分类标记和未分类标记。

为了提供更多上下文信息并定义标记的用途，通过分类可将标记组织成有用的集合。管理员定义哪些分类标记可供用户添加到对象。也可以在应用标记的工作流程中以内联的方式创建不包含类别的新标记。这些标记将会显示在标记清单的未分类部分。管理员和用户都可以应用标记，无论创建者是谁。在分配给对象、搜索或过滤时，所有类型的标记都可供选择。

## 标记术语

标记涉及以下组成部分：

| 术语 | 定义 |
| --- | --- |
| 已存档 | 标记的一种状态，该状态保持与对象当前的联系，但限制标记应用于其他对象。存档的标记对标记选择器隐藏。 |
| 对象 | 可以应用标记的 Experience Cloud 项目。示例：区段、历程、数据集。 |
| 标记 | 标记是可以被视为关键字的元数据，它们可以附加到区段、数据集、历程或其他对象上，以便在搜索时能够找到该对象和相关对象。 |
| 标记类别 | 标记类别将标记分组为有意义的集合，以提供更多上下文信息或描述标记的用途。管理员管理标记类别和类别内的标记。 |
| 未分类标记 | 在应用标记的位置以内联的方式创建的新标记。这些标记可以由任何用户创建和应用，但它们没有绑定到某个类别。管理员可以将这些标记移至某个类别，以与其他类似标记保持一致。 |

## 标记库存

Experience Platform 和 Journey Optimizer 导航中提供使用标记库存的标记分类和标记管理功能。对库存中标记的更改会反映在支持标记的所有对象中。所有用户都可以访问和浏览标记库存，但仅有系统和产品管理员才能管理标记。

标记库存具有三个层次结构，允许用户管理标记类别、类别内的标记以及单个标记。管理单个标记时，用户可以查看并导航到当前应用该标记的任何对象。

### 标记类别

分类功能会将标记分组为有意义的集合，以提供更多上下文信息或描述标记的用途。在任何带有类别的标记上，类别名称后面跟有冒号，位于标记名称之前。

使用标记类别时可以执行以下操作：

* [创建标记类别](./ui/tags-categories.md#create-tag-category)
* [编辑标记类别](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [删除标记类别](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理某个类别内的标记

>[!NOTE]
>
>若要管理 Experience Cloud 的标记，您必须是已订阅 Experience Cloud 的组织的 Adobe Experience Platform 的系统管理员或产品管理员 。

在类别（或默认的“未分类”组）中，您可以创建和管理标记。管理标记时可以执行以下操作：

* [创建标记](./ui/managing-tags.md#create-a-tag-create-tag)
* [编辑标记](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在类别之间移动标记](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [存档标记](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [恢复已存档的标记](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [删除标记](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [查看标记的对象](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
