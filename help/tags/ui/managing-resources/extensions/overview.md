---
title: 扩展
description: 了解标记扩展在Adobe Experience Platform中的工作方式。
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
source-git-commit: f7edfa05e25c17f9ace34287c8a2d8426d0f36d4
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 63%

---

# 扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

扩展是一组打包的代码，用于扩展标记或事件转发提供的功能。

添加扩展会添加新的数据元素和用于创建规则的新选项。

扩展可确定构建资产、规则和数据元素时可用的元素。它们会提供：

* 事件、条件和例外
* 数据元素
* 客户端代码

使用扩展列表顶部的链接可以查看已安装的扩展、扩展目录或更新。

选择一个扩展，然后选择[!UICONTROL Configure]以查看和更改扩展的设置。 有关更多信息，请参阅[添加新扩展](#add-a-new-extension)中的部分，以了解有关扩展选项的信息。

>[!IMPORTANT]
>
>所做的更改在[发布](../../publishing/overview.md)之后才会生效。

默认情况下，Adobe会提供支持常用集成的扩展。 可以使用自定义配置修改扩展。配置则通过扩展提供。要创建配置，请选择扩展卡，然后选择&#x200B;**[!UICONTROL Add New Configuration]**。

## 扩展目录

使用扩展目录可浏览、配置和部署由独立软件供应商构建和维护的营销和广告技术，以及Adobe解决方案的扩展。

Extensions 页面提供了三个视图：

* Installed

   显示所有已安装的扩展。

* Catalog
* 显示所有可用的扩展。
* Updates

   显示已安装扩展的更新。

选择&#x200B;**[!UICONTROL Extensions]**&#x200B;可查看所有已安装的扩展。 您还可以使用目录查看所有可用扩展的列表以及具有可用更新的扩展。

有关Adobe拥有的扩展的详细信息，请参阅[扩展引用](../../../extensions/web/overview.md)。

## 添加新扩展 {#add-a-new-extension}

标记极具可扩展性。 扩展可为标记添加核心功能。 扩展的常见用途是创建与其他应用程序的集成。

1. 在资产的概述页面中，打开&#x200B;**[!UICONTROL Extensions]**&#x200B;选项卡。
1. 选择一个扩展。

   ![核心扩展](../../../images/extensions.png)

   * 如果该扩展存在，请从扩展目录中选择它。
   * 将鼠标悬停在列表中的扩展上以配置或禁用该扩展。
   * 从目录中添加其他扩展（如果这些扩展当前不在您的列表中）。

   核心扩展是新扩展的起点。默认扩展会提供：

   * 默认事件
   * 默认条件和例外
   * 默认客户端代码

   这些默认内容是您将为创建扩展而构建的自定义规则的基础。

创建或编辑元素后，您可以将其保存并生成到[活动库](../../publishing/libraries.md#active-library)。这会立即将更改保存到库并执行生成操作。随即会显示生成操作的状态。您还可以从 Active Library 下拉菜单中创建新库。

## 配置扩展

将鼠标悬停在已安装的扩展上，然后选择&#x200B;**[!UICONTROL 配置]**。

>[!NOTE]
>
>某些扩展既不需要配置，也不提供配置选项。

每个可配置的扩展都具有独特的选项。有关每个Adobe扩展可用选项的信息，请参阅[扩展参考](../../../extensions/web/overview.md)。
