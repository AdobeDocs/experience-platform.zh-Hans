---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；数组；字段；
solution: Experience Platform
title: 在UI中定义数组字段
description: 了解如何在Experience Platform用户界面中定义数组字段。
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# 在UI中定义数组字段

在Adobe Experience Platform用户界面中定义体验数据模型(XDM)字段时，可以将该字段指定为数组。

数组的内容取决于 [!UICONTROL 类型] 已选择。 例如，如果字段的 [!UICONTROL 类型] 设置为&quot;[!UICONTROL 字符串]&quot;，将该字段设置为数组会将该字段指定为字符串数组。 如果字段的 [!UICONTROL 类型] 设置为多字段数据类型，如“[!UICONTROL 邮政地址]“，则它将成为符合数据类型的邮政地址对象数组。

在 [在用户界面中定义了新字段](./overview.md#define)，您可以通过选择 **[!UICONTROL 数组]** 复选框。

![](../../images/ui/fields/special/array.png)

选中此复选框后，右边栏中会显示其他控件，允许您选择进一步约束数组。 如果您不希望强制实施特定约束，请将字段留空。

阵列的其他配置控件如下所示：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL 最小长度] | 要使摄取成功，数组必须包含的最小项目数。 |
| [!UICONTROL 最大长度] | 要使摄取成功，数组必须包含的最大项目数。 |
| [!UICONTROL 仅独特项目] | 如果设置为“[!UICONTROL True]“，为了使摄取成功，数组中的每个项目必须是唯一的。 |

{style=&quot;table-layout:auto&quot;}

配置完字段后，选择 **[!UICONTROL 应用]** 将更改应用到架构。

![](../../images/ui/fields/special/array-config.png)

画布会更新以反映对字段所做的更改。 请注意，画布中字段名称旁边显示的数据类型将附加一对方括号(`[]`)，指示字段表示该数据类型的数组。

![](../../images/ui/fields/special/array-applied.png)

## 后续步骤

本指南介绍了如何在UI中定义数组字段。 请参阅 [在UI中定义字段](./overview.md#special) 了解如何在 [!DNL Schema Editor].
