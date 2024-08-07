---
title: 扩展升级
description: 了解扩展升级在扩展目录中如何打包和呈现。
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 72%

---

# 扩展升级

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

扩展开发人员会不断向其扩展中添加新功能，并且还经常修复错误。这些更新将打包到扩展的新版本中，并在扩展目录中作为升级提供。

## 扩展目录

当扩展开发人员提供了扩展的新版本时，该新版本将在扩展目录中可用。该目录仅会显示扩展的最新版本。您无法安装 `latest` 以外的任何扩展版本。

在资产上安装扩展时，将会安装当前可用的版本，并且自此以后，您的资产将保留该特定版本，即使将较新版本添加到目录中也是如此。

## 升级通知

如果您在资产上安装了扩展，并且目录中提供了较新的版本，则当您查看Installed Extensions页面时，您将在扩展卡片上看到[!UICONTROL 升级]按钮。

编辑该扩展提供的资源时，您也会看到通知。

## 升级具有永久性

如果要升级到目录中提供的较新版本，则必须自行安装该升级。升级即是“更改”，必须先将升级添加到库中，并对其进行测试和发布，然后升级才会对已部署的标记产生影响。

切勿随意升级。除非您准备好测试新扩展并对其进行部署，否则不应升级。将升级添加到您的资产后，必须将其包含在所有库中。任何不包含已升级扩展的库都将在生成时失败。

目前无法将扩展降级至以前的版本。升级后（无论是否发布），新扩展版本都会保留在您的资产上。

## 升级过程

安装升级的过程与首次安装扩展的过程大致相同。

1. 选择&#x200B;**[!UICONTROL 升级]**&#x200B;以转到[!UICONTROL 扩展配置]屏幕。
1. 根据需要做出任何配置更改。
1. 选择&#x200B;**[!UICONTROL 保存]**。

在您点击&#x200B;**[!UICONTROL 保存]**&#x200B;之前，实际不会执行升级。 在此之前的任何时间，您都可以选择[!UICONTROL 取消]，并继续使用当前安装的版本。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;后将无法撤销。

如果您的库处于 `Approved` 或 `Submitted` 状态，则不允许执行扩展升级。这是因为下一个生成版本必须包含新的扩展版本。对于处于 `Approved` 或 `Submitted` 状态的库，下一个生成版本是生产版本。该生成操作将由于不包含最新版本而失败，因此工作流程是在升级扩展&#x200B;_之前_&#x200B;发布或拒绝处于 `Approved` 或 `Submitted` 状态的库。

## 发布升级

当您将已升级的扩展安装在您的资产上以后，必须将其包含在所有库中。对于任何不包含该已升级扩展的库，将会显示生成失败消息。

除此之外，将已升级的扩展添加到库的方式与[将任何其他更改添加到库](../../publishing/libraries.md)的方式相同。

在[!UICONTROL Edit Library]屏幕中，您可以使用“[!UICONTROL Add All Changed Resources]”按钮，也可以使用“[!UICONTROL Add a Resource]”按钮并自行选择升级的扩展。

>[!TIP]
>
>扩展开发人员可以将新配置项添加到其扩展视图中，以便启用新功能。如果您在升级到新扩展版本后看到生成失败 - 并且您已经查明生成失败是由该扩展所导致 - 则您需要先转到扩展的 Configure 页面，并确保单击 Save（即使您没有更改任何内容）。然后，将新更改添加到库中，并尝试再次生成。

在将扩展升级添加到库之后，您可以按照[发布流](../../publishing/publishing-flow.md)中概述的步骤，发布库用于生产。
