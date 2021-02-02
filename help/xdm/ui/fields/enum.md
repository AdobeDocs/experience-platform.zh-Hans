---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；枚举；字段；
solution: Experience Platform
title: 在UI中定义枚举字段
description: 了解如何在Experience Platform用户界面中定义枚举字段。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 在UI中定义枚举字段

在体验数据模型(XDM)中，枚举字段表示一个字段，该字段被限制为可接受值的预定义列表。

当[在Adobe Experience Platform用户界面中定义新字段](./overview.md#define)时，您可以通过选中右边栏中的&#x200B;**[!UICONTROL Enum]**&#x200B;复选框将其设置为枚举字段。

![](../../images/ui/fields/special/enum.png)

选中该复选框后将显示其他控件，允许您指定枚举的值约束。 在&#x200B;**[!UICONTROL Value]**&#x200B;列下，必须提供要将字段限制为的精确值。 此值必须与您为枚举字段选择的[!UICONTROL 类型]相符。 您也可以选择为约束提供人性化的&#x200B;**[!UICONTROL 标签]**。

要向枚举添加其他约束，请选择&#x200B;**[!UICONTROL 添加行]**。

![](../../images/ui/fields/special/enum-add-row.png)

继续向枚举添加所需的约束和可选标签。 完成后，选择&#x200B;**[!UICONTROL 应用]**&#x200B;将更改应用于模式。

![](../../images/ui/fields/special/enum-configured.png)

画布会更新以反映更改。 将来浏览此模式时，您可以视图并编辑右边栏中枚举字段的约束。

![](../../images/ui/fields/special/enum-applied.png)

## 后续步骤

本指南介绍如何在UI中定义枚举字段。 请参见[定义UI](./overview.md#special)中的字段的概述，了解如何定义[!DNL Schema Editor]中的其他XDM字段类型。