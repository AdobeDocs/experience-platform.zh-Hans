---
keywords: Experience Platform；配置文件；实时客户配置文件；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；合并架构；UNION PROFILE；合并配置文件
title: 合并架构UI指南
type: Documentation
description: 在Adobe Experience Platform用户界面(UI)中，您可以轻松查看组织内的任何合并架构，并预览特定类的字段、身份、关系和参与架构。 本指南提供了有关如何使用Experience Platform UI查看和浏览合并架构的详细信息。
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%

---

# [!UICONTROL 合并架构] UI指南

在Adobe Experience Platform用户界面(UI)中，您可以轻松查看组织内的任何合并架构，并预览特定类的字段、身份、关系和参与架构。 本指南提供了有关如何使用Experience Platform UI查看和浏览合并架构的详细信息。

## 快速入门

本UI指南要求您了解与管理Real-time Customer Profile数据有关的各种[!DNL Experience Platform]服务。 在阅读本指南或使用UI之前，请查看以下服务的文档：

* [[!DNL Real-Time Customer Profile]](../home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Identity Service]](../../identity-service/home.md)：在将[!DNL Real-Time Customer Profile]引入到[!DNL Experience Platform]中时，通过桥接来自不同数据源的标识来启用它们。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。

## 了解合并架构

Real-Time Customer Profile使您能够创建强大、集中的用户档案，其中包含客户属性和带有时间戳的事件，以及与Adobe Experience Platform集成的系统间每个客户交互。 此数据的格式和结构由体验数据模型(XDM)架构提供，每个架构都基于XDM类并包含与该类兼容的字段。

可以为多个用例创建架构，这些架构引用同一类，但包含特定于其使用的字段。 为配置文件启用某个架构后，它将成为合并架构的一部分。 换言之，联合架构由共享同一类并已为配置文件启用的多个架构组成。 合并架构允许您查看共享同一类的架构中包含的所有字段的合并。 实时客户配置文件使用合并架构创建每个客户的整体视图。

使用合并模式需要深入了解XDM模式。 有关详细信息，请先阅读架构组合[&#128279;](../../xdm/schema/composition.md)的基础知识。

## 查看合并架构

要导航到Experience Platform UI中的合并架构，请从左侧导航中选择&#x200B;**[!UICONTROL 配置文件]**，然后选择&#x200B;**[!UICONTROL 合并架构]**&#x200B;选项卡。 将打开[!UICONTROL 合并架构]选项卡以显示当前选定类的合并架构。

![将显示“合并架构”页面，并突出显示“配置文件和合并架构”选项卡。](../images/union-schema/landing.png)

## 选择一个类

要显示特定XDM类的合并架构，请从&#x200B;**[!UICONTROL 类]**&#x200B;下拉列表中选择该类。 由于并非所有类都具有联合架构，因此下拉菜单中只有具有联合架构的类（即具有已为配置文件启用的架构的类）可用。

选择类后，显示的架构将更新以反映所选类的合并架构。 例如，您可以选择&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;来查看该类的合并架构。

![包含合并架构的类的下拉列表突出显示。](../images/union-schema/class.png)

## 浏览合并架构

您可以通过上下滚动查看完整的架构结构，并选择右尖括号(`>`)展开嵌套字段来浏览合并架构。

![合并架构中的一组嵌套字段已展开。](../images/union-schema/explore.png)

选择任意字段以查看其详细信息，包括显示名称、数据类型、描述、路径、创建日期和上次修改日期。 您还可以查看包含所选字段的参与架构列表。

![联合架构字段已突出显示。 有关高亮显示的字段的详细信息将显示在右侧边栏中。](../images/union-schema/explore-field.png)

选择参与架构的名称会显示与该架构相关的数据集的名称，这些数据集正在将数据摄取到所选字段中。 每个数据集名称都显示为链接。 选择数据集名称将在新窗口中打开该数据集的活动选项卡。

有关数据集的更多信息，包括在UI中查看数据集活动和预览数据集数据，请访问[数据集UI指南](../../catalog/datasets/user-guide.md)。

![与架构相关的数据集列表已突出显示。](../images/union-schema/datasets.png)

## 查看参与架构

您还可以通过选择&#x200B;**[!UICONTROL 所有参与架构]**&#x200B;来展开架构列表，以查看哪些特定架构正在参与合并架构。 根据您选择的类以及贵组织在Experience Platform中创建的架构数，该列表可以是包含单个架构的简短列表，也可以是包含多个架构的较长列表。

![对合并架构有贡献的架构列表已突出显示。](../images/union-schema/contributing-schemas.png)

选择特定架构的名称会突出显示合并架构中作为所选架构一部分的字段。 选择架构后，合并架构将显示为灰色，其中黑色条指示作为参与架构一部分的字段。

![选定的参与架构突出显示。 作为参与架构一部分的字段仍为黑色，而作为参与架构一部分的字段呈灰色。](../images/union-schema/select-schema.png)

## 查看身份

通过UI，您可以通过选择&#x200B;**[!UICONTROL 标识]**&#x200B;展开合并架构中包含的标识列表。

![属于合并架构的标识已突出显示。](../images/union-schema/identities.png)

从列表中选择单个身份会导致显示的架构根据需要自动更新，以显示身份字段。 如果标识字段已嵌套，这可能包括展开多个字段。

合并架构中会突出显示身份字段，并且屏幕右侧会显示身份的详细信息。 详细信息包括参与架构的列表，该列表包含身份字段，您可以向下钻取以查找与该架构相关的数据集的链接，这些数据集正在将数据摄取到选定的身份字段中。

![所选的标识已突出显示。 有关所选身份的详细信息，将显示在右侧边栏中。](../images/union-schema/select-identity.png)

## 查看关系

合并架构UI还允许您查看已根据所选架构类为架构定义的关系。 定义关系是连接属于不同类的两个架构的一种方法，以便获得有关客户数据的更复杂的见解。

如果已为所选类建立了关系，则选择&#x200B;**[!UICONTROL 关系]**&#x200B;将显示用于创建关系的字段列表。 并非所有架构都使用或需要定义关系，因此关系部分通常不包含任何字段。

若要了解有关架构关系的详细信息，包括如何使用UI定义这些关系，请访问[有关架构关系的本文档](../../xdm/tutorials/relationship-ui.md)。

![属于合并架构的关系突出显示。](../images/union-schema/relationships.png)

从列表中选择关系字段会导致显示的架构根据需要更新，以显示高亮显示的关系字段。 如果关系字段已嵌套，这可能包括展开多个字段。

![选定的关系已突出显示。 关系对应的字段也突出显示。](../images/union-schema/select-relationship.png)

## 后续步骤

通过阅读本指南，您现在知道如何使用[!DNL Experience Platform] UI查看和导航合并架构。 有关架构的更多信息，包括如何在整个Experience Platform中使用它们，请从阅读[XDM系统概述](../../xdm/home.md)开始。
