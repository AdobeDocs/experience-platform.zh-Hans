---
keywords: Experience Platform；配置文件；实时客户配置文件；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；合并架构；UNION PROFILE；合并配置文件
title: 合并架构UI指南
type: Documentation
description: 在Adobe Experience Platform用户界面(UI)中，您可以轻松地查看组织内的任何合并架构，并预览特定类的字段、身份、关系和参与架构。 本指南提供了有关如何使用Platform UI查看和浏览合并架构的详细信息。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---

# [!UICONTROL 合并模式] UI指南

在Adobe Experience Platform用户界面(UI)中，您可以轻松地查看组织内的任何合并架构，并预览特定类的字段、身份、关系和参与架构。 本指南提供了有关如何使用Platform UI查看和浏览合并架构的详细信息。

## 快速入门

本UI指南要求您了解各种 [!DNL Experience Platform] 与管理Real-Time Customer Profile数据有关的服务。 在阅读本指南或使用UI之前，请查看以下服务的文档：

* [[!DNL Real-Time Customer Profile]](../home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [[!DNL Identity Service]](../../identity-service/home.md)：启用 [!DNL Real-Time Customer Profile] 在引入身份时，通过桥接来自不同数据源的身份 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

## 了解合并架构

Real-Time Customer Profile使您能够创建强大、集中的用户档案，其中包含客户属性和带有时间戳的事件，以及客户在与Adobe Experience Platform集成的系统间进行的每次交互。 此数据的格式和结构由体验数据模型(XDM)架构提供，每个架构都基于XDM类并包含与该类兼容的字段。

可以为多个用例创建架构，引用同一类但包含特定于其用法的字段。 为配置文件启用某个架构后，它将成为合并架构的一部分。 换句话说，联合架构由共享同一类并已为配置文件启用的多个架构组成。 合并模式使您能够看到共享同一类的模式中包含的所有字段的合并。Real-time Customer Profile使用合并模式创建每个客户的整体视图。

使用合并架构需要深入了解XDM架构。 欲知更多信息，请首先阅读 [模式组合基础](../../xdm/schema/composition.md).

## 查看合并架构

要导航到Platform UI中的合并架构，请选择 **[!UICONTROL 配置文件]** 从左侧导航中，然后选择 **[!UICONTROL 合并架构]** 选项卡。 此 [!UICONTROL 合并架构] 选项卡打开以显示当前所选类的合并架构。

![此时将显示“合并架构”页，其中高亮显示了“配置文件和合并架构”选项卡。](../images/union-schema/landing.png)

## 选择类

要显示特定XDM类的合并架构，请从 **[!UICONTROL 类]** 下拉菜单。 由于并非所有类都具有联合架构，因此下拉菜单中只有具有联合架构的类（即具有已为配置文件启用的架构的类）可用。

选择类后，显示的架构将更新，以反映所选类的合并架构。 例如，您可以选择 **[!UICONTROL XDM个人资料]** 查看该类的合并架构。

![包含合并模式的类的下拉列表会突出显示。](../images/union-schema/class.png)

## 探索合并架构

您可以通过上下滚动查看完整的模式结构并选择右角括号(`>`)以展开嵌套字段。

![合并架构中的一组嵌套字段已展开。](../images/union-schema/explore.png)

选择任意字段可查看其详细信息，包括显示名称、数据类型、描述、路径、创建日期和上次修改日期。 您还可以查看包含所选字段的参与架构列表。

![合并架构字段会突出显示。 有关高亮显示的字段的详细信息将显示在右侧边栏中。](../images/union-schema/explore-field.png)

选择参与架构的名称会显示与该架构相关的数据集的名称，这些数据集正在将数据摄取到所选字段中。 每个数据集名称都显示为链接。 选择数据集名称将在新窗口中打开该数据集的“活动”选项卡。

有关数据集的更多信息，包括在UI中查看数据集活动和预览数据集数据，请访问 [数据集UI指南](../../catalog/datasets/user-guide.md).

![与架构相关的数据集列表会突出显示。](../images/union-schema/datasets.png)

## 查看参与模式

您还可以通过选择查看哪些特定架构对合并架构有贡献 **[!UICONTROL 所有参与架构]** 以展开架构列表。 根据您选择的类以及贵组织在Platform中创建的架构数，这可能是包含单个架构的简短列表，也可能是包含多个架构的详细列表。

![突出显示对合并模式有贡献的模式的列表。](../images/union-schema/contributing-schemas.png)

选择特定架构的名称会突出显示合并架构中属于所选架构一部分的字段。 选择架构后，合并架构显示为灰色，黑色条指示作为参与架构一部分的字段。

![选中的参与模式会突出显示。 属于贡献架构一部分的字段保持为黑色，而不属于贡献架构一部分的字段则灰显。](../images/union-schema/select-schema.png)

## 查看身份

通过UI，您可以通过选择，查看合并架构中包含的标识列表 **[!UICONTROL 身份]** 以展开列表。

![属于合并架构的标识会突出显示。](../images/union-schema/identities.png)

从列表中选择单个身份会导致显示的架构根据需要自动更新，以显示身份字段。 如果标识字段已嵌套，这可能包括展开多个字段。

身份字段在合并架构中高亮显示，并且身份的详细信息显示在屏幕的右侧。 详细信息包括参与架构的列表，其中包含身份字段，您可以细化以查找与该架构相关的数据集的链接，这些数据集正在将数据摄取到选定的身份字段中。

![选定的标识会突出显示。 有关所选身份的详细信息，将显示在右侧边栏中。](../images/union-schema/select-identity.png)

## 查看关系

合并架构UI还允许您查看已根据所选架构类为架构定义的关系。 定义关系是连接属于不同类的两个架构的一种方法，以便获得对客户数据的更复杂的见解。

如果已为所选类建立关系，请选择 **[!UICONTROL 关系]** 显示用于创建关系的字段列表。 并非所有架构都使用或需要定义关系，因此关系部分通常不包含任何字段。

要了解有关架构关系的更多信息，包括如何使用UI定义这些关系，请访问 [此文档介绍架构关系](../../xdm/tutorials/relationship-ui.md).

![属于合并架构的关系会突出显示。](../images/union-schema/relationships.png)

从列表中选择关系字段会导致显示的架构根据需要更新，以显示高亮显示的关系字段。 如果关系字段已嵌套，这可能包括展开多个字段。

![选定的关系会突出显示。 关系对应的字段也会突出显示。](../images/union-schema/select-relationship.png)

## 后续步骤

阅读本指南，您现在知道如何使用 [!DNL Experience Platform] UI。 有关架构的更多信息（包括如何在整个Platform中使用它们），请首先阅读 [XDM系统概述](../../xdm/home.md).
