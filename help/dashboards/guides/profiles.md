---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件功能板；功能板
title: 用户档案仪表板
description: Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关贵组织实时客户资料数据的重要信息。
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# （测试版）[!UICONTROL 配置文件]功能板

>[!IMPORTANT]
>
>本文档中概述的功能板功能目前处于测试阶段，并非所有用户都能使用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过该功能板可以查看有关[!DNL Real-time Customer Profile]数据的重要信息，这些信息是在每日快照期间捕获的。 本指南概述了如何在UI中访问和使用[!UICONTROL Profiles]功能板，并提供有关功能板中显示的量度的信息。

有关Experience Platform用户界面中所有配置文件功能的概述，请访问[实时客户配置文件UI指南](../../profile/ui/user-guide.md)。

## 用户档案功能板数据

[!UICONTROL Profiles]功能板显示贵组织在其Experience Platform的Profile存储中拥有的属性（记录）数据的快照。 快照不包含任何事件（时间系列）数据。

快照中的属性数据完全显示快照拍摄时在特定时间点显示的数据。 换句话说，快照不是数据的近似值或样本，而且“配置文件”功能板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新，在拍摄下一个快照之前不会反映在功能板中。

## 浏览[!UICONTROL Profiles]功能板

要导航到Platform UI中的[!UICONTROL Profiles]功能板，请选择左边栏中的&#x200B;**[!UICONTROL Profiles]** ，然后选择&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡以显示功能板。

![](../images/profiles/dashboard-overview.png)

### 选择合并策略

[!UICONTROL Profiles]功能板中显示的量度基于应用于实时Customer Profile数据的合并策略。 当从多个源收集数据时，数据可能包含冲突的值（例如，一个数据集可能将一个客户列为“单个”，而另一个数据集可能将该客户列为“已婚”），合并策略的工作是确定哪些数据要优先排序并作为配置文件的一部分显示。

功能板将自动选择要显示的合并策略，但您可以使用下拉菜单更改选定的合并策略。 要选择其他合并策略，请选择合并策略名称旁边的下拉列表，然后选择要查看的合并策略。

>[!NOTE]
>
>下拉菜单仅显示与XDM单个配置文件类相关的合并策略，但是，如果您的组织已创建多个合并策略，则可能意味着您需要滚动才能查看可用合并策略的完整列表。

有关合并策略的详细信息，包括如何为贵组织创建、编辑和声明默认的合并策略，请首先阅读[合并策略概述](../../profile/merge-policies/overview.md)。

![](../images/profiles/select-merge-policy.png)

### 小组件和量度

功能板由小组件组成，这些小组件是只读量度，提供有关用户档案数据的重要信息。 小组件上的“上次更新”日期和时间，会显示拍摄数据的最后快照的时间。

![](../images/profiles/dashboard-timestamp.png)

## 可用小组件

Experience Platform提供了多个小组件，您可以使用这些小组件来可视化与用户档案数据相关的不同量度。 选择下面小组件的名称，以了解更多信息：

* [[!UICONTROL 受众大小]](#audience-size)
* [[!UICONTROL 添加了用户档案]](#profiles-added)
* [[!UICONTROL 随着时间的推移添加的用户档案]](#profiles-added-over-time)
* [[!UICONTROL 按命名空间划分的配置文件]](#profiles-by-namespace)
* [[!UICONTROL 命名空间重叠]](#namespace-overlap)

### [!UICONTROL 受众大小] {#audience-size}

**[!UICONTROL 受众大小]**&#x200B;小组件显示拍摄快照时配置文件数据存储中合并的配置文件总数。 此数字是将所选合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为每个人形成一个配置文件。

有关片段和合并配置文件的更多信息，请首先阅读[实时客户配置文件概述](../../profile/home.md)的&#x200B;*配置文件片段与合并配置文件*&#x200B;部分。

>[!NOTE]
>
>用于计算此量度的合并策略与用于在[!UICONTROL 许可证使用情况]功能板中计算[!UICONTROL 可寻址受众]的系统生成的合并策略不同，因此，在[!UICONTROL 配置文件]和[!UICONTROL 许可证使用情况]功能板中的受众计数不太可能完全相同。

![](../images/profiles/audience-size.png)

### [!UICONTROL 添加了用户档案] {#profiles-added}

添加的&#x200B;**[!UICONTROL 配置文件]**&#x200B;小组件显示自上次快照拍摄以来添加到配置文件数据存储的合并配置文件总数。 此数字是将所选合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为每个人形成一个配置文件。

![](../images/profiles/profiles-added.png)

### [!UICONTROL 随着时间的推移添加的用户档案] {#profiles-added-over-time}

随着时间的推移添加的&#x200B;**[!UICONTROL 配置文件]**&#x200B;小组件显示过去30天内每天添加到配置文件数据存储中的合并配置文件总数。 此数字在拍摄快照时每天都会更新，因此，如果要将配置文件摄取到平台，则在拍摄下一个快照之前不会反映配置文件数量。

添加的用户档案计数是将选定的合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并在一起，为每个人形成一个用户档案。

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL 按命名空间划分的配置文件] {#profiles-by-namespace}

**[!UICONTROL 按命名空间划分的配置文件]**&#x200B;小组件显示配置文件存储区中所有合并配置文件中身份命名空间的划分。 按[!UICONTROL ID命名空间]（即，将每个命名空间显示的值相加）划分的配置文件总数可能大于合并配置文件总数，因为一个配置文件可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌交互，则多个命名空间将与该个别客户关联。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL 命名空间重叠] {#namespace-overlap}

**[!UICONTROL 命名空间重叠]**&#x200B;小组件显示维恩图或设置图，其中显示了包含多个身份命名空间的配置文件存储区中配置文件的重叠。

使用小组件上的下拉菜单选择要比较的身份命名空间后，圆圈会显示每个命名空间的相对大小，其中包含两个命名空间的配置文件数量由圈子之间的重叠大小表示。

如果客户在多个渠道上与您的品牌进行交互，则多个命名空间将与该个别客户关联，因此，您的组织可能具有多个包含来自多个身份命名空间片段的配置文件。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/namespace-overlap.png)

## 后续步骤

通过阅读本文档，您现在应该能够找到“配置文件”功能板并了解可用小组件中显示的量度。 要了解有关在Experience PlatformUI中使用[!DNL Profile]数据的更多信息，请参阅[实时客户配置文件UI指南](../../profile/ui/user-guide.md)。
