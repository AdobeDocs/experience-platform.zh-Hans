---
title: 实施Adobe Experience Platform Assurance扩展
description: 本指南介绍如何实施和安装Adobe Experience Platform Assurance扩展。
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# 实施Adobe Experience Platform保证扩展

本教程介绍如何在Mobile SDK中安装和实施平台保障扩展。 有关将保障扩展添加到应用程序的说明，请阅读 [Adobe Experience Platform保障扩展概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## 快速入门

要安装和实施保障扩展，您需要访问以下服务：

- 的 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

## 创建移动 属性

>[!NOTE]
>
>如果您已经拥有移动资产，则可以继续执行下一步。

在数据收集UI中，选择 **[!UICONTROL 标记]**. 此时会显示移动和Web属性列表，其中包含有关属于贵组织的属性的信息。 选择 **[!UICONTROL 新资产]** 创建新资产。

![“新建属性”按钮将突出显示，显示您选择创建新属性的内容](./images/implement-assurance/create-new-property.png)

的 **[!UICONTROL 创建资产]** 页面。 输入新资产的名称，然后选择 **[!UICONTROL 移动设备]** 作为平台。 插入详细信息后，选择 **[!UICONTROL 保存]** 创建移动资产。

>[!NOTE]
>
>移动资产的 **[!UICONTROL 隐私]** 设置操作 **not** 会影响保证的数据收集。

![此时将显示“创建属性”页面。 您可以在此处插入有关您的移动资产的信息。](./images/implement-assurance/create-property.png)

## 安装Assurance扩展

选择要在中安装Assurance扩展的移动资产。

![此时会显示标记属性页面，并突出显示选定的移动属性。](./images/implement-assurance/select-mobile-property.png)

的 **移动属性详细信息** 页面。 选择 **[!UICONTROL 扩展]** 以显示当前与您的移动资产关联的扩展列表。

![此时会显示移动属性详细信息页面。 此时会显示有关最近活动的信息。 扩展选项卡会突出显示。](./images/implement-assurance/tag-properties.png)

选择 **[!UICONTROL 目录]** 以查看可添加到移动资产的扩展列表。 使用过滤器，找到 **[!UICONTROL AEP保证]** 扩展，然后选择 **[!UICONTROL 安装]**.

![将显示扩展目录。 将筛选并显示保证扩展，并突出显示安装按钮。](./images/implement-assurance/assurance-extension.png)

## 后续步骤

现在，您已在移动资产中安装了Assurance扩展，接下来可以在应用程序中开始使用Assurance。 要了解如何将保证扩展添加到您的应用程序，请阅读 [Adobe Experience Platform保障扩展概述](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). 要了解如何使用“保证”，请阅读 [使用保证指南](./using-assurance.md).
