---
keywords: Experience Platform；配置文件；区段；区段；分段；用户界面；UI；自定义；区段功能板；功能板
title: 区段功能板
description: 'Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关您的组织已创建区段的重要信息。 '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---

# 区段功能板{#segment-dashboard}

Adobe Experience Platform用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关区段的重要信息，这些信息是在每日快照期间捕获的。 本指南概述了如何在UI中访问和使用区段功能板，并提供了有关功能板中显示的可视化的更多信息。

有关Platform用户界面中所有Adobe Experience Platform Segmentation Service功能的概述，请访问[Segmentation Service UI指南](../../segmentation/ui/overview.md)。

## 区段功能板数据

区段功能板显示贵组织在“配置文件”存储(在Experience Platform中)中拥有的属性（记录）数据的快照。 快照不包含任何事件（时间系列）数据。

快照中的属性数据完全显示快照拍摄时在特定时间点显示的数据。 换句话说，快照不是数据的近似值或样本，而且区段仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新，在拍摄下一个快照之前不会反映在功能板中。

## 浏览区段功能板

要导航到Platform UI中的区段功能板，请选择左边栏中的&#x200B;**[!UICONTROL 区段]**，然后选择&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡以显示功能板。

![](../images/segments/dashboard-overview.png)

### 修改[!UICONTROL 区段]功能板

通过选择&#x200B;**[!UICONTROL 修改功能板]**，可以修改[!UICONTROL 区段]功能板的外观。 这样，您就可以在功能板中移动、添加和删除小组件，以及访问[!UICONTROL 小组件库]，以探索可用的小组件并为贵组织创建自定义小组件。

有关更多信息，请参阅[修改功能板](../modify.md)和[小组件库](../widget-library.md)文档。

## 选择区段

功能板会自动选择要显示的区段，但您可以使用下拉菜单或区段选择器更改区段。

要选择其他区段，请选择区段名称旁边的下拉菜单，或使用区段选择器打开区段选择对话框。

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## 小组件和量度

区段功能板由小组件组成，这些小组件是只读量度，提供有关您选定区段的重要信息。

小组件上的“上次更新”日期和时间，会显示拍摄数据的最后快照的时间。 快照的日期和时间以UTC格式提供；它不在单个用户或IMS组织的时区中。

![](../images/segments/widget-timestamp.png)

## 可用小组件

Experience Platform提供了多个小组件，您可以使用这些小组件来显示与区段相关的不同量度。 选择下面小组件的名称，以了解更多信息：

* [[!UICONTROL 受众大小]](#audience-size)
* [[!UICONTROL 受众大小趋势]](#audience-size-trend)
* [[!UICONTROL 身份重叠]](#identity-overlap)
* [[!UICONTROL 按身份划分的用户档案]](#profiles-by-identity)

### [!UICONTROL 受众大小] {#audience-size}

**[!UICONTROL 受众大小]**&#x200B;小组件显示拍摄快照时选定区段内合并的配置文件总数。 此数字是将区段合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为区段中的每个人形成一个配置文件。

有关片段和合并配置文件的更多信息，请首先阅读[实时客户配置文件概述](../../profile/home.md)。

![](../images/segments/audience-size.png)

### [!UICONTROL 受众大小趋势] {#audience-size-trend}

**[!UICONTROL 受众大小趋势]**&#x200B;小组件提供有关在每日快照期间、最近30天、90天或12个月捕获的区段中配置文件总数的信息。 此小组件显示随着新用户档案符合区段资格或退出区段，区段大小可能随时间而发生的变化。

要了解有关区段评估以及用户档案如何确定和退出区段的更多信息，请参阅[Segmentation Service文档](../../segmentation/home.md)。

![](../images/segments/audience-size-trend.png)

### [!UICONTROL 身份重叠] {#identity-overlap}

**[!UICONTROL 身份重叠]**&#x200B;小组件会显示维恩图或设置图，其中显示了包含多个身份的区段中配置文件的重叠。

使用小组件上的下拉菜单选择要比较的身份后，圆圈会显示每个身份的相对大小，其中包含两个命名空间的用户档案数量由圈子之间重叠的大小表示。

如果客户在多个渠道上与您的品牌进行交互，则多个身份将与该个别客户关联，因此，您的组织可能具有多个包含多个身份片段的用户档案。

要了解有关身份的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/segments/identity-overlap.png)

### [!UICONTROL 按身份划分的用户档案] {#profiles-by-identity}

**[!UICONTROL 按身份划分的配置文件]**&#x200B;小组件可显示选定区段中所有合并配置文件的身份划分。 按身份划分的用户档案总数可能大于区段中的用户档案总数，因为一个用户档案可能具有多个与其关联的身份。 换言之，将每个身份显示的值相加，可能总计会大于区段中的受众总大小，因为如果客户在多个渠道上与您的品牌进行交互，则多个身份可能会与该个别客户关联。

要了解有关身份的更多信息，请访问[Adobe Experience Platform Identity Service文档](../../identity-service/home.md)。

![](../images/segments/profiles-by-identity.png)

## 后续步骤

通过遵循本文档，您现在应该能够找到区段仪表板，并选择要查看的区段。 您还应了解可用小组件中显示的量度。 要了解有关在Experience PlatformUI中使用区段的更多信息，请参阅[Segmentation Service UI指南](../../segmentation/ui/overview.md)。
