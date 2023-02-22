---
title: 弃用UI中的XDM字段
description: 了解如何使用Experience Platform中的架构编辑器来弃用Experience Data Model(XDM)字段。
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 弃用UI中的XDM字段

Experience Data Model(XDM)在摄取数据后弃用架构字段，让您能够灵活地管理数据模型，以便在业务需求发生更改时对其进行管理。 可以弃用不需要的字段，以便从UI视图中删除它们，并从下游UI中隐藏它们。 通过模式编辑器中的复选框，您可以方便地显示已弃用的字段，并且如有必要，您还可以对它们进行定义。

由于已弃用的字段默认在UI中隐藏，因此它可简化架构编辑器中的架构，并阻止将不需要的字段添加到下游依赖项，如区段生成器、历程设计器等。 字段弃用也可向后兼容。 使用已弃用字段（如区段和查询）的其他系统将继续按预期评估这些字段。 如果现有区段中使用了已弃用字段，则会正常处理该字段，这意味着该字段会在区段生成器画布中按预期显示，或根据已弃用字段中提供的任何数据进行评估。 这是一项不间断的更改，不会对任何现有的数据流造成负面影响。

>[!NOTE]
>
>在将数据摄取到架构中之前，您可以删除不必要的字段组。 请参阅 [如何从架构中删除字段组](../ui/resources/schemas.md#remove-fields) 以了解更多信息。

将数据摄取到架构后，您将无法再从架构中删除字段，而无需进行中断更改。 在这种情况下，您可以使用 [架构编辑器](./create-schema-ui.md) 或 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

本文档介绍如何使用Experience Platform用户界面中的架构编辑器来弃用不同XDM资源的字段。 有关使用API弃用XDM字段的步骤，请参阅 [使用架构注册表API弃用XDM字段](./field-deprecation-api.md).

## 弃用字段 {#deprecate}

要弃用自定义字段，请导航到要编辑的架构的架构编辑器。 选择要从 [!UICONTROL 结构] 画布的部分，然后 **[!UICONTROL 弃用]** 从 [!UICONTROL 字段属性].

![选中并弃用字段的架构编辑器已突出显示。](../images/tutorials/field-deprecation/deprecate-single-field.png)

此时会出现一个对话框，确认您所做的选择，并通知您该字段将从并集架构的UI视图中删除，并从下游UI中隐藏。 要完成操作，请选择 **[!UICONTROL 确认]**.

![“弃用”字段对话框中，“确认”突出显示。](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

字段现已从UI视图中删除。

>[!NOTE]
>
>弃用后，下游UI(如分段功能板、Customer Journey Analytics和Adobe Journey Optimizer)不再将已弃用的字段显示为其工作流的一部分。 但是，下游UI可以根据需要选择显示已弃用的字段，并继续将已弃用的字段视为正常字段。 有关更多信息，请参阅各自的文档。 使用已弃用字段的查询和区段将继续按预期运行。

## 显示已弃用的字段 {#show-deprecated}

要查看以前已弃用的字段，请在架构编辑器中导航到相关架构。 选择 **[!UICONTROL 显示已弃用的字段]** 复选框 [!UICONTROL 组合物] 部分。

现在，已弃用的字段会显示在UI视图中。 选择 **[!UICONTROL 保存]** 以确认您的设置。

![选择了字段、显示已弃用的字段并突出显示保存的架构编辑器。](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## 不足字段 {#undeprecate-fields}

要撤消已弃用的字段，请首先 [显示已弃用字段](#show-deprecated) 如上所述，从编辑器的 [!UICONTROL 结构] 中。 接下来，选择 **[!UICONTROL 不精确]** 从 [!UICONTROL 字段属性] 侧栏后跟 **[!UICONTROL 保存]**.

![突出显示了已弃用字段、未弃用和保存的架构编辑器。](../images/tutorials/field-deprecation/undeprecate-single-field.png)

的 [!UICONTROL 不精确字段] 对话框。 要确认更改，请选择 **[!UICONTROL 确认]**.

![的 [!UICONTROL 不精确字段] 对话框。](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

字段现在在UI视图和下游UI中显示为标准。 您现在可以再次选择弃用该字段。

## 后续步骤

本文档介绍了如何使用架构编辑器UI弃用XDM字段。 有关为自定义资源配置字段的更多信息，请参阅 [在API中定义XDM字段](./custom-fields-api.md). 有关管理描述符的更多信息，请参阅 [描述符终结点指南](../api/descriptors.md).
