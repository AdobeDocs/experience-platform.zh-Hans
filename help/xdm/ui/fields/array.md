---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；数组；字段；
solution: Experience Platform
title: 在UI中定义数组字段
description: 了解如何在Experience Platform用户界面中定义数组字段。
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 在UI中定义数组字段

在Adobe Experience Platform用户界面中定义体验数据模型(XDM)字段时，可以将该字段指定为数组。

数组的内容取决于为该字段选择的[!UICONTROL Type]。 例如，如果字段的[!UICONTROL Type]设置为“[!UICONTROL String]”，则将该字段设置为数组会将该字段指定为字符串数组。 如果字段的[!UICONTROL Type]设置为多字段数据类型，如“[!UICONTROL Postal address]”，则该字段将成为符合数据类型的邮政地址对象的数组。

在UI](./overview.md#define)中定义了[新字段后，可以通过选中右边栏中的&#x200B;**[!UICONTROL Array]**&#x200B;复选框将其设置为数组字段。

![](../../images/ui/fields/special/array.png)

选中此复选框后，右侧边栏中会显示其他控件，允许您选择进一步限制数组。 如果您不希望强制实施特定约束，请将该字段留空。

阵列的其他配置控件如下：

| 字段属性 | 描述 |
| --- | --- |
| [!UICONTROL Minimum length] | 数组必须包含的最小项数，才能成功摄取。 |
| [!UICONTROL Maximum length] | 数组必须包含的最大项数，才能成功摄取。 |
| [!UICONTROL Unique items only] | 如果设置为“[!UICONTROL True]”，则数组中的每个项目必须是唯一的，才能成功获取。 |

完成字段配置后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将更改应用于模式。

![](../../images/ui/fields/special/array-config.png)

画布会更新，以反映对字段所做的更改。 请注意，画布中字段名称旁边显示的数据类型会附加一对方括号(`[]`)，表示该字段表示该数据类型的数组。

![](../../images/ui/fields/special/array-applied.png)

## 后续步骤

本指南介绍如何在UI中定义数组字段。 有关在UI](./overview.md#special)中定义字段的概述，请参阅[，以了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
