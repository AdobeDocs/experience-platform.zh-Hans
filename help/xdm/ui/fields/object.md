---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；对象；字段；
solution: Experience Platform
title: 在UI中定义对象字段
description: 了解如何在Experience Platform用户界面中定义对象类型字段。
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在UI中定义对象字段

Adobe Experience Platform允许您完全自定义自定义体验数据模型(XDM)类、架构字段组和数据类型的结构。 为了在自定义XDM资源中组织和嵌套相关字段，您可以定义可包含其他子字段的对象类型字段。

When [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，使用 **[!UICONTROL 类型]** 下拉列表，选择“[!UICONTROL 对象]”。

![](../../images/ui/fields/special/object.png)

选择 **[!UICONTROL 应用]** 将对象添加到架构。 画布将更新，以显示新字段 [!UICONTROL 对象] 应用的数据类型，包括用于编辑子字段并将其添加到对象的控件。

![](../../images/ui/fields/special/object-applied.png)

要添加子字段，请选择 **加号(+)** 图标。 对象下方会显示一个新字段，其中包含用于在右边栏中配置子字段的控件。

![](../../images/ui/fields/special/object-add-field.png)

配置并选择子字段后 **[!UICONTROL 应用]**，则可以继续使用同一进程向对象添加字段。 您还可以添加子字段本身是对象，从而允许您按需要的深度嵌套字段。

构建完对象后，您可能会发现希望在不同的类和字段组中重复使用其结构。 在这种情况下，您可以选择将对象转换为数据类型。 请参阅 [将对象转换为数据类型](../resources/data-types.md#convert) （在数据类型UI指南中）以了解更多信息。

## 后续步骤

本指南介绍了如何在UI中定义对象字段。 请参阅 [在UI中定义字段](./overview.md#special) 了解如何在 [!DNL Schema Editor].
