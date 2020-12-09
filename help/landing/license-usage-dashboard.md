---
keywords: Experience Platform;user interface;UI;customization;license usage dashboard;dashboard;license usage;entitlement;consumption
title: 许可证使用仪表板
description: '本指南概述了Adobe Experience PlatformUI中提供的许可证使用仪表板。 '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# (Alpha)许可 [!UICONTROL 证使用] 仪表板 {#license-usage-dashboard}

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前位于alpha中，并且并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可以视图有关组织许可证使用情况的重要信息，这些信息在每日快照中捕获。 本指南概述了如何在UI中访问和使用许可证使用仪表板，并提供了有关仪表板中显示的可视化的更多信息。

有关平台UI的一般概述，请访问 [Experience PlatformUI指南](ui-guide.md)。

## 许可证使用仪表板数据

许可证使用仪表板显示组织与许可证相关的Experience Platform的快照。 仪表板中的数据与拍摄快照时在特定时间点的显示完全相同。 换言之，快照不是数据的近似值或样本，仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

## 浏览许可证使用仪表板

要导航到平台UI中的许可证使用仪表板，请在左边 **[!UICONTROL 栏中选择]** “许可证使用情况”。 此时将打开“概 **[!UICONTROL 述]** ”选项卡，显示仪表板。

![](images/license-usage-dashboard/dashboard-overview.png)

### 选择沙箱

要在仪表板中选择要视图的沙箱，请选择“生 [!UICONTROL 产] ”或“ [!UICONTROL 开发”]。 所选沙箱由沙箱名称旁的单选按钮指示。

>[!NOTE]
>
>沙箱的消耗报告对于同一类型的所有沙箱是累积的。 换言之，选择“ [!UICONTROL 生产] ”或 [!UICONTROL “开发] ”将分别报告所有生产或开发沙箱。

![](images/license-usage-dashboard/select-sandbox.png)

### 选择日期范围

选择沙箱后，您可以使用日期范围下拉列表选择要在仪表板中显示的时间段。 有三种可用选项： [!UICONTROL 最近]30 [!UICONTROL 天，最]近90天 [!UICONTROL ，最]近12个月。 默认情况下，最近30天处于选中状态。

![](images/license-usage-dashboard/select-date-range.png)

### 构件和指标

许可证使用仪表板由构件组成，构件显示只读指标，提供有关组织许可证使用情况的重要信息。 要进一步了解这些构件，请参阅本指南中的可用构件部分。

## 可用构件 {#available-widgets}

Experience Platform当前提供一个构件，您可以使用它直观地显示许可证使用情况，并且很快会发布更多构件。

### [!UICONTROL 可寻址受众] {#addressable-audiences}

可寻 **[!UICONTROL 址受众]** 构件在应用系统生成的合并策略以使用确定（专用）图形算法组合所有当前数据集后，测量用户档案存储中存在的受众总数。 用于计算此度量的合并策略由平台生成，无法编辑，也不能选择其他合并策略。

![](images/license-usage-dashboard/addressable-audiences.png)

## 其他仪表板

平台UI提供了更多仪表板，用于在Experience Platform内查看数据快照。 这些仪表板包括实时客户用户档案和细分。 有关这些仪表板的详细信息，请从以下链接中进行选择：

* [[!DNL Profile] 仪表板](../profile/ui/profile-dashboard.md)
* [细分仪表板](../segmentation/ui/segment-dashboard.md)

## 后续步骤

通过遵循此文档，您现在应该能够找到许可证使用仪表板并选择沙箱以进行视图。 您还应了解可用构件中显示的度量。 要进一步了解Experience PlatformUI，请参阅平 [台UI指南](ui-guide.md)。