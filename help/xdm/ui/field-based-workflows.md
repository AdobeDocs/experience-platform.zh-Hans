---
title: 架构编辑器（测试版）中基于字段的工作流
description: 了解如何将现有字段组中的字段单独添加到体验数据模型(XDM)架构。
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: c1b1a3b18a9950d71fb84e463adc973ab45ba563
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# 架构编辑器（测试版）中基于字段的工作流

>[!IMPORTANT]
>
>此测试版文档中描述的工作流现已在Adobe Experience Platform中正式提供。 有关架构编辑器中基于字段的工作流的最新指导，请参阅 [模式UI指南](./resources/schemas.md) 中。 本指南很快将被删除。

Adobe Experience Platform提供了一套强大的标准化 [字段组](../schema/composition.md#field-group) ，以用于体验数据模型(XDM)架构。 这些字段组背后的结构和语义经过精心定制，以满足平台中各种分段用例和其他下游应用程序的需求。 您还可以定义自己的自定义字段组以满足独特的业务需求。

在将字段组添加到架构时，该架构会继承该组中包含的所有字段。 但是，您现在可以向架构中添加单个字段，而无需包括关联字段组中可能不一定使用的其他字段。

本指南介绍了将各个字段添加到Platform UI架构的不同方法。

## 先决条件

本教程假定您熟悉 [XDM模式的构成](../schema/composition.md) 以及如何在平台UI中使用架构编辑器。 接下来，您应该开始 [创建新模式](./resources/schemas.md) 并将其分配到标准类，然后再继续阅读本指南。

## 删除从标准字段组添加的字段

在将标准字段组添加到架构后，您可以删除您不需要的任何标准字段。

>[!NOTE]
>
>从标准字段组中删除字段仅会影响正在处理的架构，而不会影响字段组本身。 如果删除一个架构中的标准字段，则这些字段在使用相同字段组的所有其他架构中仍然可用。

在以下示例中，标准字段组 **[!UICONTROL 人口统计详细信息]** 已添加到架构中。 删除单个字段，例如 `taxId`，选择画布中的字段，然后选择 **[!UICONTROL 删除]** 中。

![删除单个字段](../images/ui/field-based-workflows/remove-single-field.png)

如果要删除多个字段，则可以将字段组作为一个整体进行管理。 在画布中选择属于该组的字段，然后选择 **[!UICONTROL 管理相关字段]** 中。

![管理相关字段](../images/ui/field-based-workflows/manage-related-fields.png)

将显示一个对话框，其中显示了相关字段组的结构。 从此处，您可以使用提供的复选框来选择或取消选择所需的字段。 当您满意时，选择 **[!UICONTROL 确认]**.

![从字段组中选择字段](../images/ui/field-based-workflows/select-fields.png)

画布将重新显示，只显示架构结构中存在的选定字段。

![添加的字段](../images/ui/field-based-workflows/fields-added.png)

## 将标准字段直接添加到架构

您可以将标准字段组中的字段直接添加到架构，而无需事先知道其相应的字段组。 要向架构添加标准字段，请选择加号(**+**)图标。 安 **[!UICONTROL 无标题字段]** 占位符显示在架构结构中，并且右侧边栏会更新，以显示用于配置字段的控件。

![字段占位符](../images/ui/field-based-workflows/root-custom-field.png)

在 **[!UICONTROL 字段名称]**，开始键入要添加的字段名称。 系统会自动搜索与查询匹配的标准字段，并在 **[!UICONTROL 推荐的标准字段]**，包括其所属的字段组。

![推荐的标准字段](../images/ui/field-based-workflows/standard-field-search.png)

虽然某些标准字段具有相同的名称，但其结构可能会因其来源的字段组而异。 如果标准字段嵌套在字段组结构的父对象中，则如果添加了子字段，则父字段也将包含在架构中。

选择预览图标(![“预览”图标](../images/ui/field-based-workflows/preview-icon.png))以查看其字段组的结构，并更好地了解其嵌套方式。 要将标准字段添加到架构，请选择加号图标(![加号图标](../images/ui/field-based-workflows/add-icon.png))。

![添加标准字段](../images/ui/field-based-workflows/add-standard-field.png)

画布会更新，以显示已添加到架构的标准字段，包括该架构嵌套在字段组结构下的任何父字段。 字段组的名称也列在 **[!UICONTROL 字段组]** 中。 如果要从同一字段组添加更多字段，请选择 **[!UICONTROL 管理相关字段]** 中。

![添加了标准字段](../images/ui/field-based-workflows/standard-field-added.png)

## 将自定义字段直接添加到架构

与标准字段的工作流类似，您还可以将自己的自定义字段直接添加到架构中。

要将字段添加到架构的根级别，请选择加号(**+**)图标。 安 **[!UICONTROL 无标题字段]** 占位符显示在架构结构中，并且右侧边栏会更新，以显示用于配置字段的控件。

![根自定义字段](../images/ui/field-based-workflows/root-custom-field.png)

开始在要添加的字段名称中键入内容，系统将自动开始搜索匹配的标准字段。 要改为创建新的自定义字段，请选择附加的顶部选项 **([!UICONTROL 新建字段])**.

![新建字段](../images/ui/field-based-workflows/custom-field-search.png)

从此处，提供字段的显示名称和数据类型。 在 **[!UICONTROL 分配字段组]**，则必须为要关联的新字段选择字段组。 开始键入字段组的名称，如果您之前 [创建自定义字段组](./resources/field-groups.md#create) 它们将显示在下拉列表中。 或者，您也可以在字段中键入唯一名称，以改为创建新字段组。

![选择字段组](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>如果您选择了现有的自定义字段组，则采用该字段组的任何其他架构也将在您保存更改后继承新添加的字段。 因此，仅当您需要此类型的传播时，才应选择现有的字段组。 否则，您应该选择创建新的自定义字段组。

完成后，选择 **[!UICONTROL 应用]**.

![应用字段](../images/ui/field-based-workflows/apply-field.png)

新字段将添加到画布中，并且名称位于 [租户ID](../api/getting-started.md#know-your-tenant_id) 以避免与标准XDM字段冲突。 与新字段关联的字段组也显示在 **[!UICONTROL 字段组]** 中。

![租户ID](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>默认情况下，所选自定义字段组提供的其余字段将从架构中删除。 如果要向架构添加其中一些字段，请选择属于该组的字段，然后选择 **[!UICONTROL 管理相关字段]** 中。

### 将自定义字段添加到标准字段组的结构

如果您正在处理的架构具有由标准字段组提供的对象类型字段，则可以向该标准对象添加您自己的自定义字段。 选择加号(**+**)图标，并在右边栏中提供自定义字段的详细信息。

![向标准对象添加字段](../images/ui/field-based-workflows/add-field-to-standard-object.png)

应用更改后，新字段将显示在标准对象中的租户ID命名空间下。 此嵌套命名空间可防止字段组本身内的字段名称冲突，以避免破坏使用同一字段组的其他架构中的更改。

![添加到标准对象的字段](../images/ui/field-based-workflows/added-to-standard-object.png)

## 后续步骤

本指南介绍了平台UI中架构编辑器的新的基于字段的工作流。 有关在UI中管理架构的更多信息，请参阅 [UI概述](./overview.md).
