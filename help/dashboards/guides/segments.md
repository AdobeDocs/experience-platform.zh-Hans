---
keywords: Experience Platform;用户档案；段；段；分段；用户界面；UI；自定义；段仪表板;仪表板
title: 细分仪表板
description: 'Adobe Experience Platform提供了一种仪表板，您可以通过它视图与您的组织创建的区段有关的重要信息。 '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# （测试版）区段仪表板{#segment-dashboard}

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一种仪表板，通过它可以视图有关区段的重要信息，这些信息在每日快照中捕获。 本指南概述了如何在UI中访问和使用区段仪表板，并提供有关仪表板中显示的可视化的更多信息。

有关平台用户界面中所有Adobe Experience Platform Segmentation Service功能的概述，请访问[分段服务UI指南](../../segmentation/ui/overview.md)。

## 细分仪表板数据

区段仪表板显示您的组织在Experience Platform中的用户档案存储中拥有的属性（记录）数据的快照。 快照不包括任何事件（时间系列）数据。

快照中的属性数据与拍摄快照时在特定时间点显示的数据完全相同。 换句话说，快照不是数据的近似值或样本，而且区段仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

## 浏览细分仪表板

要导航到平台UI中的区段仪表板，请在左边栏中选择&#x200B;**[!UICONTROL Segments]**，然后选择&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡以显示仪表板。

![](../images/segments/dashboard-overview.png)

### 选择区段

仪表板将自动选择要显示的区段，但您可以更改使用下拉菜单显示的区段。 要选择其他区段，请选择区段名称旁的下拉框，然后选择您要视图的区段。

>[!NOTE]
>
>下拉菜单显示了您的组织到目前为止创建的所有区段。 这可能意味着您需要滚动才能视图可用区段的完整列表。

![](../images/segments/change-segment.png)

### 构件和量度

区段仪表板由构件组成，构件是只读量度，提供有关选定区段的重要信息。 构件上的“上次更新”日期和时间会显示拍摄数据的最后快照的时间。

![](../images/segments/widget-timestamp.png)

## 可用构件

Experience Platform提供了多个构件，您可以使用这些构件来可视化与您的区段相关的不同量度。 选择下面的Widget名称以了解更多信息：

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

**[!UICONTROL Segment size]**&#x200B;构件显示拍摄快照时所选区段内的合并用户档案总数。 此数字是将区段合并策略应用于您的用户档案数据的结果，以便将用户档案片段合并到一起，为区段中的每个个人形成单个用户档案。

有关片段和合并用户档案的详细信息，请首先阅读[实时客户用户档案概述](../../profile/home.md)。

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

**[!UICONTROL Profiles added over time]**&#x200B;构件提供有关在过去30天内每日快照中捕获的区段中用户档案总数的信息。 此小部件显示随着新用户档案有资格或退出区段，区段大小在30天内可能已发生的变化。

要了解有关区段评估以及用户档案如何确定和退出区段的更多信息，请参阅[分段服务文档](../../segmentation/home.md)。

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]**&#x200B;构件显示选定区段中所有合并用户档案的命名空间细分。 按身份命名空间（Widget中[!UICONTROL ID namespace]）划分的用户档案总数可能高于区段中的用户档案总数，因为一个用户档案可能具有与其关联的多个命名空间。 换句话说，将每个命名空间显示的值加在一起可能会超过区段中的用户档案总数，因为如果客户在多个渠道上与您的品牌互动，则可能会与该个别客户关联多个命名空间。

要了解有关身份命名空间的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/segments/profiles-by-namespace.png)

## 后续步骤

通过遵循此文档，您现在应能够找到区段仪表板并选择要视图的区段。 您还应了解可用构件中显示的量度。 要了解有关在Experience Platform UI中使用区段的更多信息，请参阅[分段服务UI指南](../../segmentation/ui/overview.md)。
