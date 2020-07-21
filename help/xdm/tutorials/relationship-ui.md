---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用模式模式编辑器定义两个模式之间的关系
topic: tutorials
translation-type: tm+mt
source-git-commit: 1445646be8fa3416a34408205eadca0a792290c6
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# 使用 [!DNL Schema Editor]

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要组成部分。 在(XDM)模式结构中定 [!DNL Experience Data Model] 义这些关系，使您能够对客户数据获得复杂的洞察。

此文档提供了一个教程，用于定义组织使用用户界面中定义的两个模式之间的一 [!DNL Schema Editor] 对一 [!DNL Experience Platform] 关系。 有关使用API定义模式关系的步骤，请参阅使用 [模式注册表API定义关系的教程](relationship-api.md)。

## 入门指南

本教程需要对UI中 [!DNL XDM System] 的内 [!DNL Schema Editor] 容和内 [!DNL Experience Platform] 容进行了解。 在开始本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md): XDM及其在Experience Platform中实现的概述。
* [模式合成基础](../schema/composition.md): 介绍XDM模式的构件。
* [使用模式编辑器创建模式](create-schema-ui.md): 一个教程，其中介绍使用的基础知 [!DNL Schema Editor]识。

## 定义源和目标模式

您应已创建将在关系中定义的两个模式。 为了进行演示，本教程在组织的忠诚项目(在“忠诚会员”模式中定义)的成员与其喜爱的酒店(在“[!UICONTROL 酒店]”模式中定义)之间建立了关系。

模式关系由源 **[!UICONTROL 模式表示]** ，该源具有引用目标模式内的另 **[!UICONTROL 一个字段]**。 在接下来的步骤中，“[!UICONTROL 忠诚会员]”将作为源模式，而“酒店”将充当目标模式。

为便于参考，以下各节将介绍本教程中在定义关系之前使用的每个模式的结构。

### [!UICONTROL 忠诚会员] 模式

源模式“[!UICONTROL Loyalty Members]”是在教程中构建的用于 [在UI中创建模式的模式](create-schema-ui.md)。 它在其“[!UICONTROL \_tenantId]”命名空间下包含一个[!UICONTROL “loyalty]”对象，该对象包括若干特定于忠诚度的字段。 其中一个字段“[!UICONTROL loyaltyId]”在“电子邮件”模式下充当该命名空间的[!UICONTROL 主要]标识。 如“模式 _属性_”下所示，此模式已在中启用 [!DNL Real-time Customer Profile](../../profile/home.md)。

![](../images/tutorials/relationship/loyalty-members.png)

### 酒店模式

目标模式“[!UICONTROL 酒店]”包含描述酒店的字段，包括其地址、品牌、房间数和星级等级。 “[!UICONTROL hotelId]”字段用作“ECID”命名空间下模式的主标识。 与“[!UICONTROL 忠诚会员]”不同，此模式尚未启用 [!DNL Real-time Customer Profile]。

![](../images/tutorials/relationship/hotels.png)

## 创建关系混合

>[!NOTE]
>
>仅当源模式没有专用的字符串类型字段用作对其他模式的引用时，才需要执行此步骤。 如果此字段已在源模式中定义，请跳到定义关系字 [段的下一步](#relationship-field)。

要定义两个模式之间的关系，源模式必须有一个专用字段，用作对目标模式的引用。 您可以通过创建新混音将此字段添加到源模式。

开始, **[!UICONTROL 方法是]** 在Mixins _部分中_ 单击Add。

![](../images/tutorials/relationship/loyalty-add-mixin.png)

将出 [!UICONTROL _现“添加混合&#x200B;_]”对话框。 在此处，单击“**[!UICONTROL &#x200B;新建混音”]**。 在显示的文本字段中，输入新混音的显示名称和说明。 完成**[!UICONTROL &#x200B;后，单击&#x200B;]**“添加混音”。

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

画布将重新显示，“[!UICONTROL Favorite Hotel]”将出现在 _Mixins部分_ 。 单击混音名称，然后单 **[!UICONTROL 击根级]** “Loyalty Members”字段旁[!UICONTROL 的“添加]字段”。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中的“\_tenantId”命名空间下[!UICONTROL 将显示一个新]字段。 在“ [!UICONTROL _字段属性&#x200B;_]”下，提供字段的字段名称和显示名称，并将其类型设置为“[!UICONTROL 字符串]”。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，单击“ **[!UICONTROL 应用]**”。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的“[!UICONTROL favoriteHotel]”字段显示在画布中。 单击 **[!UICONTROL 保存]** ，以完成对模式所做的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源模式定义关系字段 {#relationship-field}

在源模式定义了专用的引用字段后，您可以将其指定为关系字段。

单击画布中的引用字段，然后在字段属性下 _[!UICONTROL 向下滚动]_，直到**[!UICONTROL &#x200B;出现&#x200B;]**“关系”复选框。 选中此复选框可显示配置关系字段所需的参数。

![](../images/tutorials/relationship/relationship-checkbox.png)

单击“参考 **[!UICONTROL 模式]** ”的下拉列表[!UICONTROL ，然后选择关系的目标模式(本例]中为“Hotels”)。 如果目标模式启用了合并 **** ，则“引用标识命名空间”字段将自动设置为目标模式的主标识的命名空间。 如果模式未定义主标识，则必须从下拉菜单中手动选择您计划使用的命名空间。 Click **[!UICONTROL Apply]** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

该字段在画布中显示为关系，显示目标模式的名称和引用标识命名空间。 单击 **[!UICONTROL 保存]** ，以保存更改并完成工作流。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

通过遵循本教程，您已成功地使用创建了两个模式之间的一对一关系 [!DNL Schema Editor]。 有关如何使用API定义关系的步骤，请参阅有关使用 [模式注册表API定义关系的教程](relationship-api.md)。