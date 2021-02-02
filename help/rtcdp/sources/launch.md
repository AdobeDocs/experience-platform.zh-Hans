---
keywords: 启动Web标记；Web标记启动；网站标记；Web标记；启动；启动
title: 教程使用Adobe启动实施网站标签
seo-title: 通过Adobe启动实施网站标记
description: 使用Adobe启动在Adobe Experience Platform实施网站标记
seo-description: 使用Adobe启动在Adobe Experience Platform实施网站标记
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 8%

---


# 教程：通过Adobe启动实施网站标记

本教程介绍如何使用Adobe启动实施网站标签以将数据发送到Adobe Experience Platform。

## 先决条件

* 必需的模式和数据集在[!DNL Platform]中创建。
* 必要的配置已部署在Experience Edge中，且具有匹配的配置ID和Edge域。
* 公司CMS已配置为在每个页面上传送一个JavaScript对象，其中包含您需要发送到平台的数据。

## 步骤

本教程包含以下步骤：

1. 安装Adobe Experience Platform[!DNL Web SDK]扩展。
1. 创建规则，告诉[!DNL Launch]要发送哪些数据。
1. 捆绑库中的扩展和规则。

## 安装Adobe Experience Platform[!DNL Web SDK]扩展

首先，安装Adobe Experience Platform[!DNL Web SDK]扩展。

1. 在[!DNL Launch]中，打开&#x200B;**[!UICONTROL 扩展]**&#x200B;选项卡。

   ![image](assets/launch-overview.png)

1. 从启动扩展目录中选择Adobe Experience PlatformWeb SDK扩展
此时将打开配置屏幕。

   ![图像](assets/launch-extension-install.png)

   有关详细信息，请参阅[!DNL Launch]文档中的[扩展](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)。

1. 配置扩展.

   您现在需要的唯一设置是：

   * **配置ID:** 指定您从Adobe代表处获得的配置ID。
   * **边缘域：** 指定您从Adobe代表处获得的边缘域。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;并继续执行下一步。

## 创建规则，告诉[!DNL Launch]要发送哪些数据

接下来，创建一条规则，让[!DNL Launch]知道要向Adobe Experience Platform发送哪些数据以及何时发送这些数据。

1. 在&#x200B;**[!UICONTROL Rules]**&#x200B;选项卡下，配置一个事件，当[!DNL Launch]库加载时，它将在网站的每个新页面上触发。

   ![图像](assets/launch-make-a-rule.png)

1. 添加操作.

   要配置操作，请告诉[!DNL Launch]在何处查找数据层。 数据层是页面上存在的一个JavaScript对象，它通过呈现网页的同一CMS提供。 提供数据对象的JavaScript路径。

   ![图像](assets/launch-add-aep-action.png)

   您发送的模式对象必须是有效的XDM，它将对连接到您的配置ID的数据集所使用的数据进行验证。

1. 选择&#x200B;**[!UICONTROL 保留更改]**。

有关详细信息，请参阅[!DNL Launch]文档中的[规则](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html)。

## 捆绑库中的扩展和规则

接下来，[将扩展](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html)和新规则捆绑到库中，并在开发环境中测试这些更改。

![图像](assets/launch-add-changes-to-library.png)

完成测试后，通过工作流提升库，以便将其部署到生产站点。 数据现在从每个用户流向Adobe Experience Platform。

![图像](assets/launch-promote-library.png)

有关详细信息，请参阅[!DNL Launch]文档中的[库](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/publish/libraries.html)。