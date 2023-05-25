---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况
title: 编辑架构以创建自定义功能板构件
description: 本指南提供有关选择属性和配置组织的架构以创建Adobe Experience Platform功能板的自定义小部件的分步说明。
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 编辑架构以创建自定义构件

要为Adobe Experience Platform功能板创建自定义构件，您必须首先确定构件所基于的实时客户配置文件属性。

本指南提供了通过选择属性以创建自定义仪表板构件来编辑组织架构的分步说明。

选择属性并配置架构后，您可以继续执行以下步骤 [为功能板创建自定义构件](custom-widgets.md).

>[!NOTE]
>
>必须向用户授予“管理标准功能板”权限，才能编辑架构。 有关授予功能板访问权限的步骤，请参阅 [仪表板权限指南](../permissions.md).

## 构件库 {#widget-library}

本指南需要访问 [!UICONTROL 构件库] 在Experience Platform内。 要详细了解构件库以及如何在UI中访问它，请从阅读 [构件库概述](widget-library.md).

## 编辑架构

在Widget库中， **[!UICONTROL 自定义]** 选项卡允许您创建构件并与组织中的其他用户共享这些构件，以自定义功能板的外观。

在创建自定义构件之前，必须选择Real-Time Customer Profile属性，以确保数据包含在每日快照中。

>[!IMPORTANT]
>
>您的组织最多可以选择20个属性。

如果您的组织尚未选择任何配置文件属性，请首先选择 **[!UICONTROL 配置]** 位于屏幕中心。

![突出显示了配置下构件库工作区的“自定义”选项卡。](../images/customization/configure-schema.png)

创建至少一个自定义属性后，选择 **[!UICONTROL 编辑架构]** 以查看所选属性并添加更多属性。

![突出显示了Edit架构的Widget库工作区的“自定义”选项卡。](../images/customization/edit-schema.png)

## 选择属性

要选择属性，请执行以下操作 **[!UICONTROL 选择合并架构字段]** 对话框，导航到合并架构中的属性（或使用搜索），然后选中该属性旁边的复选框。 选中该复选框还会将属性添加到 **[!UICONTROL 选定的属性]** 对话框右侧的列表。

>[!NOTE]
>
>要使某个属性在选择时可见，它必须是下列之一：字符串、日期、日期时间、布尔值、短整数、长整数、整数或字节。 不支持Map和Double数据类型，它们显示为灰色，因此无法选择它们。

选择要添加的属性后，选择 **[!UICONTROL 保存]** 以保存您的属性并返回到“自定义构件”选项卡。

>[!WARNING]
>刷新数据后，新选择的属性将在下一个每日快照后变为可用。

![用于选择具有属性的架构属性和保存突出显示的对话框。](../images/customization/select-attribute.png)

## 后续步骤

阅读本指南后，您可以导航到构件库并选择Real-Time Customer Profile属性来配置架构。 选择配置文件属性后，即可开始 [为功能板创建自定义构件](custom-widgets.md).
