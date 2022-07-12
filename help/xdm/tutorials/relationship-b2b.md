---
title: 在Real-time Customer Data Platform B2B版中定义两个模式之间的关系
description: 了解如何在Real-time Customer Data Platform B2B Edition中定义两个架构之间的多对一关系。
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: b9ec275df738e006d3fec2cdd64b0ed6577dbff8
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# 在Real-time Customer Data Platform B2B Edition中定义两个架构之间的多对一关系

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="参考模式"
>abstract="选择要与之建立关系的架构。 根据架构的类，它可能还与B2B上下文中的其他实体存在关系。"
>text="See the documentation to learn how B2B schema classes relate to each other."

>[!NOTE]
>
>如果您没有使用Real-time Customer Data Platform B2B Edition，或者希望创建一对一的关系，请参阅 [创建一对一关系](./relationship-ui.md) 中。

Real-time Customer Data Platform B2B Edition提供了多个Experience Data Model(XDM)类，用于捕获基本的B2B数据实体，包括 [帐户](../classes/b2b/business-account.md), [机会](../classes/b2b/business-opportunity.md), [营销活动](../classes/b2b/business-campaign.md)，等等。 通过基于这些类构建模式并使它们能够在 [实时客户资料](../../profile/home.md)，您可以将来自不同来源的数据合并到称为合并模式的统一表示形式中。

但是，合并架构只能包含由共享同一类的架构捕获的字段。 这是架构关系的来源。 通过在B2B模式中实施关系，您可以描述这些业务实体如何彼此关联，并可以在下游分段用例中包含来自多个类的属性。

下图提供了不同B2B类在基本实施中如何彼此关联的示例：

![B2B类关系](../images/tutorials/relationship-b2b/classes.png)

本教程介绍了在实时CDP B2B Edition中定义两个架构之间多对一关系的步骤。

