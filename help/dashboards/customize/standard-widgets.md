---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况
title: 标准功能板小组件
description: 本指南提供了将标准构件添加到Adobe Experience Platform功能板的分步说明。
exl-id: 37353e73-b207-444a-b2b5-a20a3628086b
source-git-commit: d9ce17bbe17df175db30d283387d8fa569b97dee
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 将标准构件添加到仪表板

在Adobe Experience Platform中，您可以使用多个功能板查看您的组织数据并与之交互。 您还可以通过向仪表板视图添加新构件来更新某些仪表板。 Adobe提供了一系列标准构件，您可以选择将其添加到功能板中。

此 [!UICONTROL 配置文件]， [!UICONTROL 受众]、和 [!UICONTROL 目标] 在创建新的平台实例时，每个功能板都具有默认的小组件加载。 本指南提供了添加标准构件以自定义 [!UICONTROL 配置文件]， [!UICONTROL 受众]、和 [!UICONTROL 目标] Platform UI中的功能板。

>[!NOTE]
>
>截至2023年7月26日， [!UICONTROL 配置文件]， [!UICONTROL 受众]、和 [!UICONTROL 目标] 对于所有在过去六个月中未修改其视图的用户，概述功能板已重置为新的默认构件加载。
>请参阅 [配置文件](../guides/profiles.md#default-widgets)， [受众](../guides/audiences.md#default-widgets)、和 [目标](../guides/destinations.md#default-widgets) “默认构件”部分，了解有关哪些构件包含在默认构件加载中的详细信息。

要了解有关自定义小组件的更多信息，请参阅以下内容的指南 [创建自定义构件](custom-widgets.md).

>[!NOTE]
>
>中显示的构件 [!UICONTROL 许可证使用情况] 无法自定义仪表板。 要了解有关此独特功能板的更多信息，请参阅 [许可证使用情况仪表板文档](../guides/license-usage.md).

## 构件库 {#widget-library}

本指南需要访问 [!UICONTROL 构件库] 在Experience Platform内。 要详细了解构件库以及如何在UI中访问它，请从阅读 [构件库概述](widget-library.md).

## 标准构件快速入门 {#standard-widgets}

在Widget库中， **[!UICONTROL 标准]** 选项卡包含由Adobe创建的构件，这些构件根据可用的功能板划分为不同的类别。

所选类别与您输入构件库的仪表板匹配。 换言之，如果您从 [!UICONTROL 配置文件] 仪表板， [!UICONTROL 配置文件] 类别处于选中状态，其他类别将显示为灰色。

将显示选定类别的标准构件。 每个小组件都显示为卡片，提供量度的标题、描述和可视化示例。

>[!NOTE]
>
>构件只能添加到与所选类别匹配的仪表板。 例如，仅来自 [!UICONTROL 配置文件] 类别可添加到 [!UICONTROL 配置文件] 仪表板。

![突出显示了“标准”选项卡和可用类别的小组件库工作区。](../images/customization/standard-widgets.png)

## 将标准构件添加到仪表板

要选择要添加到功能板的标准构件，请突出显示构件并选中复选框。 选择至少一个构件后， **[!UICONTROL 添加构件]** 按钮将变为可用。

>[!NOTE]
>
>构件库右上角的计数器显示所选构件的总数。

选择 **[!UICONTROL 添加构件]** 以将所选构件添加到您的仪表板。

![已选择小组件且突出显示添加小组件和取消的小组件库工作区。](../images/customization/add-widget.png)

## 后续步骤

阅读本文档后，您便能够访问构件库，并使用它向功能板添加标准构件。 要修改显示在仪表板中的小部件的大小和位置，请参阅 [修改功能板指南](modify.md).
