---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标
title: 功能板自定义概述
description: 进一步了解自定义在Adobe Experience Platform功能板中显示的数据的方式。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 功能板自定义概述

Adobe Experience Platform中可用的配置文件、区段和目标功能板可以通过多种不同方式进行自定义。 本指南概述了可用的自定义设置，并提供了指向分步说明的链接，这些说明指导您如何个性化功能板中显示的小组件以及这些小组件的大小、形状和位置。

>[!NOTE]
>
>显示在 [!UICONTROL 许可证使用情况] 无法自定义功能板。 要了解有关此唯一功能板的更多信息，请阅读 [许可证使用仪表板文档](../guides/license-usage.md).

## 修改功能板

选择 **[!UICONTROL 修改功能板]** 通过用户档案、区段或目标功能板，您可以调整功能板中当前可见的小组件的大小、顺序和位置。 有关如何修改功能板中小组件外观的信息，请参阅 [修改功能板指南](modify.md).

## 小组件库

在Experience Platform中的小组件库中，您可以查看 [标准](#standard-widgets) 和 [自定义](#custom-widgets) 小组件。 在功能板（例如，用户档案功能板）中，您可以选择 **[!UICONTROL 修改功能板]** 以便显示 **[!UICONTROL 构件库]** 按钮。

![突出显示了“修改”功能板的“配置文件”功能板。](../images/customization/modify-dashboard.png)

选择 **[!UICONTROL 构件库]** 打开小组件库并查看所有可用的标准量度，或开始创建自定义小组件。

![突出显示了Widget库的用户档案仪表板。](../images/customization/widget-library-button.png)

### 标准小组件 {#standard-widgets}

标准小组件是指Adobe提供的用于功能板的小组件。 这些小组件是只读的，贵组织无法编辑。

在小组件库中， **[!UICONTROL 标准]** 选项卡包含由Adobe提供的所有可用的标准小组件。 您可以使用其中任何标准量度更新功能板。 要了解有关将标准小组件添加到功能板的更多信息，请参阅 [在功能板中使用标准小组件](standard-widgets.md).

### 自定义小组件 {#custom-widgets}

自定义小组件是指由您的组织成员创建和共享的小组件。 这些小组件通过 **[!UICONTROL 自定义]** ，并要求贵组织通过使用 [模式](#edit-schema)

有关创建您自己的小组件的完整步骤，请参阅 [功能板指南的自定义小组件](custom-widgets.md).

![突出显示了“标准”和“自定义”的小组件库工作区。](../images/customization/widget-library.png)

#### 编辑架构 {#edit-schema}

要创建 [自定义小组件](#custom-widgets) 对于功能板，您必须首先确定小组件所基于的“实时客户配置文件”属性。

有关编辑贵组织架构以创建自定义功能板小组件的分步说明，请访问 [编辑功能板架构](edit-schema.md).

## 后续步骤

阅读本文档后，您可以通过修改现有小组件的大小、形状和顺序、添加由Adobe提供的标准小组件，或创建自定义小组件并与您的组织共享，来开始自定义Experience Platform功能板。
