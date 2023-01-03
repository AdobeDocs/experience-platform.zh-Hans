---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 如何配置计算属性字段
topic-legacy: guide
type: Documentation
description: 计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 要配置计算属性，您首先需要标识将包含计算属性值的字段。 可以使用架构字段组创建此字段以将该字段添加到现有架构，或通过选择已在架构中定义的字段来创建此字段。
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha)在UI中配置计算属性字段

>[!IMPORTANT]
>
>计算属性功能当前位于Alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

要配置计算属性，您首先需要标识将包含计算属性值的字段。 可以使用架构字段组创建此字段以将该字段添加到现有架构，或通过选择已在架构中定义的字段来创建此字段。

>[!NOTE]
>
>计算属性无法添加到Adobe定义的字段组内的字段。 字段必须位于 `tenant` 命名空间，这意味着它必须是您定义并添加到架构的字段。

要成功定义计算的属性字段，必须为 [!DNL Profile] 并作为该架构所基于的类的并集架构的一部分显示。 有关 [!DNL Profile]启用了架构和联合，请查看 [!DNL Schema Registry] 开发人员指南部分 [启用用于用户档案和查看并集模式的模式](../../xdm/api/getting-started.md). 此外，还建议您查看 [工会一节](../../xdm/schema/composition.md) 在架构合成基础文档中。

本教程中的工作流使用 [!DNL Profile]-enabled架构，并遵循以下步骤：定义包含计算属性字段的新字段组，并确保它是正确的命名空间。 如果在启用了用户档案的架构中，已有一个字段处于正确的命名空间中，则可以直接继续执行的步骤 [创建计算属性](#create-a-computed-attribute).

## 查看架构

以下步骤使用Adobe Experience Platform用户界面查找架构、添加字段组和定义字段。 如果您希望使用 [!DNL Schema Registry] API，请参阅 [架构注册开发人员指南](../../xdm/api/getting-started.md) 有关如何创建字段组、将字段组添加到架构以及启用用于的架构的步骤 [!DNL Real-Time Customer Profile].

在用户界面中，单击 **[!UICONTROL 模式]** ，并使用 **[!UICONTROL 浏览]** 选项卡，以快速查找要更新的架构。

![](../images/computed-attributes/Schemas-Browse.png)

找到架构后，单击其名称以打开 [!DNL Schema Editor] 您可以在此处对架构进行编辑。

![](../images/computed-attributes/Schema-Editor.png)

## 创建字段组

要创建新字段组，请单击 **[!UICONTROL 添加]** 下一页 **[!UICONTROL 字段组]** 在 **[!UICONTROL 组合物]** 的子菜单。 这将打开 **[!UICONTROL 添加字段组]** 对话框中，您可以看到现有字段组。 单击 **[!UICONTROL 创建新字段组]** 以定义新字段组。

为字段组提供名称和描述，然后单击 **[!UICONTROL 添加字段组]** 完成时。

![](../images/computed-attributes/Add-field-group.png)

## 向架构添加计算属性字段

您的新字段组现在应显示在“[!UICONTROL 字段组]“”部分[!UICONTROL 组合物]&quot; 单击字段组和多个 **[!UICONTROL 添加字段]** 按钮将显示在 **[!UICONTROL 结构]** 的子代。

选择 **[!UICONTROL 添加字段]** 在架构名称旁边添加顶级字段，或选择在您喜欢的架构内的任意位置添加该字段。

单击 **[!UICONTROL 添加字段]** 随即会打开一个新对象，该对象以您的租户ID命名，表示该字段位于正确的命名空间中。 在该对象中， **[!UICONTROL 新建字段]** 中。 如果要在其中定义计算属性的字段，则使用此选项。

![](../images/computed-attributes/New-field.png)

## 配置字段

使用 **[!UICONTROL 字段属性]** 部分，为新字段提供必需的信息，包括其名称、显示名称和类型。

>[!NOTE]
>
>字段的类型必须与计算属性值的类型相同。 例如，如果计算的属性值是字符串，则架构中定义的字段必须是字符串。

完成后，单击 **[!UICONTROL 应用]** 和字段的名称及其类型将显示在 **[!UICONTROL 结构]** 的子代。

![](../images/computed-attributes/Apply.png)

## 为启用架构 [!DNL Profile]

在继续操作之前，请确保已为 [!DNL Profile]. 单击 **[!UICONTROL 结构]** 部分，以便 **[!UICONTROL 架构属性]** 选项卡。 如果 **[!UICONTROL 用户档案]** 滑块为蓝色，已为 [!DNL Profile].

>[!NOTE]
>
>启用模式 [!DNL Profile] 无法撤消，因此，如果在启用滑块后单击该滑块，则不必冒险将其禁用。

![](../images/computed-attributes/Profile.png)

您现在可以单击 **[!UICONTROL 保存]** 要保存更新的架构，并继续使用API完成教程的其余部分。

## 后续步骤

现在，您已创建一个字段，计算属性值将存储到该字段中，接下来可以使用 `/computedattributes` API端点。 有关在API中创建计算属性的详细步骤，请按照 [计算属性API端点指南](ca-api.md).