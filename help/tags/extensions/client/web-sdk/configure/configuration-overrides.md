---
title: 数据流配置覆盖设置
description: 在满足某些条件时修改配置设置。
exl-id: 68227148-3d74-4807-836c-14acd8a9c1dc
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 3%

---

# 数据流配置覆盖设置 {#config-overrides}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_overrides"
>title="数据流配置覆盖"
>abstract="有条件地触发不同的数据流行为，而无需单独的数据流。 在此部分中为环境设置任何客户端数据流配置覆盖将覆盖该环境的任何服务器端动态数据流配置和规则。"

数据流覆盖允许您为数据流定义其他配置，这些配置通过Web SDK传递到Edge Network。 此功能可帮助您有条件地触发不同的数据流行为，而无需创建新数据流或修改现有设置。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Datastream configuration overrides]**&#x200B;部分。

数据流配置覆盖是一个两步过程：

1. 首先，当在数据流UI中[配置数据流](/help/datastreams/configure.md)时，必须定义数据流配置覆盖。 有关如何配置覆盖的说明，请参阅数据流文档中的[数据流配置覆盖](/help/datastreams/overrides.md)。
1. 在数据流UI中配置数据流覆盖后，可以配置标记扩展。

必须为每个环境配置数据流覆盖。 开发、暂存和生产环境都具有单独的覆盖。 您可以在任意所需环境之间复制覆盖设置：

![显示使用Web SDK标记扩展页的数据流配置覆盖的图像。](../assets/datastream-overrides.png)

默认情况下，数据流配置覆盖处于禁用状态。 默认情况下已选中&#x200B;**[!UICONTROL Match datastream configuration]**&#x200B;选项。

![显示数据流配置的Web SDK标记扩展用户界面将覆盖默认设置。](../assets/datastream-override-default.png)

要在标记扩展中启用数据流覆盖，请从下拉菜单中选择&#x200B;**[!UICONTROL Enabled]**。

![Web SDK标记扩展用户界面显示数据流配置覆盖“已启用”设置。](../assets/datastream-override-enabled.png)

启用数据流配置覆盖后，可以为下述每项服务配置覆盖。 这些数据流覆盖设置会覆盖所选环境的任何服务器端数据流配置和规则。

## Adobe Analytics

覆盖到Adobe Analytics服务的数据路由。

![显示Adobe Analytics数据流覆盖设置的Web SDK标记扩展UI图像。](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：启用或禁用到Adobe Analytics的数据路由。
* **[!UICONTROL Report suites]**： Adobe Analytics中目标报表包的ID。 该值必须是来自您的数据流配置的预配置覆盖报表包（或以逗号分隔的报表包列表）。 此设置将覆盖主报表包。
* **[!UICONTROL Add Report Suite]**：选择此选项可添加其他报表包。

## Adobe Audience Manager

覆盖到Adobe Audience Manager的数据路由。

![显示Adobe Audience Manager数据流覆盖设置的Web SDK标记扩展UI图像。](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：启用或禁用到Adobe Audience Manager的数据路由。
* **[!UICONTROL Third-party ID sync container]**： Audience Manager中目标第三方ID同步容器的ID。 该值必须是来自数据流配置的预配置辅助容器，并覆盖主容器。

## Adobe Experience Platform

覆盖到Adobe Experience Platform的数据路由。

![显示Adobe Experience Platform数据流覆盖设置的Web SDK标记扩展UI图像。](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：启用或禁用到Adobe Experience Platform的数据路由。
* **[!UICONTROL Event dataset]**： Adobe Experience Platform中目标事件数据集的ID。 该值必须是来自数据流配置的预配置辅助数据集。
* **[!UICONTROL Offer Decisioning]**：启用或禁用到[!DNL Offer Decisioning]服务的数据路由。
* **[!UICONTROL Edge Segmentation]**：启用或禁用到[!DNL Edge Segmentation]服务的数据路由。
* **[!UICONTROL Personalization Destinations]**：启用或禁用到个性化目标的数据路由。
* **[!UICONTROL Adobe Journey Optimizer]**：启用或禁用到[!DNL Adobe Journey Optimizer]的数据路由。

## Adobe服务器端事件转发

覆盖发送到Adobe服务器端事件转发服务的数据路由。

![Web SDK标记扩展UI图像显示Adobe服务器端事件转发数据流覆盖设置。](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：启用或禁用到Adobe服务器端事件转发服务的数据路由。

## Adobe Target {#target}

覆盖到Adobe Target的数据路由。

![显示Adobe Target数据流覆盖设置的Web SDK标记扩展UI图像。](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**：启用或禁用到Adobe Target的数据路由。
