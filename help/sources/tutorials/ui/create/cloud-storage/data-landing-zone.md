---
keywords: Experience Platform；主页；热门主题；数据登陆区；数据登陆区
solution: Experience Platform
title: 使用UI将数据登陆区连接到平台
topic-legacy: overview
type: Tutorial
description: 了解如何使用平台用户界面创建数据登陆区源连接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 使用UI将[!DNL Data Landing Zone]连接到平台

[!DNL Data Landing Zone] 是一个基于云的数据存储设施，可用于配置有Adobe Experience Platform的临时文件存储。[!DNL Data Landing Zone] 仅用于数据进出平台的情况。7天后，数据将自动从[!DNL Data Landing Zone]中删除。

本教程提供了使用Platform用户界面创建[!DNL Data Landing Zone]源连接的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 将文件从[!DNL Data Landing Zone]迁移到平台

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了您可以使用创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在[!UICONTROL 云存储]类别下，选择[!DNL Data Landing Zone]，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/dlz/catalog.png)

此时将显示[!UICONTROL 添加数据]步骤，为您提供一个界面来选择和预览要引入平台的数据。

![添加数据](../../../../images/tutorials/create/dlz/add-data.png)

有关如何为云存储源创建数据流的详细分步指南，请参阅[创建云存储数据流以将数据导入Platform](../../dataflow/batch/cloud-storage.md)的教程。

## 检索并刷新[!DNL Data Landing Zone]凭据

[!DNL Data Landing Zone] 是您的Adobe Experience Platform Sources许可证附带的现成源。[!DNL Data Landing Zone] 使用基于SAS URI和SAS令牌的身份验证。您可以从[!UICONTROL Sources目录]页面中检索和刷新您的身份验证凭据。

在[!UICONTROL 源目录]的[!UICONTROL 云存储]类别下，选择省略号(**...**)。 ****&#x200B;从出现的下拉菜单中，选择&#x200B;**[!UICONTROL 查看凭据]**。

![选项](../../../../images/tutorials/create/dlz/options.png)

出现一个弹出窗口，其中显示您的容器名称、SAS令牌、存储帐户名称和SAS URI。

选择&#x200B;**[!UICONTROL 刷新凭据]**&#x200B;并允许处理更新凭据几秒钟。

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## 后续步骤

通过阅读本教程，您已经访问了[!DNL Data Landing Zone]容器，并学习了如何检索和刷新凭据。 现在，您可以继续下一个关于[创建数据流以将数据从云存储导入Platform](../../dataflow/batch/cloud-storage.md)的教程。
