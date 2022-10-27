---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；枚举；字段；
solution: Experience Platform
title: 在UI中定义枚举字段和建议值
description: 了解如何在Experience Platform用户界面中为字符串字段定义枚举和建议值。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 89ada47cb6e0b204d8f2f19e7e9b6f31bf347964
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# 在UI中定义枚举和建议值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="枚举和建议值"
>abstract="安 **枚举** 限制字符串字段，以便仅允许摄取与预定义值集匹配的数据。 可为每个枚举约束分配一个 **显示名称** 用于填充分段UI中属性下拉列表。 **建议值** （对于字段）不会限制摄取，而是仅确定区段中显示的显示名称。 如果您有多个架构共享属于公共类或字段组的字段，并且您在每个架构之间为该字段定义不同的枚举或建议值，则这些值将合并并附加到并集架构中。"

在体验数据模型(XDM)中，可以为字符串字段提供一组预定义的已接受或建议值，以更好地控制将哪些值摄取到该字段或该字段在分段中的行为。

**[!UICONTROL 枚举]** 将可为字符串字段摄取的值限制为预定义集。 如果您尝试将数据摄取到枚举字段，并且该值与其配置中定义的任何数据不匹配，则将拒绝摄取。

与枚举相比， **[!UICONTROL 建议值]** 选项允许为字符串字段表示一组建议的值，这些值不会限制可摄取的值。 建议的值会影响 [分段UI](../../../segmentation/ui/overview.md) 将字符串字段作为属性包含在内时。

When [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，并将类型设置为 [!UICONTROL 字符串]，则您可以选择定义 [枚举](#enum) 或 [建议值](#suggested-values) 对于该字段。

![该图像显示了在UI中为字符串字段启用的枚举和建议值选项](../../images/ui/fields/enum/enum-options-selected.png)

本文档介绍如何在 [!UICONTROL 模式] UI工作区。 有关枚举和建议值（包括如何在UI中配置它们及其下游效果）的快速概述，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定义枚举 {#enum}

选择 **[!UICONTROL 枚举和建议值]**，然后选择 **[!UICONTROL 枚举]**. 此时会显示其他控件，允许您指定枚举的值约束。 要添加约束，请选择 **[!UICONTROL 添加行]**.

![显示在UI中选择的枚举选项的图像](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 列中，您必须提供要将字段限制为的确切值。 您可以选择提供人性化的 **[!UICONTROL 显示名称]** ，这会影响值在分段中的显示方式。

继续使用 **[!UICONTROL 添加行]** 要向枚举添加所需的约束和可选标签，或选择删除图标(![删除图标的图像](../../images/ui/fields/enum/remove-icon.png))以将其删除。 完成后，选择 **[!UICONTROL 应用]** 以将更改应用到架构。

![显示UI中字符串字段的枚举值和显示名称的图像](../../images/ui/fields/enum/enum-confirm.png)

画布会更新以反映所做的更改。 将来浏览此架构时，您可以在右边栏中查看和编辑枚举字段的约束。

## 定义建议的值 {#suggested-values}

选择 **[!UICONTROL 枚举和建议值]**，然后选择 **[!UICONTROL 建议值]** 以显示其他控件。 从此处选择 **[!UICONTROL 添加行]** 以开始添加建议的值。

![显示在UI中选择的建议值选项的图像](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 显示名称]** 列中，为您希望在分段UI中显示的值提供一个人类易记的名称。 要添加更多建议值，请选择 **[!UICONTROL 添加行]** 再次，并根据需要重复该过程。 要删除之前添加的行，请选择 ![删除图标](../../images/ui/fields/enum/remove-icon.png) 排旁边。

完成后，选择 **[!UICONTROL 应用]** 以将更改应用到架构。

![显示UI中字符串字段的枚举值和显示名称的图像](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>字段的更新建议值大约有五分钟的延迟，才能反映在分段UI中。

### 管理标准字段的建议值

标准XDM组件中的某些字段包含它们自己的建议值，例如 `eventType` 从 [[!UICONTROL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 虽然您可以为标准字段创建其他建议值，但您无法修改或删除组织未定义的任何建议值。 在UI中查看标准字段时，其建议值虽然显示但为只读值。

![显示UI中字符串字段的枚举值和显示名称的图像](../../images/ui/fields/enum/suggested-standard.png)

要为标准字段添加新的建议值，请选择 **[!UICONTROL 添加行]**. 要删除您的组织之前添加的建议值，请选择 ![删除图标](../../images/ui/fields/enum/remove-icon.png) 排旁边。

![显示UI中字符串字段的枚举值和显示名称的图像](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 枚举和建议值的演化规则 {#evolution}

在使用具有枚举字段的架构将数据摄取到平台后，对架构定义所做的任何进一步更改都必须符合系统中已有的数据。 通常，对现有字段所做的更改只能使该字段 **减少** 限制。 字段的限制不能比现有字段更严格。

对于枚举和建议的值，以下规则会应用摄取后的规则：

* 您 **可以** 使用现有建议值为标准和自定义字段添加建议值。
* 您 **可以** 从具有现有建议值的自定义字段中删除建议值。
* 您 **可以** 为现有自定义枚举字段添加新的枚举值。
* 您 **可以** 将自定义字段的枚举值切换为仅建议的值，或将其转换为没有枚举或建议值的字符串。 **应用后，此开关将无法撤消。**
* 您 **不能** 从标准字段中删除枚举或建议值。
* 您 **不能** 将枚举值添加到没有现有枚举的字段。
* 您 **不能** 删除自定义字段的枚举值少于所有现有枚举值。
* 您 **不能** 从建议的值切换到枚举。

## 合并枚举和建议值的规则 {#merging}

如果多个架构使用具有不同配置的相同枚举字段，并且这些架构包含在并集中，则当涉及如何协调枚举差异时，某些规则将会应用。 具体规则取决于引用相同标准字段的架构(如 `eventType`)，或者他们引用不同字段组中的相同自定义字段路径。

如果引用相同的标准字段：

* 任何其他建议的值包括 **已附加** 在工会中。
* 对同一枚举键值的建议值进行了更新，包括 **已更新** 在工会中。

如果在不同的字段组中引用相同的自定义字段路径：

* 任何其他建议的值包括 **已附加** 在工会中。
* 如果在多个架构中定义了相同的其他建议值，则这些值为 **合并** 在工会中。 换言之，相同的建议值在合并后不会显示两次。

## 验证限制

由于当前系统限制，在摄取期间系统未验证枚举的情况有两种：

1. 枚举是在 [阵列字段](./array.md).
1. 枚举在架构层次结构中定义了多个级别。

## 后续步骤

本指南介绍了如何在UI中为字符串字段定义枚举和建议值。 有关如何使用架构注册表API管理枚举和建议值的信息，请参阅以下内容 [教程](../../tutorials/suggested-values.md).

了解如何在 [!DNL Schema Editor]，请参阅 [在UI中定义字段](./overview.md#special).
