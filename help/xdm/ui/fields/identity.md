---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；身份；字段；
solution: Experience Platform
title: 在UI中定义标识字段
description: 了解如何在Experience Platform用户界面中定义标识字段。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 在UI中定义标识字段

在体验数据模型(XDM)中，标识字段表示一个字段，用于标识与记录或时间系列事件相关的个人人员。 本文档介绍如何在Adobe Experience Platform UI中定义标识字段。

## 先决条件

身份字段是在Platform中构建客户身份图形的关键组件，这最终会影响实时客户资料如何将不同的数据片段合并在一起，以获得客户的完整视图。 在架构中定义标识字段之前，请参阅以下文档，了解有关标识字段相关的关键服务和概念的信息：

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):跨设备和系统构建身份桥梁，根据数据集符合的XDM架构定义的身份字段，将数据集链接在一起。
   * [身份命名空间](../../../identity-service/namespaces.md):身份命名空间定义可与单个人员关联的不同身份信息类型，这些信息是每个身份字段的必需组件。
* [实时客户资料](../../../profile/home.md):利用客户身份图以基于来自多个来源的汇总数据提供统一的客户配置文件，这些数据近乎实时地更新。

## 定义标识字段

When [定义新字段](./overview.md#define) 在UI中，您可以通过选择 **[!UICONTROL 身份]** 复选框。

![](../../images/ui/fields/special/identity.png)

选中此复选框后，将显示其他控件。 如果希望此字段作为架构的主标识，请选择 **[!UICONTROL 主标识]** 复选框。

>[!NOTE]
>
>单个架构可能定义了多个标识字段，但只能具有一个主标识。 所有身份字段（主标识或其他标识字段）都会为单个客户的身份图贡献内容，但实时客户配置文件在将数据片段合并到一起时，只使用主标识作为真实来源。 如果要启用架构以在配置文件中使用，则架构必须定义主标识。

在 **[!UICONTROL 身份命名空间]**，请使用下拉菜单为标识字段选择相应的命名空间。 将列出Adobe提供的标准命名空间，以及您的组织定义的任何自定义命名空间。

完成后，选择 **[!UICONTROL 应用]** 将更改应用到架构。

![](../../images/ui/fields/special/identity-config.png)

画布会更新以反映所做更改，所选字段会获得指纹符号(![](../../images/ui/fields/special/identity-symbol.png))将其指定为标识。 在左边栏中，标识字段现在列在为架构提供字段的类或架构字段组的名称下。

如果字段也设置为主标识，则也会列在 **[!UICONTROL 必填字段]** 中。 如果标识字段嵌套在架构结构中，则所有父字段也将按需要列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您为架构定义了主标识，则现在可以继续 [启用架构以在实时客户资料中使用](../resources/schemas.md#profile).

## 后续步骤

本指南介绍了如何在UI中定义身份字段。 使用此架构摄取数据时，您的客户身份图将进行更新，以反映架构的身份字段。 请参阅 [身份图查看器](../../../identity-service/ui/identity-graph-viewer.md) 了解如何在UI中浏览贵组织的专用图。

请参阅 [在UI中定义字段](./overview.md#special) 了解如何在 [!DNL Schema Editor].
