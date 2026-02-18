---
keywords: Experience Platform；主页；热门主题；UI；UI；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构编辑器；架构编辑器；架构；架构；架构；架构；创建；关系；关系；引用；引用；
solution: Experience Platform
title: 使用架构编辑器定义两个架构之间的关系
description: 本文档提供了一个教程，介绍如何使用Experience Platform用户界面中的架构编辑器定义两个架构之间的关系。
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 9%

---

# 使用 [!DNL Schema Editor] 定义两个架构之间的一对一关系 {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="架构关系"
>abstract="可以通过关系字段对属于不同类的架构进行上下文链接，从而生成更复杂的分段规则。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="参考架构"
>abstract="选择要与之建立关系的架构。此架构可以是与当前架构不同的类。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="参考身份标识命名空间"
>abstract="参考架构的主要身份标识字段的命名空间（类型）。参考架构必须有一个建立的主要身份标识字段才能参与关系。有关架构关系的更多信息，请参阅文档。"

了解客户之间的关系以及客户在不同渠道中与您的品牌之间的互动是Adobe Experience Platform的重要组成部分。 通过在[!DNL Experience Data Model] (XDM)架构的结构中定义这些关系，您可以获得有关客户数据的复杂洞察。

虽然可以使用合并架构和[!DNL Real-Time Customer Profile]推断架构关系，但这仅适用于共享相同类的架构。 要在属于不同类的两个架构之间建立关系，必须在源架构中添加一个专用关系字段，该字段引用其他相关架构的标识。

>[!NOTE]
>
>如果源架构和目标架构都属于同一类，则不应使用专用关系字段&#x200B;**&#x200B;**。 在这种情况下，请使用合并架构UI查看关系。 有关如何执行此操作的说明，请参阅合并架构UI指南的[查看关系](../../profile/ui/union-schema.md#view-relationships)部分。

本文档提供了一个教程，介绍如何在[!DNL Experience Platform]用户界面中使用架构编辑器定义两个架构之间的关系。 有关使用API定义架构关系的步骤，请参阅有关[使用架构注册表API定义关系的教程](relationship-api.md)。

>[!NOTE]
>
>有关如何在Adobe Real-Time Customer Data Platform B2B edition中创建多对一关系的步骤，请参阅有关[创建B2B关系](./relationship-b2b.md)的指南。

## 快速入门

本教程需要您对[!DNL XDM System]和[!DNL Experience Platform] UI中的架构编辑器有一定的了解。 在开始本教程之前，请查看以下文档：

* Experience Platform中的[XDM System](../home.md)： [!DNL Experience Platform]中的XDM及其实现的概述。
* [架构组合的基础知识](../schema/composition.md)： XDM架构的构建块简介。
* [使用 [!DNL Schema Editor]](create-schema-ui.md)创建架构：介绍使用[!DNL Schema Editor]的基础知识的教程。

## 定义源和引用架构

您应已创建将在关系中定义的两个架构。 出于演示目的，本教程将在组织的忠诚度计划（在“[!DNL Loyalty Members]”架构中定义）的成员与其喜爱的酒店（在“[!DNL Hotels]”架构中定义）之间创建关系。

>[!IMPORTANT]
>
>为了建立关系，两个架构都必须定义主标识并启用[!DNL Real-Time Customer Profile]。 如果您需要有关如何相应地配置架构的指导，请参阅架构创建教程中有关[启用架构以用于配置文件](./create-schema-ui.md#profile)的部分。

架构关系由&#x200B;**源架构**&#x200B;中的专用字段表示，该字段指向&#x200B;**引用架构**&#x200B;中的另一个字段。 在接下来的步骤中，“[!DNL Loyalty Members]”将用作源架构，而“[!DNL Hotels]”将用作参考架构。

以下各节介绍在定义关系之前本教程中使用的每个架构的结构。

### [!DNL Loyalty Members]架构

源架构“[!DNL Loyalty Members]”基于[!DNL XDM Individual Profile]类，其中包含描述忠诚度计划成员的字段。 这些字段之一`personalEmail.addess`用作[!UICONTROL Email]命名空间下的架构的主要标识。 如在&#x200B;**[!UICONTROL Schema Properties]**&#x200B;下看到的，此架构已启用以便在[!DNL Real-Time Customer Profile]中使用。

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels]架构

引用架构“[!DNL Hotels]”基于自定义“[!DNL Hotels]”类，并包含描述酒店的字段。 为了参与关系，引用架构还必须定义主标识并为[!UICONTROL Profile]启用。 在这种情况下，`_tenantId.hotelId`使用自定义“[!DNL Hotel ID]”标识命名空间作为架构的主标识。

