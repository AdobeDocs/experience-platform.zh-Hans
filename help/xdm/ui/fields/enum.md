---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；枚举；字段；
solution: Experience Platform
title: 在UI中定义枚举字段和建议值
description: 了解如何在Experience Platform用户界面中为字符串字段定义枚举和建议值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 8%

---

# 在UI中定义枚举和建议值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="枚举和建议值"
>abstract="**枚举**&#x200B;将字符串字段限制为仅允许提取与一组预定义值匹配的数据。可以为每个枚举限制分配一个&#x200B;**显示名称**，用于填充分段 UI 中的属性下拉列表。字段的&#x200B;**建议值**&#x200B;不限制提取，并且仅确定分段中显示的显示名称。如果您的多个架构共享一个属于公共类或字段组的字段，并且您在各个架构之间为该字段定义了不同的枚举或建议值，则这些值将合并和附加到联合架构中。"

在Experience Data Model (XDM)中，可以为字符串字段提供一组预定义的接受或建议值，以便更好地控制哪些值被引入到该字段中，或者如何在分段中表现。

**[!UICONTROL 枚举]** 将可为字符串字段摄取的值约束为预定义集。 如果您尝试将数据摄取到枚举字段，但值与其配置中定义的任何值都不匹配，则将拒绝摄取。

与枚举相反， **[!UICONTROL 建议值]** 选项允许为字符串字段表示一组推荐值，这些值不会限制它可以摄取的值。 相反，建议值会影响中提供的预定义值 [分段UI](../../../segmentation/ui/overview.md) 将字符串字段作为属性包含时。

时间 [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，并将类型设置为 [!UICONTROL 字符串]，您可以选择定义 [枚举](#enum) 或 [建议值](#suggested-values) 用于该字段。

![显示为UI中的字符串字段启用的“枚举和建议值”选项的图像](../../images/ui/fields/enum/enum-options-selected.png)

本文档介绍如何在中定义枚举和建议值 [!UICONTROL 架构] 用户界面工作区。 要快速了解枚举和建议值（包括如何在UI中配置它们及其下游影响），请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定义枚举 {#enum}

选择 **[!UICONTROL 枚举和建议值]**，然后选择 **[!UICONTROL 枚举]**. 将显示其他控件，允许您为枚举指定值约束。 要添加约束，请选择 **[!UICONTROL 添加行]**.

![显示在UI中选择的枚举选项的图像](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 列中，必须提供要将字段约束到的确切值。 您可以选择提供人性化的 **[!UICONTROL 显示名称]** 约束，这也会影响分段中值的表示方式。

继续使用 **[!UICONTROL 添加行]** 将所需的约束和可选标签添加到枚举，或选择删除图标(![删除图标的图像](../../images/ui/fields/enum/remove-icon.png))以将其删除。 完成后，选择 **[!UICONTROL 应用]** 将更改应用到架构。

![该图像显示UI中字符串字段填写的枚举值和显示名称](../../images/ui/fields/enum/enum-confirm.png)

画布将更新以反映这些更改。 当您以后探索此架构时，可以查看和编辑右边栏中枚举字段的约束。

## 定义建议值 {#suggested-values}

选择 **[!UICONTROL 枚举和建议值]**，然后选择 **[!UICONTROL 建议值]** 以显示其他控件。 从此处选择 **[!UICONTROL 添加行]** 以开始添加建议值。

![显示在UI中选择的“建议值”选项的图像](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 显示名称]** 列中，为您希望在分段UI中显示的值提供人类友好的名称。 要添加更多建议值，请选择 **[!UICONTROL 添加行]** 再次尝试，并根据需要重复该过程。 要删除以前添加的行，请选择 ![删除图标](../../images/ui/fields/enum/remove-icon.png) 相关行的旁边。

完成后，选择 **[!UICONTROL 应用]** 将更改应用到架构。

![该图像显示UI中字符串字段填写的枚举值和显示名称](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>字段的更新建议值大约有五分钟的延迟才能反映在分段UI中。

### 管理标准字段的建议值

标准XDM组件中的某些字段包含自己的建议值，例如 `eventType` 从 [[!UICONTROL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 虽然可以为标准字段创建其他建议值，但无法修改或删除任何未由组织定义的建议值。 在UI中查看标准字段时，其建议值会显示，但为只读。

![该图像显示UI中字符串字段填写的枚举值和显示名称](../../images/ui/fields/enum/suggested-standard.png)

要为标准字段添加新的建议值，请选择 **[!UICONTROL 添加行]**. 要删除贵组织之前添加的建议值，请选择 ![删除图标](../../images/ui/fields/enum/remove-icon.png) 相关行的旁边。

![该图像显示UI中字符串字段填写的枚举值和显示名称](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 枚举和建议值的演化规则 {#evolution}

使用具有枚举字段的架构将数据摄取到Platform后，对架构定义所做的任何进一步更改都必须符合系统中已存在的数据。 通常，对现有字段进行的更改只能使该字段成为必填字段 **更少** 限制性。 不能使字段的限制比它已有的更严格。

对于枚举和建议值，以下规则适用于摄取后：

* 您 **可以** 为具有现有建议值的标准和自定义字段添加建议值。
* 您 **可以** 从具有现有建议值的自定义字段中移除建议值。
* 您 **可以** 为现有的自定义枚举字段添加新的枚举值。
* 您 **可以** 将自定义字段的枚举值仅切换为建议值，或将其转换为没有枚举或建议值的字符串。 **此开关一经应用便无法撤消。**
* 您 **无法** 从标准字段中移除枚举或建议值。
* 您 **无法** 向没有现有枚举的字段添加枚举值。
* 您 **无法** 删除自定义字段少于所有现有枚举值。
* 您 **无法** 从建议值切换到枚举。

## 枚举和建议值的合并规则 {#merging}

如果多个架构使用具有不同配置的同一枚举字段，并且这些架构包含在合并中，则在如何协调枚举差异时将会应用某些规则。 确切的规则取决于引用同一标准字段的架构(如 `eventType`)，或者如果它们在不同字段组中引用相同的自定义字段路径。

如果引用同一标准字段：

* 任何其他建议值包括 **已附加** 在联盟里。
* 对同一枚举键的建议值进行的更新如下 **已更新** 在联盟里。

如果在不同字段组中引用相同的自定义字段路径：

* 任何其他建议值包括 **已附加** 在联盟里。
* 如果在多个架构中定义了相同的附加建议值，则这些值为 **已合并** 在联盟里。 换句话说，相同的建议值在合并后不会显示两次。

## 验证限制

由于当前系统的限制，在两种情况下，系统会在引入期间不验证枚举：

1. 枚举定义在 [数组字段](./array.md).
1. 枚举在架构层次结构中的多个级别上定义。

## 后续步骤

本指南介绍了如何在UI中定义字符串字段的枚举和建议值。 有关如何使用架构注册表API管理枚举和建议值的信息，请参阅以下内容 [教程](../../tutorials/suggested-values.md).

了解如何在中定义其他XDM字段类型 [!DNL Schema Editor]，请参阅 [在UI中定义字段](./overview.md#special).
