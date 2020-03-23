---
title: 教程使用Adobe Launch实施网站标记
seo-title: 使用Adobe Launch实施网站标记
description: 使用Adobe Launch在Adobe Experience Platform中实施网站标记
seo-description: 使用Adobe Launch在Adobe Experience Platform中实施网站标记
translation-type: tm+mt
source-git-commit: b8eda33a88b81dff5f3b45a131a5585a062519c2

---


# 教程：使用Adobe Launch实施网站标记

本教程介绍如何实施网站标签，以使用Adobe Launch将数据发送到Adobe Experience Platform。

## 先决条件

* 必需的架构和数据集在平台中创建。
* 必要的配置已部署在Experience Edge中，且具有匹配的配置ID和Edge域。
* 公司CMS已配置为在每个页面上传送包含您需要发送到平台的数据的JavaScript对象。

## 步骤

本教程包含以下步骤：

1. 安装Adobe Experience Platform Web SDK扩展。
1. 创建规则以告知启动要发送的数据。
1. 捆绑库中的扩展和规则。

## 安装Adobe Experience Platform Web SDK扩展

首先，安装Adobe Experience Platform Web SDK扩展。

1. 在 Launch 中，打开 **[!UICONTROL Extensions]** 选项卡。

   ![image](assets/launch-overview.png)

1. 从“启动扩展目录”中选择Adobe Experience Platform Web SDK扩展。此时将打开配置屏幕。

   ![image](assets/launch-extension-install.png)

   有关详细信息，请参 [阅Launch文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) 中的扩展。

1. 配置扩展.

   您现在需要的唯一设置是：

   * **配置ID:** 指定您从Adobe代表处获得的配置ID。
   * **边缘域：** 指定您从Adobe代表处获得的边缘域。

1. 单 **[!UICONTROL Save]** 击并继续下一步。

## 创建规则以告知Launch要发送哪些数据

接下来，创建一个规则，让Launch知道您要将哪些数据发送到Adobe Experience Platform以及何时发送。

1. 在选项 **[!UICONTROL Rules]** 卡下，配置一个事件，该事件将在启动库加载时在网站的每个新页面上触发。

   ![image](assets/launch-make-a-rule.png)

1. 添加操作.

   要配置操作，请告诉启动项在何处查找数据层。 数据层是页面上存在的一个JavaScript对象，该对象是从呈现网页的相同CMS传送的。 提供数据对象的JavaScript路径。

   ![image](assets/launch-add-aep-action.png)

   您发送的数据对象必须是有效的XDM，它将通过对与您的配置ID连接的数据集所使用的架构的验证。

1. 单击 **[!UICONTROL Keep Changes]**。

有关详细信息，请参阅 [启动文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) 中的规则。

## 捆绑库中的扩展和规则

然后， [将扩展和新规则捆绑到库中](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) ，并在开发环境中测试这些更改。

![image](assets/launch-add-changes-to-library.png)

完成测试后，通过工作流提升库，以便将其部署到生产站点。 现在，数据从每个用户流向Adobe Experience Platform。

![image](assets/launch-promote-library.png)

有关详细信息，请参 [阅Launch文档](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) 中的库。