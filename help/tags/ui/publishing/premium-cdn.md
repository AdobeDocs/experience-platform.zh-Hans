---
title: 标记的Premium CDN支持
description: 了解标记的高级CDN功能，以及如何将其用于在多个地理区域交付内容。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 标记的Premium CDN支持（测试版）

>[!IMPORTANT]
>
>标记的高级CDN功能当前为测试版，您的组织可能还不能访问它。 此文档可能会发生更改。

当您使用 [Adobe管理的主机](./hosts/managed-by-adobe-host.md) 为了在您的网站上交付您的Adobe Experience Platform标记资产，这些资产在全球各地的各种内容交付网络(CDN)中分发，以提供最快的下载速度。 但是，某些区域要求将所有网站资产复制并托管到该区域的服务器上。

为此，Experience Platform中的标记提供了一项高级CDN功能，可让您向这些特殊区域交付内容。

Premium CDN支持是一项付费功能，贵组织必须购买它才能启用和使用它。 本指南介绍购买此功能后，如何在Experience PlatformUI或数据收集UI中配置和使用此功能。

## 为您的组织启用Premium CDN

Premium CDN在公司级别启用。 贵组织购买高级CDN功能后，Adobe管理员将在贵公司的UI中启用该功能。

## 使用更新的嵌入代码重建和安装标记库

启用Premium CDN后，并不意味着您的标记资产会立即复制并在新区域中随时可用。 它仅意味着您现在可以选择何时选择启用此功能。

>[!IMPORTANT]
>
>在启用高级CDN之前构建的库将继续按原样运行。 这也适用于不由Adobe管理的库，因为 [存档环境](./environments.md#archive) 仅对其资源路径使用相对URL。 请注意，启用Premium CDN后，您构建的任何非由Adobe管理的库都将像未启用Premium CDN功能一样运行。

启用高级CDN并重建要从新托管区域使用的任何库后，您可以检索要添加到网站的新托管区域嵌入代码。

>[!NOTE]
>
>列在下的库嵌入代码 [!UICONTROL 标准] 托管区域将继续按原样运行，并且您的网站上已存在的任何Page Top或Page Bottom嵌入代码也将按原样运行。

访问 **[!UICONTROL 环境]** 从“库编辑”屏幕中页面或查看环境安装说明，以查找新的嵌入代码。 每个新的受支持托管区域都显示在 [!UICONTROL 标准] 托管区域（用于世界上受支持、但无高级CDN的地区）。 以下屏幕截图显示了用于“中国”区域的嵌入代码，该代码使用 `.cn` 作为其顶级域(TLD)。

![中国地区的嵌入代码](../../images/ui/publishing/premium-cdn/embed-codes.png)

为网页选择相应的嵌入代码，并将其粘贴到 `<head>` 标记的位置。 有关使用嵌入代码安装标记库的更多信息，请参阅 [环境用户界面指南](./environments.md#installation).

## 后续步骤

本指南介绍了如何为标记实施启用和安装高级CDN功能。 有关在Web和移动资产上安装和测试标记库的更多信息，请参阅 [发布概述](./overview.md).