为配置文件![启用](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>要了解如何创建自定义身份命名空间，请参阅[Identity Service文档](../../identity-service/features/namespaces.md#manage-namespaces)。

## 创建关系字段组

>[!NOTE]
>
>仅当源架构没有专用字符串类型字段用作引用架构的主要标识的指针时，才需要执行此步骤。 如果已在源架构中定义此字段，请跳到[定义关系字段](#relationship-field)的下一步骤。

为了定义两个架构之间的关系，源架构必须具有专用字段，以指示引用架构的主要身份。 您可以通过创建新架构字段组或扩展现有架构字段组，将此字段添加到源架构中。

对于[!DNL Loyalty Members]架构，将添加新的`preferredHotel`字段以指示忠诚度成员首选的公司访问酒店。 首先，选择源架构名称旁边的加号图标(**+**)。

![](../images/tutorials/relationship/loyalty-add-field.png)

画布中将显示一个新的字段占位符。 在&#x200B;**[!UICONTROL Field properties]**&#x200B;下，为字段提供字段名称和显示名称，并将其类型设置为“[!UICONTROL String]”。 在&#x200B;**[!UICONTROL Assign to]**&#x200B;下，选择要扩展的现有字段组，或键入唯一名称以创建新字段组。 在这种情况下，将创建一个新的&quot;[!DNL Preferred Hotel]&quot;字段组。

![](../images/tutorials/relationship/relationship-field-details.png)

完成后，选择&#x200B;**[!UICONTROL Apply]**。

![](../images/tutorials/relationship/relationship-field-apply.png)

更新的`preferredHotel`字段显示在画布中，位于`_tenantId`对象下方，因为它是自定义字段。 选择&#x200B;**[!UICONTROL Save]**&#x200B;以完成对架构的更改。

![](../images/tutorials/relationship/relationship-field-save.png)

## 为源架构定义关系字段 {#relationship-field}

一旦您的源架构定义了专用引用字段，您就可以将其指定为关系字段。

>[!NOTE]
>
>只能对字符串或字符串数组字段支持关系。

在画布中选择`preferredHotel`字段，然后在&#x200B;**[!UICONTROL Add relationship]**&#x200B;侧边栏中选择&#x200B;**[!UICONTROL Field properties]**。

![字段属性侧边栏中突出显示了具有Add关系的架构编辑器。](../images/tutorials/relationship/add-relationship.png)

出现[!UICONTROL Add relationship]对话框。 通过此对话框，您可以设置配置关系字段所需的参数。 对于Real-Time CDP B2C用户，您只能&#x200B;**1&rbrace;在源架构和引用架构之间设置一对一关系。**

>[!NOTE]
>
>如果您有权访问Real-Time CDP B2B edition，则可以使用画布的右边栏控件定义关系字段，并使用[相同对话框](./relationship-b2b.md#relationship-field)构建多对一关系。

![添加关系对话框。](../images/tutorials/relationship/add-relationship-dialog.png)

使用&#x200B;**[!UICONTROL Reference schema]**&#x200B;的下拉列表并选择关系的引用架构（本示例中为“[!DNL Hotels]”）。

>[!NOTE]
>
>只有包含主标识的架构才会包含在引用架构下拉菜单中。 此安全保护可防止您意外与尚未正确配置的架构创建关系。

引用架构的标识命名空间（在本例中为“[!DNL Hotel ID]”）自动填充到&#x200B;**[!UICONTROL Reference identity namespace]**&#x200B;下。 完成后，选择 **[!UICONTROL Apply]**。

![已配置关系参数并突出显示了“添加关系”对话框。](../images/tutorials/relationship/apply-relationship.png)

`preferredHotel`字段现在在画布中作为关系突出显示，显示引用架构的名称。 选择&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改并完成工作流。

![突出显示关系引用和“保存”的架构编辑器。](../images/tutorials/relationship/relationship-save.png)

### 编辑现有关系字段 {#edit-relationship}

要更改引用架构，请选择具有现有关系的字段，然后在&#x200B;**[!UICONTROL Edit relationship]**&#x200B;侧边栏中选择&#x200B;**[!UICONTROL Field properties]**。

![已突出显示具有编辑关系的架构编辑器。](../images/tutorials/relationship/edit-relationship.png)

出现[!UICONTROL Edit relationship]对话框。 从此处，您可以按照[中列出的流程定义关系字段](#relationship-field)或删除关系。 选择&#x200B;**[!UICONTROL Delete relationship]**&#x200B;以移除与引用架构的关系。

![编辑关系对话框。](../images/tutorials/relationship/edit-relationship-dialog.png)

## 筛选和搜索关系 {#filter-and-search}

您可以从[!UICONTROL Relationships]工作区的[!UICONTROL Schemas]选项卡筛选和搜索架构中的特定关系。 您可以使用此视图快速找到和管理您的关系。 有关筛选选项的详细说明，请阅读有关[浏览架构资源](../ui/explore.md#lookup)的文档。

![架构工作区中的“关系”选项卡。](../images/tutorials/relationship-b2b/relationship-tab.png)

## 后续步骤

通过学习本教程，您已使用[!DNL Schema Editor]成功地创建了两个架构之间的一对一关系。 有关如何使用API定义关系的步骤，请参阅有关[使用架构注册表API定义关系的教程](relationship-api.md)。
