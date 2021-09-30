---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件功能板；功能板
title: 用户档案仪表板
description: Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关贵组织实时客户资料数据的重要信息。
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: d5c69972426008809c3fd0ac03be995efcc2f541
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---

#  用户档案仪表板

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

>[!NOTE]
>
>如果贵组织是Platform的新用户，但尚未创建活动的配置文件数据集或合并策略，则[!UICONTROL Profiles]功能板将不可见。 相反， [!UICONTROL 概述]选项卡会显示可帮助您开始使用实时客户资料的链接和文档。

![](../images/profiles/dashboard-overview.png)

### 修改[!UICONTROL Profiles]功能板

通过选择&#x200B;**[!UICONTROL 修改功能板]**，可以修改[!UICONTROL Profiles]功能板的外观。 这样，您就可以在功能板中移动、添加和删除小组件，以及访问&#x200B;**[!UICONTROL 小组件库]**，以探索可用的小组件并为贵组织创建自定义小组件。

有关更多信息，请参阅[修改功能板](../customize/modify.md)和[小组件库概述](../customize/widget-library.md)文档。

## 合并策略 {#merge-policies}

[!UICONTROL Profiles]功能板中显示的量度基于应用于实时Customer Profile数据的合并策略。 当从多个来源收集数据以创建客户配置文件时，数据可能包含冲突值（例如，一个数据集可能将一个客户列为“单个”，而另一个数据集可能将该客户列为“已婚”）。 合并策略的作业是确定哪些数据要优先排序，并作为用户档案的一部分显示。

有关合并策略的详细信息，包括如何为贵组织创建、编辑和声明默认的合并策略，请首先阅读[合并策略概述](../../profile/merge-policies/overview.md)。

功能板将自动选择要显示的合并策略，但您可以使用下拉菜单更改选定的合并策略。 要选择其他合并策略，请选择合并策略名称旁边的下拉列表，然后选择要查看的合并策略。

>[!NOTE]
>
>下拉菜单仅显示与XDM单个配置文件类相关的合并策略，但是，如果您的组织已创建多个合并策略，则可能意味着您需要滚动才能查看可用合并策略的完整列表。

![](../images/profiles/select-merge-policy.png)

## 小组件和量度

功能板由小组件组成，这些小组件是只读量度，提供有关用户档案数据的重要信息。

小组件上的“上次更新”日期和时间，会显示拍摄数据的最后快照的时间。 快照的日期和时间以UTC格式提供；它不在单个用户或IMS组织的时区中。

## 标准小组件

Adobe提供了多个标准小组件，您可以使用这些小组件来可视化与用户档案数据相关的不同量度。 您还可以使用[!UICONTROL Widget库]创建要与贵组织共享的自定义小组件。 要了解有关创建自定义小组件的更多信息，请首先阅读[小组件库概述](../customize/widget-library.md)。

要进一步了解每个可用的标准小组件，请从以下列表中选择小组件的名称：

