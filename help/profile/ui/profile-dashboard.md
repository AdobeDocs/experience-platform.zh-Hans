---
keywords: Experience Platform;用户档案；实时用户档案；用户界面；UI；自定义；用户档案仪表板;仪表板
title: 用户档案仪表板UI指南
description: '本指南概述了Adobe Experience PlatformUI中提供的实时客户用户档案仪表板。 '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# (Alpha)[!DNL Real-time Customer Profile]仪表板{#profile-dashboard}

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前位于alpha中，并且并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可以视图有关[!DNL Real-time Customer Profile]数据的重要信息，这是在每日快照中捕获的。 本指南概述了如何在UI中访问和使用[!DNL Profile]仪表板，并提供了有关仪表板中显示的度量的更多信息。

有关用户档案用户界面中所有Experience Platform功能的概述，请访问[实时客户用户档案UI指南](user-guide.md)。

## 用户档案仪表板数据

用户档案仪表板显示您的组织在Experience Platform中的用户档案存储中具有的属性（记录）数据的快照。 快照不包括任何事件（时间序列）数据。

快照中的属性数据与拍摄快照时在特定时间点显示的数据完全相同。 换言之，快照不是数据的近似值或样本，用户档案仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

用户档案仪表板中显示的量度基于组织的默认合并策略。 有关合并策略以及如何选择或更改默认合并策略的详细信息，请访问[合并策略UI指南](merge-policies.md)。

## 探索用户档案仪表板

要导航到平台UI中的用户档案仪表板，请在左边栏中选择&#x200B;**[!UICONTROL 用户档案]**，然后选择&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡以显示仪表板。

![](../images/profile-dashboard/dashboard-overview.png)

### 构件和指标

仪表板由构件组成，构件是只读度量，提供与用户档案数据相关的重要信息。 构件上的“上次更新”日期和时间显示数据的最后快照拍摄的时间。

![](../images/profile-dashboard/dashboard-timestamp.png)

## 可用构件

Experience Platform提供了多个构件，您可以使用这些构件来可视化与用户档案数据相关的不同指标。 选择下面构件的名称以了解更多信息：

* [[!UICONTROL 受众大小]](#audience-size)
* [[!UICONTROL 用户档案，按命名空间]](#profiles-by-namespace)

### [!UICONTROL 受众大小] {#audience-size}

**[!UICONTROL 受众大小]**&#x200B;构件显示拍摄快照时用户档案数据存储中合并用户档案的总数。 此编号是组织的默认合并策略应用于用户档案数据的结果，以便将用户档案片段合并到一起，为每个用户档案组成一个。

有关片段和合并用户档案的详细信息，请首先阅读[用户档案概述](../home.md)的&#x200B;*用户档案片段与合并用户档案*&#x200B;部分。

>[!NOTE]
>
>用于计算此度量的合并策略与用于计算[!UICONTROL 许可证使用情况]仪表板中的[!UICONTROL 可寻址受众]的系统生成的合并策略不同，因此[!DNL Profile]和[!UICONTROL 许可证使用情况]仪表板中的受众计数不太可能完全相同。

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL 用户档案，按命名空间] {#profiles-by-namespace}

按命名空间&#x200B;]**的**[!UICONTROL &#x200B;用户档案构件显示用户档案商店中所有合并用户档案的命名空间细分。 按[!UICONTROL ID用户档案](换言之，将每个命名空间显示的值加在一起)列出的用户档案总数将始终高于合并命名空间总数，因为一个用户档案可能有多个命名空间与其关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform身份服务文档](../../identity-service/home.md)。

![](../images/profile-dashboard/profiles-by-namespace.png)

## 其他仪表板

平台UI提供了更多仪表板，用于在Experience Platform内查看数据快照。 这些仪表板包括细分和许可证使用。 有关这些附加仪表板的详细信息，请从以下链接中进行选择：

* [细分仪表板](../../segmentation/ui/segment-dashboard.md)
* [许可证使用仪表板](../../landing/license-usage-dashboard.md)

## 后续步骤

通过遵循此文档，您现在应该能够找到用户档案仪表板并了解可用构件中显示的度量。 要进一步了解如何在Experience PlatformUI中使用[!DNL Profile]数据，请参阅[[!DNL Profile] UI指南](user-guide.md)。