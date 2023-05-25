---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 如何配置计算属性字段
type: Documentation
description: 计算属性是用于将事件级数据聚合到配置文件级属性的函数。 要配置计算属性，您首先需要标识将保存计算属性值的字段。 此字段可以使用架构字段组创建，以将该字段添加到现有架构，或者通过选择已在架构中定义的字段来创建。
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha)在UI中配置计算属性字段

>[!IMPORTANT]
>
>计算属性功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。

要配置计算属性，您首先需要标识将保存计算属性值的字段。 此字段可以使用架构字段组创建，以将该字段添加到现有架构，或者通过选择已在架构中定义的字段来创建。

>[!NOTE]
>
>无法将计算属性添加到Adobe定义的字段组中的字段。 该字段必须在 `tenant` 命名空间，这意味着它必须是您定义并添加到架构的字段。

为了成功定义计算属性字段，必须为以下项启用架构 [!DNL Profile] 和将作为架构所基于的类的合并架构的一部分显示。 有关的详细信息 [!DNL Profile] — 启用的架构和联合，请查看 [!DNL Schema Registry] 开发人员指南部分，位于 [为配置文件启用架构并查看合并架构](../../xdm/api/getting-started.md). 此外，还建议审查 [关于合并的部分](../../xdm/schema/composition.md) 架构组合基础知识文档中的。

本教程中的工作流使用 [!DNL Profile]-enabled架构并按照以下步骤操作：定义包含计算属性字段的新字段组并确保它是正确的命名空间。 如果您在启用了配置文件的架构中已有字段位于正确的命名空间中，则可以直接进入以下步骤 [创建计算属性](#create-a-computed-attribute).

## 查看架构

后续步骤使用Adobe Experience Platform用户界面查找架构、添加字段组和定义字段。 如果您希望使用 [!DNL Schema Registry] API，请参阅 [Schema Registry开发人员指南](../../xdm/api/getting-started.md) 有关如何创建字段组的步骤，请将字段组添加到架构，并启用架构以用于 [!DNL Real-Time Customer Profile].

在用户界面中，单击 **[!UICONTROL 架构]** 左边栏中的任意位置，并使用 **[!UICONTROL 浏览]** 选项卡，以快速找到要更新的架构。

![](../images/computed-attributes/Schemas-Browse.png)

找到架构后，单击其名称以打开 [!DNL Schema Editor] 您可以在其中编辑架构。

![](../images/computed-attributes/Schema-Editor.png)

## 创建字段组

要创建新字段组，请单击 **[!UICONTROL 添加]** 旁边 **[!UICONTROL 字段组]** 在 **[!UICONTROL 合成]** 部分。 这将打开 **[!UICONTROL 添加字段组]** 用于查看现有字段组的对话框。 单击单选按钮 **[!UICONTROL 创建新字段组]** 以定义您的新字段组。

为字段组指定名称和描述，然后单击 **[!UICONTROL 添加字段组]** 完成时。

![](../images/computed-attributes/Add-field-group.png)

## 将计算属性字段添加到架构

您的新字段组现在应显示在“[!UICONTROL 字段组]“ ”下的“ ”部分[!UICONTROL 合成]“。 单击字段组的名称，然后单击 **[!UICONTROL 添加字段]** 按钮将显示在 **[!UICONTROL 结构]** 部分。

选择 **[!UICONTROL 添加字段]** ，以添加顶级字段，或者您可以选择在喜欢的架构内的任意位置添加该字段。

单击后 **[!UICONTROL 添加字段]** 此时将打开一个新对象，该对象以您的租户ID命名，表明字段位于正确的命名空间中。 在该对象内， **[!UICONTROL 新建字段]** 显示。 这是指将在其中定义计算属性的字段。

![](../images/computed-attributes/New-field.png)

## 配置字段

使用 **[!UICONTROL 字段属性]** 部分，提供新字段的必要信息，包括其名称、显示名称和类型。

>[!NOTE]
>
>字段的类型必须与计算属性值类型相同。 例如，如果计算属性值是一个字符串，则在架构中定义的字段必须是字符串。

完成后，单击 **[!UICONTROL 应用]** 和字段的名称及其类型将显示在 **[!UICONTROL 结构]** 部分。

![](../images/computed-attributes/Apply.png)

## 为以下项启用架构 [!DNL Profile]

在继续之前，请确保已为以下项启用架构： [!DNL Profile]. 单击中的架构名称 **[!UICONTROL 结构]** 部分，以便 **[!UICONTROL 架构属性]** 选项卡。 如果 **[!UICONTROL 个人资料]** 滑块为蓝色，表示已为以下项启用架构： [!DNL Profile].

>[!NOTE]
>
>启用架构 [!DNL Profile] 无法撤消，因此，如果在启用滑块后单击该滑块，则不必冒险禁用它。

![](../images/computed-attributes/Profile.png)

您现在可以单击 **[!UICONTROL 保存]** 以保存更新的架构，并使用API继续本教程的其余部分。

## 后续步骤

现在，您已创建一个字段，计算属性值将存储到该字段中，接下来可以使用 `/computedattributes` API端点。 有关在API中创建计算属性的详细步骤，请按照 [计算属性API端点指南](ca-api.md).