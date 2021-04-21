---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；标识；字段；
solution: Experience Platform
title: 在UI中定义标识字段
description: 了解如何在Experience Platform用户界面中定义标识字段。
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 在UI中定义标识字段

在体验数据模型(XDM)中，标识字段表示一个字段，可用于标识与记录或时间序列事件相关的个人。 本文档介绍如何在Adobe Experience Platform UI中定义标识字段。

## 先决条件

身份字段是在平台中构建客户身份图的关键组件，它最终影响实时客户用户档案将不同数据片段合并到一起以获得客户的完整视图。 在模式中定义标识字段之前，请参阅以下文档，了解与标识字段相关的主要服务和概念：

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):跨设备和系统构建身份桥梁，根据符合的XDM模式定义的身份字段将数据集链接在一起。
   * [身份命名空间](../../../identity-service/namespaces.md):身份命名空间定义可与单个人相关的不同类型的身份信息，这些信息是每个身份字段的必需组件。
* [实时客户用户档案](../../../profile/home.md):利用客户身份图，根据来自多个来源的汇总数据提供统一的消费者用户档案，这些数据几乎实时更新。

## 定义标识字段

当[在UI中定义新字段](./overview.md#define)时，可以通过选中右边栏中的&#x200B;**[!UICONTROL Identity]**&#x200B;复选框将其设置为标识字段。

![](../../images/ui/fields/special/identity.png)

选中此复选框后会显示其他控件。 如果希望此字段是模式的主要标识，请选中&#x200B;**[!UICONTROL Primary identity]**&#x200B;复选框。

>[!NOTE]
>
>单个模式可能定义了多个标识字段，但只能有一个主标识。 所有标识字段（主要或其他）都会为单个客户的标识图贡献内容，但实时客户用户档案在合并数据碎片时仅使用主标识作为真相来源。 如果要启用模式以在用户档案中使用，则模式必须定义主标识。

在&#x200B;**[!UICONTROL Identity namespace]**&#x200B;下，使用下拉菜单为标识字段选择适当的命名空间。 将列出Adobe提供的标准命名空间以及您的组织定义的任何自定义命名空间。

完成后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将更改应用到模式。

![](../../images/ui/fields/special/identity-config.png)

画布更新以反映更改，所选字段获得指纹符号(![](../../images/ui/fields/special/identity-symbol.png))以将其指定为标识。 在左边栏中，标识字段现在以类或混合的名称列出，此类或混合将字段提供给模式。

由于默认情况下所有标识字段都是必填字段，因此该字段现在列在左边栏的&#x200B;**[!UICONTROL Required fields]**&#x200B;下。 如果标识字段嵌套在模式结构中，则所有父字段也将按要求列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您为模式定义了主标识，您现在可以继续[启用模式以在实时客户用户档案](../resources/schemas.md#profile)中使用。

## 后续步骤

本指南介绍如何在UI中定义标识字段。 使用此模式摄取数据时，您的客户身份图将更新以反映模式的身份字段。 请参阅[标识图查看器](../../../identity-service/ui/identity-graph-viewer.md)中的指南，了解如何在UI中浏览组织的专用图。

有关在UI](./overview.md#special)中定义字段的概述，请参阅[，以了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
