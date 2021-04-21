---
keywords: Experience Platform;用户档案；实时客户用户档案；用户界面；UI；自定义；用户档案仪表板;仪表板
title: 用户档案仪表板
description: Adobe Experience Platform提供了一个仪表板，您可以通过它视图有关组织实时客户用户档案数据的重要信息。
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 1%

---

# （测试版）[!UICONTROL Profiles]仪表板

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可以视图有关[!DNL Real-time Customer Profile]数据的重要信息，这些信息是在每日快照中捕获的。 本指南概述了如何在UI中访问和使用[!UICONTROL Profiles]仪表板，并提供有关仪表板中显示的量度的信息。

有关Experience Platform用户界面中所有用户档案功能的概述，请访问[实时客户用户档案UI指南](../../profile/ui/user-guide.md)。

## 用户档案仪表板数据

[!UICONTROL Profiles]仪表板显示您的组织在Experience Platform中的用户档案存储中拥有的属性（记录）数据的快照。 快照不包括任何事件（时间系列）数据。

快照中的属性数据与拍摄快照时在特定时间点显示的数据完全相同。 换句话说，快照不是数据的近似值或样本，用户档案仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

## 浏览[!UICONTROL Profiles]仪表板

要导航到平台UI中的[!UICONTROL Profiles]仪表板，请在左边栏中选择&#x200B;**[!UICONTROL Profiles]**，然后选择&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡以显示仪表板。

![](../images/profiles/dashboard-overview.png)

### 选择合并策略

[!UICONTROL Profiles]仪表板中显示的量度基于对您的实时客户用户档案数据应用的合并策略。 当从多个源收集数据时，数据可能包含冲突值(例如，一个数据集可能将客户列表为“单一”，而另一个数据集可能将客户列表为“已婚”)，而合并策略的工作是确定哪些数据优先排序并作为用户档案的一部分显示。

仪表板将自动选择要显示的合并策略，但您可以更改使用下拉菜单选择的合并策略。 要选择其他合并策略，请选择合并策略名称旁边的下拉框，然后选择要视图的合并策略。

>[!NOTE]
>
>下拉菜单仅显示与XDM单个用户档案类相关的合并策略，但是，如果您的组织已创建多个合并策略，则可能意味着您需要滚动才能视图可用合并策略的完整列表。

有关合并策略的详细信息，包括如何创建、编辑和声明组织的默认合并策略，请访问[合并策略UI指南](../../profile/ui/merge-policies.md)。

![](../images/profiles/select-merge-policy.png)

### 构件和量度

仪表板由构件组成，构件是只读量度，提供有关用户档案数据的重要信息。 Widget上的“上次更新”日期和时间显示了拍摄数据的最后快照的时间。

![](../images/profiles/dashboard-timestamp.png)

## 可用构件

Experience Platform提供了多个构件，您可以使用这些构件来可视化与您的用户档案数据相关的不同量度。 选择下面的Widget名称以了解更多信息：

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

**[!UICONTROL Audience size]**&#x200B;构件显示拍摄快照时用户档案用户档案存储中合并的总数。 此数字是将选定的合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并到一起，为每个用户档案组成单个。

有关片段和合并用户档案的详细信息，请首先阅读[实时客户用户档案概述](../../profile/home.md)的&#x200B;*用户档案片段与合并用户档案*&#x200B;部分。

>[!NOTE]
>
>用于计算此量度的合并策略与用于在[!UICONTROL License usage]仪表板中计算[!UICONTROL Addressable audiences]的系统生成的合并策略不同，因此[!UICONTROL Profiles]和[!UICONTROL License usage]仪表板中的受众计数不太可能完全相同。

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

**[!UICONTROL Profiles added]**&#x200B;构件显示自拍摄上次快照以来已添加到用户档案用户档案存储的合并总数。 此数字是将选定的合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并到一起，为每个用户档案组成单个。

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

**[!UICONTROL Profiles added over time]**&#x200B;构件显示最近30天内每天添加到用户档案用户档案存储的合并总数。 此数字在拍摄快照时每天更新，因此，如果要将用户档案收录到平台，则直到拍摄下一个快照后，用户档案数才会反映出来。

添加的用户档案数是所选合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并到一起，为每个用户档案组成单个。

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]**&#x200B;构件显示您的用户档案存储中所有合并用户档案的标识命名空间细分。 按[!UICONTROL ID namespace]列出的用户档案总数(即，将每个命名空间显示的值相加)可能高于合并用户档案的总数，因为一个用户档案可能具有与其关联的多个命名空间。 例如，如果一个客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

**[!UICONTROL Namespace overlap]**&#x200B;构件显示一个维恩图或设置图，显示包含多个身份用户档案的用户档案存储中的命名空间重叠。

在使用构件上的下拉菜单选择要比较的标识命名空间后，会出现圆形，显示每个命名空间的相对大小，其中包含两个命名空间的用户档案数由圆之间重叠的大小表示。

如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联，因此您的组织可能有多个用户档案，其中包含来自多个身份命名空间的片段。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/profiles/namespace-overlap.png)

## 后续步骤

通过遵循此文档，您现在应能找到用户档案仪表板并了解可用构件中显示的量度。 要了解有关在Experience Platform UI中使用[!DNL Profile]数据的更多信息，请参阅[实时客户用户档案UI指南](../../profile/ui/user-guide.md)。
