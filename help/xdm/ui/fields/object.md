---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；对象；字段；
solution: Experience Platform
title: 在UI中定义对象字段
description: 了解如何在Experience Platform用户界面中定义对象类型字段。
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 在UI中定义对象字段

Adobe Experience Platform允许您完全自定义自定义Experience Data Model (XDM)类、架构字段组和数据类型的结构。 为了在自定义XDM资源中组织和嵌套相关字段，可以定义可包含其他子字段的对象类型字段。

时间 [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，使用 **[!UICONTROL 类型]** 下拉并选择&quot;[!UICONTROL 对象]”从列表中删除。

![](../../images/ui/fields/special/object.png)

选择 **[!UICONTROL 应用]** 将对象添加到模式。 画布将更新以显示包含的新字段 [!UICONTROL 对象] 应用的数据类型，包括用于编辑子字段并将其添加到对象的控件。

![](../../images/ui/fields/special/object-applied.png)

要添加子字段，请选择 **加(+)** 图标（位于画布中的对象字段旁边）。 对象下方将显示一个新字段，其中包含用于在右边栏中配置子字段的控件。

![](../../images/ui/fields/special/object-add-field.png)

配置子字段并选择后 **[!UICONTROL 应用]**，则可以使用相同的过程继续将字段添加到对象。 您还可以添加作为对象本身的子字段，从而允许嵌套任意深度的字段。

完成对象的构建后，您可能会发现希望在不同类和字段组中重用其结构。 在这种情况下，您可以选择将对象转换为数据类型。 请参阅以下部分 [将对象转换为数据类型](../resources/data-types.md#convert) 有关更多信息，请参阅数据类型UI指南。

## 后续步骤

本指南介绍了如何在UI中定义对象字段。 有关更多详细信息，请参阅 [在UI中定义字段](./overview.md#special) 了解如何在中定义其他XDM字段类型 [!DNL Schema Editor].
