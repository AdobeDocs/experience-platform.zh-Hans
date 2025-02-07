---
title: 使用UI将数据登陆区连接到Platform
description: 了解如何使用Platform用户界面创建数据登陆区源连接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: cdcce07a5adf08bf9d5e6a08d6bc965d37458a5d
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 使用UI将[!DNL Data Landing Zone]连接到平台

>[!IMPORTANT]
>
>此页面特定于Experience Platform中的[!DNL Data Landing Zone] *源*&#x200B;连接器。 有关连接到[!DNL Data Landing Zone] *目标*&#x200B;连接器的信息，请参阅[[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone]是一种安全的基于云的文件存储工具，可将文件导入Adobe Experience Platform。 数据会在七天后自动从[!DNL Data Landing Zone]中删除。

本教程提供了使用Platform用户界面创建[!DNL Data Landing Zone]源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 将您的文件从[!DNL Data Landing Zone]带到Platform

>[!IMPORTANT]
>
> 若要连接到源，您需要&#x200B;**[!UICONTROL 查看源]**&#x200B;和&#x200B;**[!UICONTROL 管理源]**&#x200B;访问控制权限。 阅读[访问控制概述](../../../../../access-control/home.md)或联系您的产品管理员以获取所需的权限。

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 云存储]类别下，选择[!DNL Data Landing Zone]，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![已选择具有数据登陆区域的源目录。](../../../../images/tutorials/create/dlz/catalog.png)

此时会显示[!UICONTROL 添加数据]步骤，为您提供一个界面来选择和预览要带到Platform的数据。

* 界面的左侧是一个文件夹浏览器，为您提供来自容器的文件列表，您可以将这些文件带到Platform。
* 界面的右侧部分允许您预览兼容文件中最多100行数据。

选择要带到Experience Platform中的文件，并留出一些时间，让正确的界面更新到预览屏幕中。

![源工作区的添加数据接口。](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform自动检测所选文件的属性信息，包括有关文件数据格式、指定的列分隔符和压缩类型的信息。

预览界面允许您检查文件的内容和结构。 默认情况下，预览界面显示所选文件夹中的第一个文件。

要预览其他文件，请选择要检查的文件名称旁边的预览图标。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作区的数据预览页面。](../../../../images/tutorials/create/dlz/file-detection.png)

有关如何为云存储源创建数据流的详细分步指南，请参阅有关[创建云存储数据流以将数据引入平台](../../dataflow/batch/cloud-storage.md)的教程。

## 检索您的[!DNL Data Landing Zone]凭据

[!DNL Data Landing Zone]是您的Adobe Experience Platform源许可证随附的源。 [!DNL Data Landing Zone]使用基于SAS URI和SAS令牌的身份验证。 您可以从[!UICONTROL 源目录]页面检索身份验证凭据。

要检索您的凭据，请选择&#x200B;**[!UICONTROL 数据登陆区]**&#x200B;卡，然后从显示的右边栏复制您的凭据。

![数据登陆区域的视图选项列表。](../../../../images/tutorials/create/dlz/view-credentials.png)

此时会出现一个弹出窗口，显示容器名称、SAS令牌、存储帐户名称、SAS URI和到期日期。

## 刷新您的[!DNL Data Landing Zone]凭据

您的[!DNL Data Landing Zone]凭据设置为90天后自动过期，并且您必须使用新凭据在过期后重新连接到[!DNL Data Landing Zone]。 您的Experience Platform数据流不受凭据过期的影响，您仍然可以使用新凭据继续使用新的和现有数据流。

有两种方法可刷新您的[!DNL Data Landing Zone]凭据：

>[!BEGINTABS]

>[!TAB 使用源卡]

若要从源目录页面刷新凭据，请选择[!DNL Data Landing Zone]信息卡中的省略号(**`...`**)，然后选择&#x200B;**[!UICONTROL 刷新凭据]**。

![使用源卡刷新凭据。](../../../../images/tutorials/create/dlz/refresh-with-card.png)

此时会出现一个弹出窗口，提示您进行确认，然后才能继续。 准备就绪后，选择&#x200B;**[!UICONTROL 刷新凭据]**。

![刷新凭据确认窗口。](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB 使用右边栏]

若要使用右边栏刷新凭据，请选择&#x200B;**[!UICONTROL 数据登陆区域]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 更多操作]**。 接下来，选择&#x200B;**[!UICONTROL 刷新凭据]**，然后使用显示的弹出窗口进行确认。

![使用右边栏刷新凭据。](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已访问您的[!DNL Data Landing Zone]容器并学会了检索和刷新凭据。 您现在可以继续有关[创建数据流以将数据从云存储带到Platform](../../dataflow/batch/cloud-storage.md)的下一个教程。
