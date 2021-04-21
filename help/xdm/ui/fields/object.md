---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；对象；字段；
solution: Experience Platform
title: 在UI中定义对象字段
description: 了解如何在Experience Platform用户界面中定义对象类型字段。
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 在UI中定义对象字段

Adobe Experience Platform允许您完全自定义自定义体验数据模型(XDM)类、混合和数据类型的结构。 为了在自定义XDM资源中组织和嵌套相关字段，您可以定义可包含其他子字段的对象类型字段。

当[在Adobe Experience Platform用户界面中定义新字段](./overview.md#define)时，请使用&#x200B;**[!UICONTROL Type]**&#x200B;下拉列表并从列表中选择“[!UICONTROL Object]”。

![](../../images/ui/fields/special/object.png)

选择&#x200B;**[!UICONTROL Apply]**&#x200B;将对象添加到模式。 画布会更新以显示应用了[!UICONTROL Object]数据类型的新字段，包括用于编辑子字段和向对象添加子字段的控件。

![](../../images/ui/fields/special/object-applied.png)

要添加子字段，请选择画布中对象字段旁边的加号(+)**图标。**&#x200B;对象下方将显示一个新字段，右侧边栏中包含用于配置子字段的控件。

![](../../images/ui/fields/special/object-add-field.png)

配置子字段并选择&#x200B;**[!UICONTROL Apply]**&#x200B;后，可以继续使用同一进程向对象添加字段。 您还可以添加子字段，这些子字段本身是对象，这样您就可以随意嵌套字段。

![](../../images/ui/fields/special/object-nested.png)

构建完对象后，您可能会发现希望在不同的类和混合中重复使用其结构。 在这种情况下，您可以选择将对象转换为数据类型。 有关详细信息，请参阅数据类型UI指南中有关将对象转换为数据类型](../resources/data-types.md#convert)的部分。[

## 后续步骤

本指南介绍如何在用户界面中定义对象字段。 有关在UI](./overview.md#special)中定义字段的概述，请参阅[，以了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