>[!NOTE]
>
>本教程重点介绍如何在Platform UI中手动建立B2B模式之间的关系。 如果您从B2B源连接中导入数据，则可以使用自动生成实用程序来创建所需的架构、标识和关系。 有关B2B命名空间和模式的更多信息，请参阅源文档 [使用自动生成实用程序](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## 快速入门

本教程需要对 [!DNL XDM System] 和模式编辑器 [!DNL Experience Platform] UI。 在开始使用本教程之前，请查阅以下文档：

* [XDM系统在Experience Platform](../home.md):XDM及其在 [!DNL Experience Platform].
* [架构组合的基础知识](../schema/composition.md):介绍XDM模式的构建基块。
* [使用创建架构 [!DNL Schema Editor]](create-schema-ui.md):本教程介绍了如何在UI中构建和编辑模式的基础知识。

## 定义源架构和目标架构

您应该已经创建了将在关系中定义的两个架构。 出于演示目的，本教程将在业务机会(在[!DNL Opportunities]“模式”)及其关联的业务帐户(在“[!DNL Accounts]“架构”)。

架构关系由 **源模式** 引用 **目标架构**. 在后续步骤中，“[!DNL Opportunities]“ ”用作源架构，而“[!DNL Accounts]“ ”用作目标架构。

### 了解B2B关系中的身份

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="引用标识命名空间"
>abstract="引用架构的主标识字段的命名空间（类型）。 引用架构必须具有已建立的主标识字段才能参与关系。"
>text="See the documentation to learn more about identities in B2B relationships."

要建立关系，目标架构必须具有定义的主标识。 在为B2B实体设置主标识时，请记住，如果您跨不同系统或位置收集基于字符串的实体ID，则它们可能会重叠，这可能会导致平台中的数据冲突。

为此，所有标准B2B类都包含符合 [[!UICONTROL B2B源] 数据类型](../data-types/b2b-source.md). 此数据类型提供B2B实体的字符串标识符的字段以及有关该标识符源的其他上下文信息。 其中一个领域， `sourceKey`，关联数据类型中其他字段的值，以生成实体的唯一标识符。 此字段应始终用作B2B实体架构的主标识。

![sourceKey字段](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>When [将XDM字段设置为标识](../ui/fields/identity.md)，则必须提供标识命名空间才能在下定义标识。 这可以是由Adobe提供的标准命名空间，也可以是由您的组织定义的自定义命名空间。 实际上，命名空间只是一个上下文字符串，可以设置为您喜欢的任何值，前提是该命名空间对于对您的组织进行身份类型分类很有意义。 请参阅 [身份命名空间](../../identity-service/namespaces.md) 以了解更多信息。

出于参考目的，以下各节介绍了在定义关系之前本教程中使用的每个架构的结构。 请注意在架构结构中定义了主标识的位置以及它们使用的自定义命名空间。

### [!DNL Opportunities] 模式

源架构“[!DNL Opportunities]“ ”基于 [!UICONTROL XDM业务机会] 类。 类提供的一个字段， `opportunityKey`，用作架构的标识符。 具体而言， `sourceKey` 字段 `opportunityKey` 对象在名为的自定义命名空间下设置为架构的主标识 [!DNL B2B Opportunity].

如 **[!UICONTROL 架构属性]**，此架构已启用，可在中使用 [!DNL Real-time Customer Profile].

![机会模式](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] 模式

目标架构“[!DNL Accounts]“ ”基于 [!UICONTROL XDM帐户] 类。 根级别 `accountKey` 字段包含 `sourceKey` 在名为的自定义命名空间下用作其主标识的 [!DNL B2B Account]. 此架构也已启用，可在用户档案中使用。

![帐户架构](../images/tutorials/relationship-b2b/accounts.png)

## 为源架构定义关系字段 {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="当前架构中的关系名称"
>abstract="一个标签，用于描述从当前架构到引用架构的关系（例如，“相关帐户”）。 此标签用于配置文件和分段，以提供来自相关B2B实体的数据的上下文。"
>text="See the documentation to learn more about building B2B schema relationships."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="引用架构中的关系名称"
>abstract="一个标签，用于描述从引用架构到当前架构（例如，“相关商机”）的关系。 此标签用于配置文件和分段，以提供来自相关B2B实体的数据的上下文。"
>text="See the documentation to learn more about building B2B schema relationships."

要定义两个架构之间的关系，源架构必须具有引用目标架构主标识的专用字段。 标准B2B类包括适用于常见相关业务实体的专用源密钥字段。 例如， [!UICONTROL XDM业务机会] 类包含相关帐户的源键字段(`accountKey`)和相关的营销活动(`campaignKey`)。 但是，您还可以添加其他 [!UICONTROL B2B源] 字段（如果需要的组件数超过默认组件数）。

>[!NOTE]
>
>目前，只能从源架构定义到目标架构的多对一和一对一关系。 对于一对多关系，您必须在架构中定义表示“多”的关系字段。

要设置关系字段，请选择箭头图标(![箭头图标](../images/tutorials/relationship-b2b/arrow.png))。 对于 [!DNL Opportunities] 架构，这是 `accountKey.sourceKey` 字段，因为其目标是与帐户建立多对一关系。

![“关系”按钮](../images/tutorials/relationship-b2b/relationship-button.png)

此时将显示一个对话框，用于指定有关关系的详细信息。 关系类型自动设置为 **[!UICONTROL 多对一]**.

![关系对话框](../images/tutorials/relationship-b2b/relationship-dialog.png)

在 **[!UICONTROL 参考模式]**，请使用搜索栏查找目标架构的名称。 突出显示目标架构的名称时， **[!UICONTROL 引用标识命名空间]** 字段会自动更新架构主标识的命名空间。

![参考模式](../images/tutorials/relationship-b2b/reference-schema.png)

在 **[!UICONTROL 当前架构中的关系名称]** 和 **[!UICONTROL 引用架构中的关系名称]**，分别在源架构和目标架构的上下文中为关系提供友好名称。 完成后，选择 **[!UICONTROL 保存]** 以应用更改并保存架构。

![关系名称](../images/tutorials/relationship-b2b/relationship-name.png)

画布将重新显示，现在使用您之前提供的友好名称标记关系字段。 关系名称也列在左边栏下方，以便于参考。

![已应用的关系](../images/tutorials/relationship-b2b/relationship-applied.png)

如果您查看目标架构的结构，则关系标记将显示在架构的主标识字段旁边和左边栏中。

![目标架构关系标记](../images/tutorials/relationship-b2b/destination-relationship.png)

## 后续步骤

通过阅读本教程，您已使用 [!DNL Schema Editor]. 使用基于这些架构的数据集摄取数据并在用户档案数据存储中激活数据后，您便可以将两个架构中的属性用于多类分段用例。 有关更多信息，请参阅Real-time CDP B2B Edition文档。
