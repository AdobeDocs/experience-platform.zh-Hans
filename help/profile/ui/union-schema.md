---
keywords: Experience Platform;用户档案；实时客户用户档案；统一用户档案；统一用户档案；统一用户档案;模式;rtcp；启用用户档案；启用用户档案;合并合并;用户档案合并;用户档案;
title: 合并 模式 UI指南
topic-legacy: guide
type: Documentation
description: 在Adobe Experience Platform用户界面(UI)中，您可以轻松地视图组织内的任何合并模式，并预览特定类的字段、身份、关系和贡献模式。 本指南提供有关如何使用平台UI视图和浏览合并模式的详细信息。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# [!UICONTROL Union schema] UI指南

在Adobe Experience Platform用户界面(UI)中，您可以轻松地视图组织内的任何合并模式，并预览特定类的字段、身份、关系和贡献模式。 本指南提供有关如何使用平台UI视图和浏览合并模式的详细信息。

## 入门指南

本UI指南要求了解与管理实时客户用户档案数据相关的各种[!DNL Experience Platform]服务。 在阅读本指南或在UI中工作之前，请查阅以下服务的文档：

* [[!DNL Real-time Customer Profile]](../home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [[!DNL Identity Service]](../../identity-service/home.md):当不同 [!DNL Real-time Customer Profile] 的数据源被引入其中时，通过连接它们的身份来实现这一 [!DNL Platform]点。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

## 了解合并模式

实时客户用户档案使您能够创建强大、集中的用户档案，这些事件包含客户属性和跨与Adobe Experience Platform集成的系统的每次客户交互的有时间戳的。 此数据的格式和结构由体验数据模型(XDM)模式提供，每个模式基于XDM类并包含与该类兼容的字段。

可以为多个用例创建模式，引用相同的类，但包含特定于其使用的字段。 启用模式进行用户档案后，它将成为合并模式的一部分。 换句话说，合并模式由多个模式组成，这些共享同一类并已启用用户档案。 合并模式使您能够看到共享同一类的模式中包含的所有字段的合并。 实时客户用户档案使用合并模式为每位客户创建整体视图。

使用合并模式需要深入了解XDM模式。 有关详细信息，请首先阅读模式合成[基础知识](../../xdm/schema/composition.md)。

## 视图合并模式

要导航到平台UI中的合并模式，请从左侧导航中选择&#x200B;**[!UICONTROL Profiles]**，然后选择&#x200B;**[!UICONTROL Union Schema]**&#x200B;选项卡。 将打开[!UICONTROL Union Schema]选项卡，显示当前选定类的合并模式。

![](../images/union-schema/union-schema-landing.png)

## 选择类

要显示特定XDM类的合并模式，请从&#x200B;**[!UICONTROL Class]**&#x200B;下拉列表中选择该类。 由于并非所有类都具有合并模式，因此下拉列表中只有具有合并模式的类(即具有已启用用户档案的模式的类)可用。

选择某个类后，显示的模式会更新，以反映选定类的合并模式。 例如，您可以选择&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;来视图该类的合并模式。

![](../images/union-schema/union-schema-class.png)

## 浏览合并模式

您可以浏览合并模式，方法是上下滚动以视图整个模式结构，并选择右尖括号(`>`)展开嵌套字段。

![](../images/union-schema/union-schema-explore.png)

选择任意字段以视图其详细信息，包括显示名称、数据类型、说明、路径、创建日期和上次修改日期。 您还可以视图包含所选字段的贡献模式的列表。

![](../images/union-schema/union-schema-explore-field.png)

选择贡献模式的名称将显示与该模式相关的数据集的名称，这些数据集将数据引入所选字段。 每个数据集名称都显示为一个链接。 选择活动集名称后，该数据集将在新窗口中打开“数据集”选项卡。

有关数据集的更多信息(包括查看数据集活动和在UI中预览数据集数据)，请访问[数据集UI指南](../../catalog/datasets/user-guide.md)。

![](../images/union-schema/union-schema-field-datasets.png)

## 视图贡献模式

您还可以通过选择&#x200B;**[!UICONTROL All contributing schemas]**&#x200B;展开合并的列表,视图哪些特定模式对模式模式有贡献。 根据您选择的类和您的组织在平台中创建的模式数，这可以是包含单个模式的短列表或包含多个模式的长列表。

![](../images/union-schema/union-schema-contributing-schemas.png)

选择特定模式的名称会突出显示合并模式中属于您选择的模式的字段。 选择模式后，合并模式将灰显，并显示黑条，指示作用模式的一部分的字段。

![](../images/union-schema/union-schema-select-schema.png)

## 视图身份

通过UI，您可以视图合并模式中包含的身份列表，方法是选择&#x200B;**[!UICONTROL Identities]**&#x200B;展开列表。

![](../images/union-schema/union-schema-identities.png)

从列表中选择单个标识会导致显示的模式根据需要自动更新以显示标识字段。 如果标识字段嵌套在一起，这可能包括扩展多个字段。

标识字段在合并模式中高亮显示，并且标识的详细信息显示在屏幕的右侧。 详细信息包括包含标识字段的贡献模式的列表，您可以向下钻取以查找到与该模式相关的数据集的链接，这些数据集将数据引入所选标识字段。

![](../images/union-schema/union-schema-select-identity.png)

## 视图关系

合并 模式 UI还允许您查看已根据所选模式类为模式定义的关系。 定义关系是一种将属于不同类的两个模式连接起来的方式，以便获得对客户数据的更复杂的洞察。

如果已为所选类建立关系，则选择&#x200B;**[!UICONTROL Relationships]**&#x200B;将显示用于创建关系的字段列表。 并非所有模式都使用或需要定义关系，因此关系部分不包含任何字段是常见的。

要进一步了解模式关系，包括如何使用UI定义模式关系，请访问[此关系文档](../../xdm/tutorials/relationship-ui.md)。

![](../images/union-schema/union-schema-relationships.png)

从列表中选择关系字段会导致显示的模式根据需要更新以显示高亮显示的关系字段。 如果关系字段嵌套在一起，这可能包括扩展多个字段。

![](../images/union-schema/union-schema-select-relationship.png)

## 后续步骤

通过阅读本指南，您现在了解如何使用[!DNL Experience Platform] UI视图和导航合并模式。 有关模式的更多信息（包括如何在整个平台中使用它们），请首先阅读[XDM系统概述](../../xdm/home.md)。
