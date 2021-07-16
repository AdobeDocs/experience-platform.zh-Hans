---
title: 委派描述符ID
description: 了解Reactor API中的委派描述符ID，以及它们如何将资源与扩展链接。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委托描述符ID

在Adobe Experience Platform中使用标记时，您可以在网站上部署的所有功能都由扩展提供。 每个扩展提供的功能由扩展开发人员定义。 部署扩展时，该扩展会与其各种功能捆绑在一起，形式为[扩展包](../endpoints/extension-packages.md)。 开发人员添加到扩展包的功能被视为该包的“代理”。

扩展包中的每个委托都将获得一个唯一的委托描述符ID。 特定资源的委托描述符ID可告知系统它是哪种资源以及它属于哪个扩展包。

## 语法

委托描述符ID由三个字符串组成，这些字符串由双冒号字符(`::`)联接，分别表示扩展包名称、委托类型和委托名称。 这些字符串由人类可读组成，在摄取扩展包时由系统自动生成并分配。

例如，如果名为`example-package`的扩展包具有名为`custom-code`的操作，则该操作将具有以下委托描述符ID:`example-package::actions::custom-code`。

## 在适用的资源上使用委派描述符ID

委派描述符ID对于在API中定义规则组件（事件、条件和操作）和数据元素时，要了解它们的含义，非常重要。 以下各节概述了这些ID如何在每个资源中发挥作用。

### 规则组件

[规则组件](../endpoints/rule-components.md)必须与属于扩展包的事件、条件或操作相关联。 这表示规则组件的“类型”，因为它与整个规则（事件、条件或操作）的逻辑相关。 因此，在创建规则组件时，必须提供委派描述符ID来指示规则组件应与哪个事件、条件或操作关联。

例如，要创建基于扩展包`example-package`中`click`事件的事件规则组件，规则组件将使用以下`delegate_descriptor_id`值：`example-package::events::click`。

有关更多信息，请参阅[创建规则组件](../endpoints/rule-components.md#create)中的部分。

### 数据元素

首次创建[数据元素](../endpoints/data-elements.md)时，必须将其与扩展包关联，因为每个扩展包都定义其委托数据元素的兼容类型及其预期行为。

例如，要创建使用扩展包`example-package`定义的`cookie`类型的数据元素，该数据元素将使用以下`delegate_descriptor_id`值：`example-package::dataElements::cookie`。

有关更多信息，请参阅[创建数据元素](../endpoints/data-elements.md#create)中的部分。

### 扩展

[扩展](../endpoints/extensions.md)在首次创建时自动与扩展包关联，并在扩展的`relationships`对象中表示。 如果您的扩展需要自定义设置，则它还需要委派描述符ID。

>[!NOTE]
>
>不需要自定义设置的扩展不需要委托描述符ID。

例如，要向属于扩展包`example-package`的扩展添加委派描述符ID，该扩展将使用以下`delegate_descriptor_id`值：`example-package::extensionConfiguration::config`。

有关更多信息，请参阅[创建扩展](../endpoints/extensions.md#create)的指南。