* [[!UICONTROL 用户档案计数]](#profile-count)
* [[!UICONTROL 添加了用户档案]](#profiles-added)
* [[!UICONTROL 用户档案计数趋势]](#profiles-count-trend)
* [[!UICONTROL 按身份划分的用户档案]](#profiles-by-identity)
* [[!UICONTROL 身份重叠]](#identity-overlap)

### [!UICONTROL 用户档案计数] {#profile-count}

**[!UICONTROL 配置文件计数]**&#x200B;小组件显示拍摄快照时配置文件数据存储中合并的配置文件总数。 此数字是将所选合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为每个人形成一个配置文件。

有关详细信息，请参阅本文档前面有关合并策略的[部分。](#merge-policies)

>[!NOTE]
>
>由于多种原因，[!UICONTROL 配置文件计数]小组件显示的配置文件计数可能与UI[!UICONTROL Profiles]部分的[!UICONTROL Browse]选项卡中显示的配置文件计数不同。 最常见的原因是，[!UICONTROL Browse]选项卡根据贵组织的默认合并策略引用合并配置文件的总数，而[!UICONTROL 配置文件计数]小组件根据您选择在功能板中查看的合并策略引用合并配置文件的总数。
>
>另一个常见原因是，在[!UICONTROL Browse]选项卡中，拍摄功能板快照的时间与运行示例作业的时间之间存在差异。 您可以通过查看小组件上的时间戳来查看上次更新[!UICONTROL 配置文件计数]小组件的时间，并要详细了解如何在[!UICONTROL Browse]选项卡上触发示例作业，请参阅实时客户配置文件UI指南](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count)中的[配置文件计数部分。

![](../images/profiles/profile-count.png)

### [!UICONTROL 添加了用户档案] {#profiles-added}

添加的&#x200B;**[!UICONTROL 配置文件]**&#x200B;小组件显示自上次拍摄快照起添加到配置文件数据存储的合并配置文件总数。 此数字是将所选合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为每个人形成一个配置文件。 您可以使用下拉选择器查看过去30天、90天或12个月内添加的用户档案。

>[!NOTE]
>
>添加的[!UICONTROL 配置文件]小组件反映在贵组织进行初始配置后添加到系统的配置文件数量。 要了解有关将用户档案添加到用户档案存储的更多信息，请参阅[Real-time Customer Profile文档](../../profile/home.md)。
>
>例如，如果在配置期间添加了400万个配置文件，并且您在过去30天内又添加了100万个配置文件，则[!UICONTROL 添加的配置文件]小组件将显示“1,000,000”，而[!UICONTROL 配置文件计数]小组件将显示“5,000,000”。

![](../images/profiles/profiles-added.png)

### [!UICONTROL 用户档案计数趋势] {#profiles-count-trend}

**[!UICONTROL 配置文件计数趋势]**&#x200B;小组件显示过去30天、90天或12个月内每天添加到配置文件数据存储中的合并配置文件总数。 此数字在拍摄快照时每天都会更新，因此，如果要将配置文件摄取到平台，则在拍摄下一个快照之前不会反映配置文件数量。 添加的用户档案计数是将选定的合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并在一起，为每个人形成一个用户档案。

有关详细信息，请参阅本文档前面有关合并策略的[部分。](#merge-policies)

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL 按身份划分的用户档案] {#profiles-by-identity}

**[!UICONTROL 按身份划分的配置文件]**&#x200B;小组件显示Profile存储区中所有合并配置文件的身份划分。 按身份划分的用户档案总数（即将每个命名空间显示的值相加）可能大于合并的用户档案总数，因为一个用户档案可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌交互，则多个命名空间将与该个别客户关联。

有关详细信息，请参阅本文档前面有关合并策略的[部分。](#merge-policies)

要了解有关身份的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL 身份重叠] {#identity-overlap}

**[!UICONTROL 身份重叠]**&#x200B;小组件显示维恩图或设置图，其中显示了包含多个身份的配置文件存储区中配置文件的重叠。

使用小组件上的下拉菜单选择要比较的身份后，圆圈会显示每个身份的相对大小，其中包含两个命名空间的用户档案数量由圈子之间重叠的大小表示。 如果客户在多个渠道上与您的品牌进行交互，则多个身份将与该个别客户关联，因此，您的组织可能具有多个包含多个身份片段的用户档案。

有关配置文件片段的更多信息，请首先阅读实时客户配置文件概述中[配置文件片段与合并配置文件](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles)中的部分。

要了解有关身份的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/identity-overlap.png)

## 后续步骤

通过阅读本文档，您现在应该能够找到“配置文件”功能板并了解可用小组件中显示的量度。 要了解有关在Experience PlatformUI中使用[!DNL Profile]数据的更多信息，请参阅[实时客户配置文件UI指南](../../profile/ui/user-guide.md)。
