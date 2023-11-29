---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标
title: 仪表板自定义概述
description: 详细了解自定义在Adobe Experience Platform功能板中显示的数据的方法。
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 仪表板自定义概述

可以通过多种方式自定义Adobe Experience Platform中可用的配置文件、区段和目标功能板。 本指南概述了可用的自定义设置，其中包含指向分步说明的链接，该分步说明引导您完成如何个性化仪表板中显示哪些构件以及这些构件的大小、形状和位置。

>[!NOTE]
>
>对功能板所做的任何更新都是按组织和沙盒进行的。

## 修改仪表板

选择 **[!UICONTROL 修改仪表板]** 通过“用户档案”、“区段”或“目标”功能板，可调整当前显示在功能板中的小部件的大小、顺序和位置。 有关如何修改仪表板中构件外观的信息，请参阅 [修改仪表板指南](modify.md).

## 构件库

在Experience Platform中的构件库中，您可以查看所有 [标准](#standard-widgets) 和 [自定义](#custom-widgets) 您的组织可以使用构件。 从功能板（例如，用户档案功能板）中，您可以选择 **[!UICONTROL 修改仪表板]** 以显示 **[!UICONTROL 构件库]** 按钮。

![突出显示“修改”仪表板的“配置文件”仪表板。](../images/customization/modify-dashboard.png)

选择 **[!UICONTROL 构件库]** 打开构件库并查看所有可用的标准量度，或开始创建自定义构件。

![突出显示带有小组件库的配置文件仪表板。](../images/customization/widget-library-button.png)

### 标准构件 {#standard-widgets}

标准构件是指Adobe提供的用于功能板中的构件。 这些构件为只读构件，您的组织无法对其进行编辑。

在Widget库中， **[!UICONTROL 标准]** 选项卡包含Adobe提供的所有可用标准构件。 您可以使用任意这些标准量度更新您的仪表板。 要了解有关将标准构件添加到仪表板的更多信息，请参阅指南，了解 [在功能板中使用标准构件](standard-widgets.md).

### 自定义构件 {#custom-widgets}

自定义构件是指由组织成员创建和共享的构件。 这些构件是通过 **[!UICONTROL 自定义]** 选项卡中，并要求您的组织通过使用 [架构](#edit-schema)

有关创建您自己的构件的完整步骤，请参阅 [仪表板自定义构件指南](custom-widgets.md).

![突出显示“标准”和“自定义”的小组件库工作区。](../images/customization/widget-library.png)

#### 编辑架构 {#edit-schema}

为了创建 [自定义构件](#custom-widgets) 对于仪表板，您必须首先确定构件所基于的Real-time Customer Profile属性。

有关编辑您组织的架构以创建自定义仪表板小部件的分步说明，请访问指南 [编辑您的仪表板架构](edit-schema.md).

## 后续步骤

阅读本文档后，您可以通过修改现有构件的大小、形状和顺序、添加由Adobe提供的标准构件或者创建自定义构件并与您的Experience Platform共享来开始自定义组织仪表板。
