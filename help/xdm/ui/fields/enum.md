---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；ui；工作区；枚举；字段；
solution: Experience Platform
title: 在UI中定义枚举字段
description: 了解如何在Experience Platform用户界面中定义枚举字段。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 在UI中定义枚举字段

在体验列表模型(XDM)中，枚举字段表示一个字段，该字段被限制为可接受值的预定义数据。

当[在Adobe Experience Platform用户界面中定义新字段](./overview.md#define)时，您可以通过选中右边栏中的&#x200B;**[!UICONTROL Enum]**&#x200B;复选框将其设置为枚举字段。

![](../../images/ui/fields/special/enum.png)

选中此复选框后会显示其他控件，允许您指定枚举的值约束。 在&#x200B;**[!UICONTROL Value]**&#x200B;列下，必须提供要将字段限制为的确切值。 此值必须符合您为枚举字段选择的[!UICONTROL Type]。 您也可以选择为约束提供人性化的&#x200B;**[!UICONTROL Label]**。

要向枚举添加其他约束，请选择&#x200B;**[!UICONTROL Add row]**。

![](../../images/ui/fields/special/enum-add-row.png)

继续向枚举添加所需的约束和可选标签。 完成后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将更改应用到模式。

![](../../images/ui/fields/special/enum-configured.png)

画布会更新以反映更改。 将来浏览此模式时，您可以视图和编辑右边栏中枚举字段的约束。

![](../../images/ui/fields/special/enum-applied.png)

## 后续步骤

本指南介绍如何在UI中定义枚举字段。 有关在UI](./overview.md#special)中定义字段的概述，请参阅[，以了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
