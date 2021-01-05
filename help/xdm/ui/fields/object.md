---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;object;field;
solution: Experience Platform
title: 在UI中定义对象字段
description: 了解如何在Experience Platform用户界面中定义对象类型字段。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# 在UI中定义对象字段

Adobe Experience Platform允许您完全自定义自定义体验数据模型(XDM)类、混合和数据类型的结构。 为了在自定义XDM资源中组织和嵌套相关字段，您可以定义可包含其他子字段的对象类型字段。

当[在Adobe Experience Platform用户界面中定义新字段](./overview.md#define)时，请使用&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表，并从列表中选择“[!UICONTROL 对象]”。

![](../../images/ui/fields/special/object.png)

选择&#x200B;**[!UICONTROL 应用]**&#x200B;将对象添加到模式。 画布将更新以显示应用了[!UICONTROL Object]数据类型的新字段，包括用于编辑子字段并向对象添加子字段的控件。

![](../../images/ui/fields/special/object-applied.png)

要添加子字段，请选择画布中对象字段旁边的加号(+)**图标。**&#x200B;对象下方会显示一个新字段，右边栏中提供用于配置子字段的控件。

![](../../images/ui/fields/special/object-add-field.png)

配置子字段并选择&#x200B;**[!UICONTROL 应用]**&#x200B;后，您可以继续使用相同的进程向对象添加字段。 您还可以添加子字段，它们本身是对象，允许您随意嵌套字段。

![](../../images/ui/fields/special/object-nested.png)

构建完对象后，您可能会发现要在不同的类和混合中重复使用其结构。 在这种情况下，您可以选择将对象转换为数据类型。 有关详细信息，请参阅数据类型UI指南中的[将对象转换为数据类型](../resources/data-types.md#convert)一节。

## 后续步骤

本指南介绍如何在UI中定义对象字段。 请参见[定义UI](./overview.md#special)中的字段的概述，了解如何定义[!DNL Schema Editor]中的其他XDM字段类型。
