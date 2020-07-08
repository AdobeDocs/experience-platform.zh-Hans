---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用模式模式编辑器定义两个模式之间的关系
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# 使用模式编辑器定义两个模式之间的关系

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要组成部分。 在体验数据模型(XDM)模式结构中定义这些关系，使您能够获得对客户数据的复杂洞察。

本文档提供了一个教程，用于定义组织使用Experience Platform用户界面中的模式编辑器定义的两个模式之间的一对一关系。 有关使用API定义模式关系的步骤，请参阅使用 [模式注册表API定义关系的教程](relationship-api.md)。

## 入门指南

本教程需要对XDM系统和模式编辑器在Experience PlatformUI中有效的了解。 在开始本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md): XDM及其在Experience Platform中实现的概述。
* [模式合成基础](../schema/composition.md): 介绍XDM模式的构件。
* [使用模式编辑器创建模式](create-schema-ui.md): 一个教程，其中介绍使用模式编辑器的基础知识。

## 定义源和目标模式

您应已创建将在关系中定义的两个模式。 为了进行演示，本教程在组织的忠诚项目(在“忠诚会员”模式中定义)的成员与其喜爱的酒店(在“酒店”模式中定义)之间建立了关系。

模式关系由源 **模式表示** ，该源具有引用目标模式内的另 **一个字段**。 在接下来的步骤中，“忠诚会员”将是源模式，而“酒店”将充当目标模式。

为便于参考，以下各节将介绍在定义关系之前本教程中使用的每个模式的结构。

### 忠诚会员模式

源模式“Loyalty Members”是在教程中构建的用于在 [UI中创建模式的模式](create-schema-ui.md)。 它在其“\_tenantId”命名空间下包含“loyalty”对象，该对象包括若干特定于忠诚度的字段。 其中一个字段“loyaltyId”在“电子邮件”命名空间下充当模式的主要标识。 如模式属 _性下所示_，此模式已启用 [在实时客户用户档案中使用](../../profile/home.md)。

![](../images/tutorials/relationship/loyalty-members.png)

### 酒店模式

目的地模式“酒店”包含描述酒店的字段，包括其地址、品牌、房间数和星级等级。 “hotelId”字段用作“ECID”模式下该命名空间的主标识。 与“忠诚会员”不同，此模式尚未启用实时客户用户档案。

![](../images/tutorials/relationship/hotels.png)

## 创建关系混合

>[!NOTE]
>
>仅当源模式没有专用的字符串类型字段用作对其他模式的引用时，才需要执行此步骤。 如果此字段已在源模式中定义，请跳到定义关系字 [段的下一步](#relationship-field)。

要定义两个模式之间的关系，源模式必须有一个专用字段，用作对目标模式的引用。 您可以通过创建新混音将此字段添加到源模式。

开始, **方法是** 在Mixins _部分中_ 单击Add。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

将出 _现“添加混合_ ”对话框。 在此处，单击“ **新建混音”**。 在显示的文本字段中，输入新混音的显示名称和说明。 完成 **后，单击** “添加混音”。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

画布将重新显示，“忠诚度关系”将显示在“ _Mixins_ ”部分。 单击混音名称，然后单 **击根级** “Loyalty Members”字段旁的“添加字段”。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的“\_tenantId”命名空间下将显示一个新字段。 在“ _字段属性_”下，为字段提供字段名称和显示名称，并将其类型设置为“字符串”。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，单击“ **应用**”。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的“loyaltyRelationship”字段将显示在画布中。 单击 **保存** ，以完成对模式所做的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源模式定义关系字段 {#relationship-field}

在源模式定义了专用的引用字段后，您可以将其指定为关系字段。

单击画布中的引用字段，然后在字段属性下 _向下滚动_ ，直到 **出现** “关系”复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

单击“参考 **模式** ”的下拉列表，然后选择关系的目标模式（本例中的“酒店”）。 如果目标模式启用了合并 **** ，则“引用标识命名空间”字段将自动设置为目标模式的主标识的命名空间。 如果模式未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

该字段在画布中显示为关系，显示目标模式的名称和引用标识命名空间。 单击 **保存** ，以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过遵循本教程，您已成功使用模式编辑器在两个模式之间创建了一对一关系。 有关如何使用API定义关系的步骤，请参阅有关使用 [模式注册表API定义关系的教程](relationship-api.md)。