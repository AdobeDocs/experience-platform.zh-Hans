---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；数组；字段；
solution: Experience Platform
title: 在UI中定义数组字段
description: 了解如何在Experience Platform用户界面中定义数组字段。
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# 在UI中定义数组字段

在Adobe Experience Platform用户界面中定义体验数据模型(XDM)字段时，您可以将该字段指定为数组。

阵列的内容取决于 [!UICONTROL 类型] 已为该字段选择。 例如，如果字段的 [!UICONTROL 类型] 设置为&quot;[!UICONTROL 字符串]“”，将该字段设置为数组会将字段指定为字符串数组。 如果字段的 [!UICONTROL 类型] 设置为多字段数据类型，例如&quot;[!UICONTROL 邮政地址]“”，则它将成为符合数据类型的邮政地址对象数组。

在您拥有 [在UI中定义了新字段](./overview.md#define)，则可以通过选择 **[!UICONTROL 数组]** 复选框。

![](../../images/ui/fields/special/array.png)

选中此复选框后，右边栏中会显示其他控件，以便您可以选择进一步限制数组。 如果不希望强制实施特定约束，请将该字段留空。

阵列的其他配置控制如下所示：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 最小长度] | 为了成功引入，数组必须包含的最小项数。 |
| [!UICONTROL 最大长度] | 为了成功引入，数组必须包含的最大项数。 |
| [!UICONTROL 仅限唯一项目] | 如果设置为&quot;[!UICONTROL True]“，数组中的每个项目都必须是唯一的，才能成功引入。 |

{style="table-layout:auto"}

配置完字段后，选择 **[!UICONTROL 应用]** 将更改应用于架构。

![](../../images/ui/fields/special/array-config.png)

画布将进行更新以反映对该字段所做的更改。 请注意，在画布中的字段名称旁边显示的数据类型附加了一对方括号(`[]`)，指示字段表示该数据类型的数组。

![](../../images/ui/fields/special/array-applied.png)

## 后续步骤

本指南介绍了如何在UI中定义数组字段。 有关更多详细信息，请参阅 [在UI中定义字段](./overview.md#special) 了解如何在中定义其他XDM字段类型 [!DNL Schema Editor].
