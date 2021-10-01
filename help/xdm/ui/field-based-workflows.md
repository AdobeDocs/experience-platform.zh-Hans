---
title: 架构编辑器中基于字段的工作流
description: 了解如何将Adobe定义的字段组中的标准字段单独添加到体验数据模型(XDM)架构中。
hide: true
hidefromtoc: true
source-git-commit: 8947fbb815f3eda97fb218be6791cb67e6e66719
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 架构编辑器中基于字段的工作流

Adobe Experience Platform提供了一组功能强大的标准化[字段组](../schema/composition.md#field-group)，以用于体验数据模型(XDM)架构。 这些字段组背后的结构和语义经过精心定制，以满足平台中各种分段用例和其他下游应用程序的需求。 您还可以定义自己的自定义字段组以满足独特的业务需求。

在将字段组添加到架构时，该架构会继承该组中包含的所有字段。 但是，您现在可以向架构中添加单个字段，而无需包括关联字段组中可能不一定使用的其他字段。

本指南介绍了将各个字段添加到Platform UI架构的不同方法。

## 先决条件

本教程假定您熟悉XDM架构](../schema/composition.md)的[组成，以及如何在平台UI中使用架构编辑器。 接下来，您应该开始创建新架构](./resources/schemas.md)并将其分配给标准类的过程，然后再继续阅读本指南。[

## 删除从标准字段组添加的字段

在将标准字段组添加到架构后，您可以删除您不需要的任何标准字段。

>[!NOTE]
>
>从标准字段组中删除字段仅会影响正在处理的架构，而不会影响字段组本身。 如果删除一个架构中的标准字段，则这些字段在使用相同字段组的所有其他架构中仍然可用。

在以下示例中，标准字段组&#x200B;**[!UICONTROL 人口统计详细信息]**&#x200B;已添加到架构中。 要删除单个字段（如`taxId`），请在画布中选择该字段，然后在右边栏中选择&#x200B;**[!UICONTROL Remove]**。

![删除单个字段](../images/ui/field-based-workflows/remove-single-field.png)

如果要删除多个字段，则可以将字段组作为一个整体进行管理。 在画布中选择属于该组的字段，然后选择右边栏中的&#x200B;**[!UICONTROL 管理相关字段]**。

![管理相关字段](../images/ui/field-based-workflows/manage-related-fields.png)

将显示一个对话框，其中显示了相关字段组的结构。 从此处，您可以使用提供的复选框来选择或取消选择所需的字段。 如果您满意，请选择&#x200B;**[!UICONTROL 添加字段]**。

![从字段组中选择字段](../images/ui/field-based-workflows/select-fields.png)

画布将重新显示，只显示架构结构中存在的选定字段。

![添加的字段](../images/ui/field-based-workflows/fields-added.png)

## 将自定义字段直接添加到架构

如果您之前已[创建自定义字段组](./resources/field-groups.md#create)，则可以直接将自定义字段添加到架构中，而无需预先将它们单独添加到自定义字段组。

>[!WARNING]
>
>在将自定义字段添加到架构时，您仍必须选择要与其关联的现有自定义字段组。 这意味着要将自定义字段直接添加到架构，您必须至少在正在使用的沙盒中定义一个自定义字段组。 此外，使用该自定义字段组的任何其他架构也将在您保存更改后继承新添加的字段。

要向架构的根级别添加字段，请在画布中选择架构名称旁边的加号(**+**)图标。 架构结构中会显示一个&#x200B;**[!UICONTROL 无标题字段]**&#x200B;占位符，右边栏会更新以显示用于配置字段的控件。

![根自定义字段](../images/ui/field-based-workflows/root-custom-field.png)

使用右边栏中的控件为字段提供名称、显示名称和数据类型。 在&#x200B;**[!UICONTROL 分配字段组]**&#x200B;下，选择要与新字段关联的自定义字段组。

![选择字段组](../images/ui/field-based-workflows/select-field-group.png)

完成后，选择&#x200B;**[!UICONTROL Apply]**。

![应用字段](../images/ui/field-based-workflows/apply-field.png)

新字段将添加到画布中，并在[租户ID](../api/getting-started.md#know-your-tenant_id)下命名，以避免与标准XDM字段冲突。 与新字段关联的字段组也显示在左边栏的&#x200B;**[!UICONTROL 字段组]**&#x200B;下。

![租户ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>默认情况下，所选自定义字段组提供的其余字段将从架构中删除。 如果要向架构中添加其中一些字段，请选择属于该组的字段，然后选择右边栏中的&#x200B;**[!UICONTROL 管理相关字段]**。

### 向标准字段组的结构中添加字段

如果您正在处理的架构具有由标准字段组提供的对象类型字段，则可以向该标准对象添加您自己的自定义字段。 选择对象根旁边的加号(**+**)图标，并在右边栏中提供自定义字段的详细信息。

![向标准对象添加字段](../images/ui/field-based-workflows/add-field-to-standard-object.png)

应用更改后，新字段将显示在标准对象中的租户ID命名空间下。 此嵌套命名空间可防止字段组本身内的字段名称冲突，以避免破坏使用同一字段组的其他架构中的更改。

## 后续步骤

本指南介绍了平台UI中架构编辑器的新的基于字段的工作流。 有关在UI中管理架构的更多信息，请参阅[UI概述](./overview.md)。
