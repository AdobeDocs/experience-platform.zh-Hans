---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；混合；混合；
solution: Experience Platform
title: 在UI中创建和编辑混音
description: 了解如何在Experience Platform用户界面中创建和编辑混音。
topic: user guide
translation-type: tm+mt
source-git-commit: cf74c7922271035474c7f10534692983add48616
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# 在UI中创建和编辑混音

在体验数据模型(XDM)中，混合是可重用的组件，它们定义一个或多个字段，实现某些功能，如个人详细信息、酒店偏好或地址。 混合被设计为实现兼容类的模式的一部分。

混音根据混音所表示数据的行为（记录或时间序列）定义它与哪些类兼容。 这意味着并非所有混音都可用于所有类。

Adobe Experience Platform提供许多标准混音，涵盖各种营销用例。 但是，您也可以创建和编辑自己的自定义混合，以定义与XDM模式内业务相关的其他概念。 本指南概述了如何在平台UI中为您的组织创建、编辑和管理自定义混合。

## 先决条件

本指南要求对XDM系统有有效的了解。 有关XDM在Experience Platform生态系统中的作用的介绍，请参阅[XDM概述](../../home.md)，以及[模式组合基础知识](../../schema/composition.md)，了解混合对XDM模式的贡献。

虽然本指南不是必需的，但建议您还要按照[在UI](../../tutorials/create-schema-ui.md)中编写模式的教程来熟悉[!DNL Schema Editor]的各种功能。

## 创建新的混音{#create}

要创建新的混音，您必须首先选择要添加混音的模式。 您可以选择[创建新模式](./schemas.md#create)或[选择现有模式进行编辑。](./schemas.md#edit)

在[!DNL Schema Editor]中打开模式后，选择左边栏中[!UICONTROL  Mixins]部分旁边的&#x200B;**[!UICONTROL 添加]**。

![](../../images/ui/resources/mixins/add-mixin-button.png)

将显示一个对话框，其中显示组织的现有混音的列表。 在对话框顶部附近，选择&#x200B;**[!UICONTROL 新建混音]**。 在此，可以为混音提供&#x200B;**[!UICONTROL 显示名称]**&#x200B;和&#x200B;**[!UICONTROL 说明]**。 完成后，选择&#x200B;**[!UICONTROL 添加mixin]**。

![](../../images/ui/resources/mixins/create-mixin.png)

将重新显示[!DNL Schema Editor]，左边栏中列出新混音。 由于这是全新的混音，因此它当前不向模式提供任何字段，因此画布将保持不变。 您现在可以开始[向mixin](#add-fields)添加字段。

## 编辑{#edit}中的现有混音

>[!NOTE]
>
>只有组织定义的自定义混音才能完全编辑和自定义。 对于Adobe定义的核心混音，在单个模式的上下文中只能编辑其字段的显示名称。 有关详细信息，请参阅[编辑模式字段的显示名称部分](./schemas.md#display-names)。
>
>一旦在模式中保存并使用自定义混音以获取数据，之后只能对混音进行附加更改。 有关详细信息，请参阅[模式演化规则](../../schema/composition.md#evolution)。

要编辑现有的混音，必须首先在[!DNL Schema Editor]中打开使用混音的模式。 您可以[选择要编辑的现有模式](./schemas.md#edit)，也可以[创建新模式](./schemas.md#create)并添加相关的混音。

在编辑器中打开模式后，可以开始[向mixin](#add-fields)添加字段。

## 将字段添加到混音{#add-fields}

要在[!DNL Schema Editor]中向混音添加字段，请在左边栏中选择混音的名称，然后在画布中选择该开始名称旁的&#x200B;**加号(+)**&#x200B;图标。

![](../../images/ui/resources/mixins/add-field-button.png)

画布中会显示&#x200B;**[!UICONTROL 新字段]**，右边栏会更新以显示用于配置字段属性的控件。 有关如何配置字段并将其添加到混音中的特定步骤，请参见UI](../fields/overview.md#define)中的[定义字段的指南。

继续向混音添加所需数量的字段。 完成后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存模式和混音。

![](../../images/ui/resources/mixins/complete-mixin.png)

如果同一混音已用于其他模式，则新添加的字段将自动显示在这些模式中。

## 后续步骤

本指南介绍如何使用平台UI创建和编辑混合。 有关[!UICONTROL 模式]工作区功能的详细信息，请参阅[[!UICONTROL 模式]工作区概述](../overview.md)。

要了解如何使用[!DNL Schema Registry] API管理混音，请参阅[mixins端点指南](../../api/mixins.md)。