---
title: 委托描述符ID
description: 了解Reactor API中的委派描述符ID，以及它们如何将资源与扩展相关联。
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委托描述符ID

使用Adobe Experience Platform中的标记时，您可以在网站上部署的所有功能都由扩展提供。 每个扩展提供的功能由扩展开发人员定义。 部署扩展时，它将与其各种功能捆绑在一起，其形式为 [扩展包](../endpoints/extension-packages.md). 开发人员添加到扩展包的功能被视为该包的“代理”。

扩展包中的每个委托都有一个唯一的委托描述符ID。 特定资源的委托描述符ID可告知系统它是什么类型的资源以及它属于哪个扩展包。

## 语法

委托描述符ID由三个用双冒号字符(`::`)，分别表示扩展包名称、委托类型和委托名称。 这些字符串的构成方式可供用户读取，并在摄取扩展包时由系统自动生成和分配。

例如，如果扩展包名为 `example-package` 具有名为的操作 `custom-code`，则该操作将具有以下委托描述符ID： `example-package::actions::custom-code`.

## 在适用的资源上使用委托描述符ID

在定义API中的规则组件（事件、条件和操作）和数据元素时，务必要了解委托描述符ID。 以下各节概述了这些ID如何对每个资源发挥作用。

### 规则组件

A [规则组件](../endpoints/rule-components.md) 必须与属于扩展包的事件、条件或操作关联。 这表示规则组件的“类型”，因为它与整体规则（事件、条件或操作）的逻辑相关。 因此，在创建规则组件时，必须提供委托描述符ID以指示应与规则组件关联的事件、条件或操作。

例如，要创建基于 `click` 扩展包中的事件 `example-package`，规则组件将使用以下内容 `delegate_descriptor_id` 值： `example-package::events::click`.

请参阅以下部分： [创建规则组件](../endpoints/rule-components.md#create) 了解更多信息。

### 数据元素

A [数据元素](../endpoints/data-elements.md) 首次创建扩展包时必须与扩展包关联，因为每个扩展包都为其委托数据元素定义了兼容类型及其预期行为。

例如，要创建使用 `cookie` 扩展包定义的类型 `example-package`，数据元素将使用以下内容 `delegate_descriptor_id` 值： `example-package::dataElements::cookie`.

请参阅以下部分： [创建数据元素](../endpoints/data-elements.md#create) 了解更多信息。

### 扩展

An [扩展](../endpoints/extensions.md) 首次创建扩展包时会自动与扩展包关联，并在扩展的 `relationships` 对象。 如果您的扩展需要自定义设置，则它还需要委派描述符ID。

>[!NOTE]
>
>不需要自定义设置的扩展不需要委托描述符ID。

例如，将委托描述符ID添加到属于扩展包的扩展 `example-package`，扩展将使用以下内容 `delegate_descriptor_id` 值： `example-package::extensionConfiguration::config`.

请参阅指南，网址为 [创建扩展](../endpoints/extensions.md#create) 了解更多信息。
