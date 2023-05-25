---
title: 实施Adobe Experience Platform Assurance扩展
description: 本指南介绍了如何实施和安装Adobe Experience Platform Assurance扩展。
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# 实施Adobe Experience Platform Assurance扩展

本教程介绍了如何在Mobile SDK中安装和实施Platform Assurance扩展。 有关将Assurance扩展添加到应用程序的说明，请阅读 [Adobe Experience Platform Assurance扩展概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## 快速入门

要安装并实施Assurance扩展，您需要访问以下服务：

- 此 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## 创建移动 属性

>[!NOTE]
>
>如果您已经拥有移动资产，则可以继续下一步骤。

在数据收集UI中，选择 **[!UICONTROL 标记]**. 此时将显示一个移动和Web资产列表，其中包含有关属于您组织的资产的信息。 选择 **[!UICONTROL 新建属性]** 以创建新资产。

![新资产按钮突出显示，显示您选择用来创建新资产的内容](./images/implement-assurance/create-new-property.png)

此 **[!UICONTROL 创建属性]** 页面。 输入新资产的名称并选择 **[!UICONTROL 移动设备]** 作为您的平台。 插入详细信息后，选择 **[!UICONTROL 保存]** 以创建移动资产。

>[!NOTE]
>
>移动资产的 **[!UICONTROL 隐私]** 设置do **非** 影响Assurance的数据收集。

![此时将显示“创建属性”页。 您可以在此处插入有关移动资产的信息。](./images/implement-assurance/create-property.png)

## 安装Assurance扩展

选择要在其中安装Assurance扩展的移动资产。

![此时会显示“标记属性”页面，其中突出显示了选定的移动属性。](./images/implement-assurance/select-mobile-property.png)

此 **移动资产详细信息** 页面。 选择 **[!UICONTROL 扩展]** 调出当前与您的移动资产关联的扩展的列表。

![此时将显示移动属性详细信息页面。 将显示有关最近活动的信息。 扩展选项卡会突出显示。](./images/implement-assurance/tag-properties.png)

选择 **[!UICONTROL 目录]** 查看可添加到移动资产的扩展列表。 使用过滤器，找到 **[!UICONTROL AEP保证]** 扩展并选择 **[!UICONTROL 安装]**.

![此时会显示扩展目录。 将筛选并显示Assurance扩展，并突出显示install按钮。](./images/implement-assurance/assurance-extension.png)

## 后续步骤

现在，您已将Assurance扩展安装在移动资产中，您可以在应用程序内开始使用Assurance 。 要了解如何将Assurance扩展添加到应用程序，请阅读 [Adobe Experience Platform Assurance扩展概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). 要了解如何使用Assurance，请阅读 [使用Assurance指南](./using-assurance.md).
