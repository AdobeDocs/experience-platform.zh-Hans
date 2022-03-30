---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；字段组；字段组；
solution: Experience Platform
title: 在UI中创建和编辑架构字段组
description: 了解如何在Experience Platform用户界面中创建和编辑架构字段组。
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 在UI中创建和编辑架构字段组

在体验数据模型(XDM)中，架构字段组是可重用的组件，用于定义一个或多个字段以实施某些功能，例如个人详细信息、酒店首选项或地址。 字段组将作为实现兼容类的架构的一部分包含在内。

字段组根据字段组表示的数据（记录或时间序列）的行为，定义与哪些类兼容。 这意味着并非所有字段组都可用于所有类。

Adobe Experience Platform提供了许多涵盖各种营销用例的标准字段组。 但是，您也可以创建和编辑自己的自定义字段组，以定义与XDM架构中的业务相关的其他概念。 本指南概述了如何在Platform UI中为贵组织创建、编辑和管理自定义字段组。

## 先决条件

本指南需要对XDM系统有一定的了解。 请参阅 [XDM概述](../../home.md) 介绍XDM在Experience Platform生态系统中的作用，以及 [架构组合基础知识](../../schema/composition.md) 以了解字段组对XDM模式的贡献情况。

虽然本指南不是必需的，但建议您也要遵循 [在UI中合成架构](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 创建新字段组 {#create}

要创建新字段组，您必须先选择要将字段组添加到的架构。 您可以选择 [创建新模式](./schemas.md#create) 或 [选择要编辑的现有架构](./schemas.md#edit).

在中打开架构后， [!DNL Schema Editor]，选择 **[!UICONTROL 添加]** 旁边 [!UICONTROL 字段组] 区域。

![](../../images/ui/resources/field-groups/add-field-group.png)

此时会出现一个对话框，其中显示了贵组织的现有字段组列表。 在对话框顶部附近，选择 **[!UICONTROL 创建新字段组]**. 在此，您可以提供 **[!UICONTROL 显示名称]** 和 **[!UICONTROL 描述]** 字段组。 完成后，选择 **[!UICONTROL 添加字段组]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

的 [!DNL Schema Editor] 重新显示，新字段组列在左边栏中。 由于这是一个全新的字段组，因此它当前不向架构提供任何字段，因此画布保持不变。 您现在可以开始 [向字段组添加字段](#add-fields).

## 编辑现有字段组 {#edit}

>[!NOTE]
>
>只能完全编辑和自定义由您的组织定义的自定义字段组。 对于由Adobe定义的核心字段组，在单个架构的上下文中只能编辑其字段的显示名称。 请参阅 [编辑架构字段的显示名称](./schemas.md#display-names) 以了解详细信息。
>
>在用于数据摄取的架构中保存和使用自定义字段组后，以后只能对字段组进行附加更改。 请参阅 [模式演化规则](../../schema/composition.md#evolution) 以了解更多信息。

要编辑现有字段组，必须首先打开一个架构，该架构在 [!DNL Schema Editor]. 您可以 [选择要编辑的现有架构](./schemas.md#edit)，或者您可以 [创建新模式](./schemas.md#create) 并添加相关字段组。

在编辑器中打开架构后，您可以启动 [向字段组添加字段](#add-fields).

## 向字段组添加字段 {#add-fields}

向 [!DNL Schema Editor]，首先在左边栏中选择字段组的名称，然后选择 **加号(+)** 图标。

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL 新建字段]** 将显示在画布中，并且右边栏会更新以显示用于配置字段属性的控件。 请参阅 [在UI中定义字段](../fields/overview.md#define) 有关如何配置字段并将其添加到字段组的具体步骤。

继续向字段组添加所需数量的字段。 完成后，选择 **[!UICONTROL 保存]** 保存架构和字段组。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果同一字段组已在其他架构中使用，则新添加的字段将自动显示在这些架构中。

## 后续步骤

本指南介绍了如何使用平台UI创建和编辑字段组。 有关 [!UICONTROL 模式] 工作区，请参阅 [[!UICONTROL 模式] 工作区概述](../overview.md).

了解如何使用 [!DNL Schema Registry] API，请参阅 [字段组终结点指南](../../api/field-groups.md).
