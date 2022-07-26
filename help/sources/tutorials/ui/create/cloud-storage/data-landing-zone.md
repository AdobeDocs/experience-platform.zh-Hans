---
keywords: Experience Platform；主页；热门主题；数据登陆区；数据登陆区
title: 使用UI将数据登陆区连接到平台
description: 了解如何使用平台用户界面创建数据登陆区源连接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: fb16ea940ef394a15dd24fe703239b4487fafb18
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# 连接 [!DNL Data Landing Zone] 到使用UI的平台

[!DNL Data Landing Zone] 是一个安全、基于云的文件存储工具，用于将文件导入Adobe Experience Platform。 数据会自动从 [!DNL Data Landing Zone] 七天后。

本教程提供了创建 [!DNL Data Landing Zone] 源连接。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 从 [!DNL Data Landing Zone] 到平台

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 [!DNL Data Landing Zone] 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/dlz/catalog.png)

的 [!UICONTROL 添加数据] 步骤，为您提供一个界面来选择和预览要引入平台的数据。

* 界面的左部是文件夹浏览器，为您提供了容器中的文件列表，然后您可以将这些文件调到Platform。
* 界面的右侧部分允许您从兼容的文件中预览多达100行数据。

选择要引入平台的文件，并在适当的时间将正确的界面更新到预览屏幕中。

![添加数据](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform会自动检测所选文件的属性信息，包括有关文件数据格式、指定列分隔符和压缩类型的信息。

预览界面允许您检查文件的内容和结构。 默认情况下，预览界面会显示所选文件夹中的第一个文件。

要预览其他文件，请选择要检查的文件名称旁边的预览图标。

完成后，选择 **[!UICONTROL 下一个]**.

![文件检测](../../../../images/tutorials/create/dlz/file-detection.png)

有关如何为云存储源创建数据流的详细分步指南，请参阅 [创建云存储数据流以将数据导入平台](../../dataflow/batch/cloud-storage.md).

## 检索并刷新 [!DNL Data Landing Zone] 凭据

[!DNL Data Landing Zone] 是您的Adobe Experience Platform Sources许可证附带的现成源。 [!DNL Data Landing Zone] 使用基于SAS URI和SAS令牌的身份验证。 您可以从 [!UICONTROL 源目录] 页面。

在 [!UICONTROL 源目录]，在 [!UICONTROL 云存储] 类别中，选择省略号(**...**) **[!UICONTROL 数据登陆区]** 卡。 从显示的下拉菜单中，选择 **[!UICONTROL 查看凭据]**.

![选项](../../../../images/tutorials/create/dlz/options.png)

出现一个弹出窗口，其中显示您的容器名称、SAS令牌、存储帐户名称和SAS URI。

选择 **[!UICONTROL 刷新凭据]** 并且需要几秒钟才能处理更新的凭据。

>[!TIP]
>
>您的 [!DNL Data Landing Zone] 凭据会设置为在90天后自动过期，您必须使用新凭据重新连接到 [!DNL Data Landing Zone] 过期之后。 Platform中的数据流不会受到凭据过期的影响，您仍然可以使用新凭据继续使用新数据流和现有数据流。

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## 后续步骤

通过阅读本教程，您可以访问 [!DNL Data Landing Zone] 容器，并学习了如何检索和刷新您的凭据。 您现在可以继续阅读下一个教程： [创建数据流以将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md).
