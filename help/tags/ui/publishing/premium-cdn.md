---
title: 对标记的高级CDN支持
description: 了解适用于标记的高级CDN功能，以及如何使用该功能在多个地理区域交付内容。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 针对标记的Premium CDN支持（测试版）

>[!IMPORTANT]
>
>标记的高级CDN功能目前处于测试阶段，贵组织可能还无法访问该功能。 本文档可能会发生更改。

当您使用 [Adobe管理的主机](./hosts/managed-by-adobe-host.md) 为了在您的网站上交付Adobe Experience Platform标记资产，这些资产会分发到世界各地的各种内容交付网络(CDN)，以提供最快的下载速度。 但是，某些地区要求复制所有网站资产并将其托管在该地区内的服务器上。

为此，Experience Platform中的标记提供了一项高级CDN功能，允许您向这些特殊地区交付内容。

高级CDN支持是一项付费功能，贵组织必须购买才能启用和使用该功能。 本指南介绍购买此功能后，如何在数据收集UI中配置和使用此功能。

## 为贵组织启用高级CDN

Premium CDN在公司级别启用。 贵组织购买高级CDN功能后，Adobe管理员将在数据收集UI中为贵公司启用此功能。

## 使用更新的嵌入代码重建和安装标记库

启用高级CDN后，并不意味着您的标记资产会立即复制并准备在新区域中使用。 这仅意味着您现在可以选择何时选择启用此功能。

>[!IMPORTANT]
>
>在启用高级CDN之前构建的库将继续按原样运行，与现在完全一样。 这也适用于不由Adobe管理的库，因为 [存档环境](./environments.md#archive) 仅对其资产路径使用相对URL。 请注意，启用高级CDN后，您构建的任何不由Adobe管理的库都会像未启用高级CDN功能一样运行。

启用高级CDN并重新构建您希望从新托管区域使用的任何库后，即可检索新的托管区域嵌入代码以添加到您的网站。

>[!NOTE]
>
>库嵌入代码，列在 [!UICONTROL 标准] 托管区域将继续按原样工作，以及您网站上已有的任何Page Top或Page Bottom嵌入代码。

访问 **[!UICONTROL 环境]** 页面或查看库编辑屏幕中的环境安装说明，以查找新的嵌入代码。 每个新的受支持托管区域都显示在 [!UICONTROL 标准] 托管区域（用于全球范围内没有高级CDN支持的区域）。 以下屏幕截图显示了中国地区的嵌入代码，该代码使用 `.cn` 作为其顶级域(TLD)。

![中国地区的嵌入代码](../../images/ui/publishing/premium-cdn/embed-codes.png)

为网页选择适当的嵌入代码，并将其粘贴到 `<head>` 标记。 有关使用嵌入代码安装标记库的更多信息，请参阅 [环境UI指南](./environments.md#installation).

## 后续步骤

本指南介绍了如何为您的标记实施启用和安装高级CDN功能。 有关在Web资产和移动资产上安装和测试标签库的更多信息，请参阅 [发布概述](./overview.md).
