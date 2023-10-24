---
keywords: Experience Platform；主页；热门主题；数据登陆区；数据登陆区
title: 使用UI将数据登陆区连接到Platform
description: 了解如何使用Platform用户界面创建数据登陆区源连接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 9cffd508c1bff7ce133f84ca686c414e997343b8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# 连接 [!DNL Data Landing Zone] 到Platform，使用UI

>[!IMPORTANT]
>
>此页面特定于 [!DNL Data Landing Zone] *源* Experience Platform中的连接器。 有关连接到 [!DNL Data Landing Zone] *目标* 连接器，请参阅 [[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是一个安全、基于云的文件存储工具，可将文件导入Adobe Experience Platform。 数据将自动从 [!DNL Data Landing Zone] 七天之后。

本教程提供了用于创建 [!DNL Data Landing Zone] 源连接，使用Platform用户界面。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 从以下位置导入文件 [!DNL Data Landing Zone] 目标平台

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕中显示多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 [!DNL Data Landing Zone] 然后选择 **[!UICONTROL 添加数据]**.

![已选择数据登陆区域的源目录。](../../../../images/tutorials/create/dlz/catalog.png)

此 [!UICONTROL 添加数据] 此时会显示步骤，为您提供一个界面来选择和预览要带到Platform的数据。

* 界面的左侧是一个文件夹浏览器，为您提供来自容器的文件列表，您可以将这些文件带到Platform。
* 界面的右侧部分允许您预览兼容文件中最多100行数据。

选择要带到Experience Platform中的文件，并留出一些时间，让正确的界面更新到预览屏幕中。

![源工作区的添加数据接口。](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform自动检测所选文件的属性信息，包括有关文件数据格式、指定的列分隔符和压缩类型的信息。

预览界面允许您检查文件的内容和结构。 默认情况下，预览界面显示所选文件夹中的第一个文件。

要预览其他文件，请选择要检查的文件名称旁边的预览图标。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作区的数据预览页面。](../../../../images/tutorials/create/dlz/file-detection.png)

有关如何为云存储源创建数据流的分步指南，请参阅上的教程 [创建云存储数据流以将数据引入平台](../../dataflow/batch/cloud-storage.md).

## 检索并刷新 [!DNL Data Landing Zone] 凭据

[!DNL Data Landing Zone] 是随Adobe Experience Platform Sources许可证提供的开箱即用源。 [!DNL Data Landing Zone] 使用基于SAS URI和SAS令牌的身份验证。 您可以从以下位置检索和刷新您的身份验证凭据： [!UICONTROL 源目录] 页面。

在 [!UICONTROL 源目录]，位于 [!UICONTROL 云存储] 类别中，选择省略号(**...**)中的 **[!UICONTROL 数据登陆区]** 卡片。 从出现的下拉菜单中，选择 **[!UICONTROL 查看凭据]**.

![数据登陆区域的视图选项列表。](../../../../images/tutorials/create/dlz/options.png)

此时会出现一个弹出窗口，显示容器名称、SAS令牌、存储帐户名称、SAS URI和到期日期。

选择 **[!UICONTROL 刷新凭据]** 留出几秒时间，以便处理您更新的凭据。

>[!TIP]
>
>您的 [!DNL Data Landing Zone] 凭据设置为在90天后自动过期，您必须使用新凭据重新连接到 [!DNL Data Landing Zone] 过期后。 您的Platform中的数据流不受凭据过期的影响，并且您仍然可以使用新凭据继续使用新的和现有的数据流。

![与给定数据登陆区帐户关联的凭据。](../../../../images/tutorials/create/dlz/view-credentials.png)

## 后续步骤

按照本教程，您已访问 [!DNL Data Landing Zone] 并了解如何检索和刷新您的凭据。 现在，您可以继续阅读上的下一个教程 [创建数据流以将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md).
