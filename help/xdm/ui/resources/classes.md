---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；类；类；
solution: Experience Platform
title: 在UI中创建和编辑类
description: 了解如何在Experience Platform用户界面中创建和编辑类。
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# 在UI中创建和编辑类

在体验数据模型(XDM)中，类定义模式将包含的数据的行为方面（记录或时间序列）。 除此之外，类还描述了所有基于该类的模式需要包含的公共属性的最小数量，并为合并多个兼容数据集提供了一种方法。

Adobe提供多个标准（“核心”）XDM类，包括[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织的更具体用例。

本文档概述了如何在Adobe Experience Platform UI中创建、编辑和管理自定义类。

## 先决条件

本指南要求对XDM系统有充分的了解。 有关Experience Platform生态系统中XDM角色的介绍，请参阅[XDM概述](../../home.md)，以及模式合成[基础知识](../../schema/composition.md)，了解类对XDM模式的贡献。

虽然本指南不是必需的，但建议您也要按照有关在UI](../../tutorials/create-schema-ui.md)中编写模式的教程来熟悉[!DNL Schema Editor]的各种功能。[

## 创建新类{#create}

在&#x200B;**[!UICONTROL Schemas]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL Create schema]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL Browse]**。

![](../../images/ui/resources/classes/browse-classes.png)

将显示一个对话框，允许您从可用类的列表中进行选择。 在对话框顶部，选择&#x200B;**[!UICONTROL Create new class]**。 然后，您可以为新类提供一个显示名称（类的简短、描述性、唯一且用户友好的名称）、说明以及模式将定义的数据的行为（&quot;[!UICONTROL Record]&quot;或&quot;[!UICONTROL Time-series]&quot;）。

完成后，选择&#x200B;**[!UICONTROL Assign class]**。

![](../../images/ui/resources/classes/class-details.png)

将显示[!DNL Schema Editor]，其中显示画布中基于刚刚创建的自定义类的新模式。 由于尚未向类添加任何字段，因此该模式只包含`_id`字段，该字段表示系统生成的唯一标识符，该标识符将自动应用于[!DNL Schema Registry]中的所有资源。

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>构建实现由您的组织定义的类的模式时，请记住，混合仅可与兼容类一起使用。 由于您定义的类是新类，因此&#x200B;**[!UICONTROL Add mixin]**&#x200B;对话框中没有列出兼容的混音。 相反，您需要[创建新的mixin](./mixins.md#create)以与该类一起使用。 下次您构建实现新类的模式时，您定义的混音将列出并可供使用。

您现在可以开始[向类](#add-fields)添加字段，该类将由使用该类的所有模式共享。

## 编辑现有类{#edit}

>[!NOTE]
>
>只能完全编辑和自定义您的组织定义的自定义类。 对于由Adobe定义的核心类，只能在单个模式的上下文中编辑其字段的显示名称。 有关详细信息，请参阅[编辑模式字段的显示名称部分](./schemas.md#display-names)。
>
>在保存自定义类并将其用于数据摄取后，之后只能对其进行附加更改。 有关详细信息，请参阅[模式演化规则](../../schema/composition.md#evolution)。

要编辑现有类，请选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，然后选择使用要编辑的类的模式的名称。

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找模式。 有关详细信息，请参阅[探索XDM资源](../explore.md)指南。

出现[!DNL Schema Editor]，画布中显示模式的结构。 您现在可以开始[向类](#add-fields)添加字段。

![](../../images/ui/resources/classes/edit.png)

## 将字段添加到类{#add-fields}

在[!UICONTROL Schema Editor]中打开使用自定义类的模式后，可以开始向该类添加字段。 要添加新字段，请选择模式名称旁的加号(+)**图标。**

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>请记住，您添加到某个类的任何字段都将用于使用该类的所有模式。 因此，您应仔细考虑哪些字段在所有模式用例中都会有用。 如果您考虑添加只能在此类下的某些模式中使用的字段，您可能希望考虑通过[创建混音](./mixins.md#create)将其添加到这些模式。

画布中会显示&#x200B;**[!UICONTROL New field]**，右边栏会更新，显示用于配置字段属性的控件。 有关如何配置字段并将其添加到类的具体步骤，请参阅[在UI](../fields/overview.md#define)中定义字段的指南。

继续向类添加所需数量的字段。 完成后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存模式和类。

![](../../images/ui/resources/classes/save.png)

如果您之前已创建使用此类的模式，则新添加的字段将自动显示在这些模式中。

## 更改模式{#schema}的类

在保存模式之前，您可以在初始创建过程中的任意点更改该类。 有关详细信息，请参阅[创建和编辑模式](./schemas.md#change-class)的指南。

## 后续步骤

本文档介绍了如何使用平台UI创建和编辑类。 有关[!UICONTROL Schemas]工作区功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](../overview.md)。

要了解如何使用[!DNL Schema Registry] API管理类，请参阅[类终结点指南](../../api/classes.md)。
