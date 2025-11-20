---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；身份；字段；
solution: Experience Platform
title: 在UI中定义标识字段
description: 了解如何在Experience Platform用户界面中定义标识字段。
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 3570197ca6cff95368b4facb034386e793033fe2
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 6%

---

# 在UI中定义标识字段

在Experience Data Model (XDM)中，身份字段表示可用于识别与记录或时间序列事件相关的个人人员的字段。 本文档介绍如何在Adobe Experience Platform UI中定义标识字段。

## 先决条件

标识字段是如何在Experience Platform中构建客户标识图的关键组件，它最终影响Real-time Customer Profile如何将不同的数据片段合并到一起，从而获得客户的完整视图。 在架构中定义身份字段之前，请参阅以下文档以了解与身份字段相关的关键服务和概念：

* [Adobe Experience Platform Identity服务](../../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集所遵循的XDM架构定义的身份字段将数据集链接在一起。
   * [身份命名空间](../../../identity-service/features/namespaces.md)：身份命名空间定义可以与单个人员相关的不同类型的身份信息，并且是每个身份字段的必需组件。
* [实时客户个人资料](../../../profile/home.md)：利用客户身份图根据来自多个来源的汇总数据提供近乎实时更新的统一客户个人资料。

## 定义身份标识字段 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="对主要身份标识的限制"
>abstract="此架构使用旨在用于特定源连接的字段组。该连接要求将 identityMap 用作主要标识并已自动设置。"

在UI中定义[新字段](./overview.md#define)时，您可以通过选中右边栏中的&#x200B;**[!UICONTROL Identity]**&#x200B;复选框将其设置为标识字段。

![](../../images/ui/fields/special/identity.png)

选中此复选框后，将显示其他控件。 如果您希望此字段作为架构的主标识，请选中&#x200B;**[!UICONTROL Primary identity]**&#x200B;复选框。

>[!NOTE]
>
>单个架构可以定义多个标识字段，但只能有一个主标识。 所有身份字段（主要或其他类型）都有助于单个客户的身份图，但在合并数据片段时，实时客户配置文件仅使用主要身份作为真实来源。 如果要启用架构以便在Profile中使用，则架构必须定义主标识。

在&#x200B;**[!UICONTROL Identity namespace]**&#x200B;下，使用下拉菜单为标识字段选择适当的命名空间。 列出了Adobe提供的标准命名空间以及您的组织定义的任何自定义命名空间。

完成后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以将更改应用于架构。

>[!IMPORTANT]
>
>一旦启用了架构以便在Real-time Customer Profile中使用并且数据已被摄取，**您就无法更改主标识字段**。 尝试这样做将导致验证错误。 如果您需要使用其他主身份，则必须使用更新的身份配置创建新架构和新数据集。

![](../../images/ui/fields/special/identity-config.png)

画布将更新以反映这些更改，所选字段将获得指纹符号(![](/help/images/icons/identity-service.png))以将其指定为标识。 在左边栏中，标识字段现在列在为架构提供字段的类或架构字段组的名称下。

如果该字段也设置为主标识，则它也会在左边栏中列在&#x200B;**[!UICONTROL Required fields]**&#x200B;下。 如果标识字段嵌套在架构结构中，则所有父字段也将按要求列出。

![](../../images/ui/fields/special/identity-applied.png)

如果您为架构定义了主标识，则现在可以继续[启用架构以在实时客户个人资料中使用](../resources/schemas.md#profile)。

## 后续步骤

本指南介绍了如何在UI中定义标识字段。 使用此架构摄取数据时，您的客户身份图将进行更新以反映架构的身份字段。 请参阅[身份图形查看器](../../../identity-service/features/identity-graph-viewer.md)上的指南，了解如何在UI中浏览组织的专用图形。

请参阅[在UI](./overview.md#special)中定义字段的概述，了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
