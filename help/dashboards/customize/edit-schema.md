---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况
title: 编辑架构以创建自定义功能板构件
description: 本指南提供了有关选择属性和配置组织的架构以创建Adobe Experience Platform功能板的自定义小部件的分步说明。
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 编辑架构以创建自定义构件

要为Adobe Experience Platform功能板创建自定义构件，您必须首先确定构件所基于的实时客户配置文件属性。

本指南通过选择属性以创建自定义仪表板构件来提供有关编辑组织架构的分步说明。

选择属性并配置架构后，您可以继续执行[为功能板创建自定义小组件](custom-widgets.md)的步骤。

>[!NOTE]
>
>必须向用户授予“管理标准功能板”权限才能编辑架构。 有关授予仪表板访问权限的步骤，请参阅[仪表板权限指南](../permissions.md)。

## 构件库 {#widget-library}

本指南需要访问Experience Platform中的[!UICONTROL 构件库]。 要了解有关构件库以及如何在UI中访问它的更多信息，请从阅读[构件库概述](widget-library.md)开始。

## 编辑架构

在小组件库中，**[!UICONTROL 自定义]**&#x200B;选项卡允许您创建小组件并与组织中的其他用户共享这些小组件，以便自定义仪表板的外观。

在创建自定义构件之前，必须选择“实时客户配置文件”属性，以确保每日快照中包含数据。

>[!IMPORTANT]
>
>您的组织最多可以选择20个属性。

如果您的组织尚未选择任何配置文件属性，请从选择屏幕中心的&#x200B;**[!UICONTROL 配置]**&#x200B;开始。

![突出显示了“配置”的Widget库工作区的“自定义”选项卡。](../images/customization/configure-schema.png)

创建至少一个自定义属性后，选择&#x200B;**[!UICONTROL 编辑架构]**&#x200B;以查看所选属性并添加更多属性。

![突出显示“编辑”架构的构件库工作区的“自定义”选项卡。](../images/customization/edit-schema.png)

## 选择属性

要在&#x200B;**[!UICONTROL 选择合并架构字段]**&#x200B;对话框中选择属性，请导航到合并架构中的属性（或使用搜索），然后选中该属性旁边的复选框。 选中该复选框还会将该属性添加到对话框右侧的&#x200B;**[!UICONTROL 选定属性]**&#x200B;列表中。

>[!NOTE]
>
>要使某个属性在选择时可见，该属性必须是下列值之一： String、Date、Date-Time、Boolean、Short、Long、Integer或Byte。 不支持映射和双精度数据类型，并且这两种数据类型呈灰显状态，因此无法选择它们。

选择要添加的属性后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存属性并返回自定义构件选项卡。

>[!WARNING]
>刷新数据后，新选择的属性将在下次每日快照后变为可用。

![用于选择具有突出显示的属性和保存的架构属性的对话框。](../images/customization/select-attribute.png)

## 后续步骤

阅读本指南后，您可以导航到构件库，并选择Real-Time Customer Profile属性来配置架构。 选择配置文件属性后，您就可以开始[为功能板创建自定义小组件](custom-widgets.md)。
