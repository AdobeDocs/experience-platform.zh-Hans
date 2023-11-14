---
title: 弃用UI中的XDM字段
description: 了解如何使用Experience Platform中的架构编辑器弃用Experience Data Model (XDM)字段。
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 在UI中弃用XDM字段

体验数据模型(XDM)让您在摄取数据后通过弃用架构字段而灵活地管理数据模型，以应对业务需求的变化。 可以弃用不需要的字段，以便从UI视图中删除它们，同时在下游UI中隐藏它们。 方便之处在于，架构编辑器中的复选框允许您显示已弃用的字段，如有必要，您还可以取消弃用它们。

由于默认情况下已从UI中隐藏已弃用的字段，因此这可以简化架构编辑器中的架构，并防止将不需要的字段添加到下游依赖项，例如区段生成器、历程设计器等。 字段弃用也可以向后兼容。 使用已弃用字段的其他系统（如受众和查询）将继续按预期进行评估。 如果在一个现有受众中使用了一个已弃用的字段，则会正常处理该字段，这意味着该字段会按预期显示在区段生成器的画布中，或根据已弃用字段中提供的任何数据进行评估。 这是一项不间断的更改，不会对任何现有数据流产生负面影响。

>[!NOTE]
>
>将数据摄取到架构中之前，您可以删除不必要的字段组。 请参阅相关文档 [如何从架构中删除字段组](../ui/resources/schemas.md#remove-fields) 以了解更多信息。

一旦将数据摄取到架构中，您就无法再从架构中删除字段而无需进行重大更改。 在这种情况下，您可以使用来弃用架构或自定义资源中的不需要字段 [架构编辑器](./create-schema-ui.md) 或 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

本文档介绍如何使用Experience Platform用户界面中的架构编辑器来弃用其他XDM资源的字段。 有关使用API弃用XDM字段的步骤，请参阅上的教程 [使用架构注册表API弃用XDM字段](./field-deprecation-api.md).

## 弃用字段 {#deprecate}

要弃用自定义字段，请导航到要编辑的架构的架构编辑器。 从中选择要弃用的字段 [!UICONTROL 结构] 部分，然后是 **[!UICONTROL 弃用]** 从 [!UICONTROL 字段属性].

![架构编辑器，其中选中了字段，并突出显示了“弃用” 。](../images/tutorials/field-deprecation/deprecate-single-field.png)

此时将显示一个对话框，用于确认您的选择并通知您，该字段将从合并架构的UI视图中删除并隐藏在下游UI中。 要完成操作，请选择 **[!UICONTROL 确认]**.

![弃用字段对话框，其中突出显示了确认。](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

该字段现已从UI视图中删除。

>[!NOTE]
>
>一旦弃用，下游UI(例如分段功能板、Customer Journey Analytics和Adobe Journey Optimizer)将不再将已弃用的字段作为其工作流的一部分显示。 但是，下游UI会根据需要选择显示已弃用的字段，并继续正常处理已弃用的字段。 有关更多信息，请参阅其各自的文档。 使用已弃用字段的查询和受众将继续按预期运行。

## 显示已弃用的字段 {#show-deprecated}

要查看以前弃用的字段，请导航到架构编辑器中的相关架构。 选择 **[!UICONTROL 显示已弃用的字段]** 中的复选框 [!UICONTROL 合成] 部分。

已弃用的字段现在显示在UI视图中。 选择 **[!UICONTROL 保存]** 以确认您的设置。

![架构编辑器中选择了字段，并突出显示显示已弃用的字段和保存。](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## 取消弃用字段 {#undeprecate-fields}

要撤消已弃用的字段，请首先 [显示已弃用的字段](#show-deprecated) 如上所述，然后从编辑器的 [!UICONTROL 结构] 部分。 接下来，选择 **[!UICONTROL 取消弃用]** 从 [!UICONTROL 字段属性] 侧栏后跟 **[!UICONTROL 保存]**.

![架构编辑器中，已弃用字段“Undeprecated”（取消弃用）和“Save”（保存）突出显示。](../images/tutorials/field-deprecation/undeprecate-single-field.png)

此 [!UICONTROL 取消弃用字段] 出现对话框。 要确认更改，请选择 **[!UICONTROL 确认]**.

![此 [!UICONTROL 取消弃用字段] 对话框，其中突出显示了确认。](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

字段现在在UI视图和下游UI中显示为标准字段。 同样，您现在可以选择弃用字段。

## 后续步骤

本文档介绍了如何使用架构编辑器UI弃用XDM字段。 有关为自定义资源配置字段的更多信息，请参阅 [在API中定义XDM字段](./custom-fields-api.md). 有关管理描述符的更多信息，请参见 [描述符端点指南](../api/descriptors.md).
