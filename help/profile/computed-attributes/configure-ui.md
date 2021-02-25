---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 如何配置计算属性字段
topic: 指南
type: 文档
description: 计算属性是用于将事件级数据聚合为用户档案级属性的函数。 要配置计算属性，您首先需要标识将包含计算属性值的字段。 可以使用混音创建此字段，以将该字段添加到现有模式，或通过选择已在模式中定义的字段来创建此字段。
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# (Alpha)在UI中配置计算属性字段

>[!IMPORTANT]
>
>计算属性功能当前位于Alpha中，并且不适用于所有用户。 文档和功能可能会发生变化。

要配置计算属性，您首先需要标识将包含计算属性值的字段。 可以使用混音创建此字段，以将该字段添加到现有模式，或通过选择已在模式中定义的字段来创建此字段。

>[!NOTE]
>
>无法将计算属性添加到Adobe定义的混音中的字段。 该字段必须位于`tenant`命名空间内，这意味着它必须是您定义并添加到模式的字段。

为了成功定义计算的属性字段，必须为[!DNL Profile]启用模式，并作为模式所基于的类的合并模式的一部分显示。 有关[!DNL Profile]启用的模式和合并的详细信息，请查看[上[!DNL Schema Registry]开发人员指南部分中启用用户档案和查看合并模式的模式的部分](../../xdm/api/getting-started.md)。 还建议查看模式合成基础文档中关于合并](../../xdm/schema/composition.md)的[部分。

本教程中的工作流使用启用了[!DNL Profile]的模式，并遵循定义包含计算属性字段的新混音并确保它是正确命名空间的步骤。 如果已在启用用户档案的模式中有一个字段处于正确命名空间，则可以直接继续执行创建计算属性](#create-a-computed-attribute)的步骤。[

## 视图模式

随后的步骤使用Adobe Experience Platform用户界面查找模式、添加混音和定义字段。 如果您希望使用[!DNL Schema Registry] API，请参阅[模式注册表开发人员指南](../../xdm/api/getting-started.md)，了解有关如何创建混音、向模式添加混音以及启用模式以与[!DNL Real-time Customer Profile]一起使用的步骤。

在用户界面中，单击左边栏中的&#x200B;**[!UICONTROL 模式]**，然后使用&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡上的搜索栏快速找到要更新的模式。

![](../images/computed-attributes/Schemas-Browse.png)

找到模式后，单击其名称以打开[!DNL Schema Editor]，您可以在其中编辑模式。

![](../images/computed-attributes/Schema-Editor.png)

## 创建混音

要创建新混音，请单击编辑器左侧&#x200B;**[!UICONTROL 合成]**&#x200B;部分中&#x200B;**[!UICONTROL 混音]**&#x200B;旁边的&#x200B;**[!UICONTROL 添加]**。 这会打开&#x200B;**[!UICONTROL 添加混音]**&#x200B;对话框，您可以在其中看到现有混音。 单击&#x200B;**[!UICONTROL “新建混音]**”的单选按钮以定义新混音。

为混音指定名称和说明，完成后单击&#x200B;**[!UICONTROL 添加混音]**。

![](../images/computed-attributes/Add-mixin.png)

## 向模式添加计算属性字段

您的新混音现在应显示在“[!UICONTROL 合成]”下的“[!UICONTROL Mixins]”部分中。 单击混音的名称，编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分将显示多个&#x200B;**[!UICONTROL 添加字段]**&#x200B;按钮。

选择模式名称旁的&#x200B;**[!UICONTROL 添加字段]**&#x200B;以添加顶级字段，也可以选择在您喜欢的模式的任意位置添加字段。

单击&#x200B;**[!UICONTROL 添加字段]**&#x200B;后，将打开一个新对象，该对象以您的租户ID命名，表明该字段处于正确命名空间。 在该对象中，将显示&#x200B;**[!UICONTROL 新字段]**。 如果要定义计算属性的字段，则为此。

![](../images/computed-attributes/New-field.png)

## 配置字段

使用编辑器右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;部分，为新字段提供必要信息，包括其名称、显示名称和类型。

>[!NOTE]
>
>字段的类型必须与计算的属性值相同。 例如，如果计算的属性值是字符串，则模式中定义的字段必须是字符串。

完成后，单击&#x200B;**[!UICONTROL 应用]**，该字段的名称及其类型将显示在编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分。

![](../images/computed-attributes/Apply.png)

## 为[!DNL Profile]启用模式

在继续之前，请确保已为[!DNL Profile]启用模式。 单击编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分中的模式名称，以显示&#x200B;**[!UICONTROL 模式属性]**&#x200B;选项卡。 如果&#x200B;**[!UICONTROL 用户档案]**&#x200B;滑块为蓝色，则已为[!DNL Profile]启用模式。

>[!NOTE]
>
>为[!DNL Profile]启用模式无法撤消，因此，如果在启用滑块后单击该滑块，则不必冒险禁用它。

![](../images/computed-attributes/Profile.png)

您现在可以单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更新的模式，并使用API继续教程的其余部分。

## 后续步骤

现在，您已创建了一个字段，将计算属性值存储到该字段中，可以使用`/computedattributes` API端点创建计算属性。 有关在API中创建计算属性的详细步骤，请按照[计算属性API端点指南](ca-api.md)中提供的步骤进行操作。