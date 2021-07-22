---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标
title: 功能板自定义概述
description: 进一步了解自定义在Adobe Experience Platform功能板中显示的数据的方式。
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 功能板自定义概述

Adobe Experience Platform中可用的配置文件、区段和目标功能板可以通过多种不同方式进行自定义。 本指南概述了可用的自定义设置，并提供了指向分步说明的链接，这些说明指导您如何个性化功能板中显示的小组件以及这些小组件的大小、形状和位置。

>[!NOTE]
>
>无法自定义[!UICONTROL 许可证使用情况]功能板中显示的小组件。 要了解有关此唯一功能板的更多信息，请阅读[许可证使用功能板文档](../guides/license-usage.md)。

## 修改功能板

从配置文件、区段或目标功能板中选择&#x200B;**[!UICONTROL 修改功能板]**，即可调整功能板中当前可见的小组件的大小、顺序和位置。 有关如何修改功能板中小组件外观的信息，请参阅[修改功能板指南](modify.md)。

## 小组件库

在Experience Platform中的小组件库中，您可以查看组织可用的所有[标准](#standard-widgets)和[自定义](#custom-widgets)小组件。 在功能板（例如，用户档案功能板）中，您可以选择&#x200B;**[!UICONTROL 修改功能板]**&#x200B;以显示&#x200B;**[!UICONTROL Widget库]**&#x200B;按钮。

![](../images/customization/modify-dashboard.png)

选择&#x200B;**[!UICONTROL 小组件库]**&#x200B;以打开小组件库并查看所有可用的标准量度，或开始创建自定义小组件。

![](../images/customization/widget-library-button.png)

### 标准小组件 {#standard-widgets}

标准小组件是指Adobe提供的用于功能板的小组件。 这些小组件是只读的，贵组织无法编辑。

在小组件库中，**[!UICONTROL Standard]**&#x200B;选项卡包含由Adobe提供的所有可用的标准小组件。 您可以使用其中任何标准量度更新功能板。 要了解有关将标准小组件添加到功能板的更多信息，请参阅[使用功能板](standard-widgets.md)中的标准小组件指南。

### 自定义小组件 {#custom-widgets}

自定义小组件是指由您的组织成员创建和共享的小组件。 这些小组件是通过小组件库的&#x200B;**[!UICONTROL Custom]**&#x200B;选项卡创建的，并且需要贵组织通过使用[架构](#edit-schema)来指定可用的量度

有关创建您自己的小组件的完整步骤，请参阅功能板指南的[自定义小组件](custom-widgets.md)。

![](../images/customization/widget-library.png)

#### 编辑架构 {#edit-schema}

要为功能板创建[自定义小组件](#custom-widgets)，您必须首先确定该小组件所基于的“实时客户配置文件”属性。

有关编辑贵组织架构以创建自定义功能板小部件的分步说明，请访问[编辑功能板架构](edit-schema.md)的指南。

## 后续步骤

阅读本文档后，您可以通过修改现有小组件的大小、形状和顺序、添加由Adobe提供的标准小组件，或创建自定义小组件并与您的组织共享，来开始自定义Experience Platform功能板。
