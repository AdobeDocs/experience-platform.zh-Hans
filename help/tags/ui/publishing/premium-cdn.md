---
title: Experience Platform标记（中国）
description: 了解用于标记的Experience Platform标记（中国）功能，以及如何将其用于在多个地理区域交付您的内容。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Experience Platform标记（中国）

当您使用 [Adobe管理的主机](./hosts/managed-by-adobe-host.md) 为了在您的网站上交付Adobe Experience Platform标记资产，这些资产在全球各地的各种内容交付网络(CDN)中分发，从而提供最快的下载速度。 但是，某些区域要求将所有网站资产复制并托管到该区域的服务器上。

为此，Experience Platform中的标记提供了Experience Platform标记（中国）功能，可让您向这些特殊区域交付内容。

Experience Platform标签（中国）支持是一项付费功能，您的组织必须购买它才能启用和使用。 本指南介绍购买此功能后，如何在Experience PlatformUI或数据收集UI中配置和使用它。

## 为您的组织启用Experience Platform标签（中国）

Experience Platform标记（中国）在公司级别启用。 贵组织购买Experience Platform标记（中国）功能后，Adobe管理员将在贵公司的UI中启用该功能。

## 使用更新的嵌入代码重建并安装标记库

启用Experience Platform标记（中国）后，并不意味着您的标记资产会立即复制并准备在新的区域中使用。 这仅意味着您现在可以选择何时选择启用此功能。

>[!IMPORTANT]
>
>在中国启用标记之前构建的库将继续按原样运行。 这也适用于不由Adobe管理的库，因为 [归档环境](./environments.md#archive) 仅将相对URL用于其资源路径。 请注意，启用“Experience Platform标签（中国）”后，您构建的任何不受Adobe管理的库都将像未启用“中国标签”功能那样发挥作用。

在中国启用了标记并重建了要从新托管区域使用的任何库后，您可以检索新的托管区域嵌入代码以添加到您的网站。

>[!NOTE]
>
>列在下面的库嵌入代码 [!UICONTROL 标准] 托管区域将继续按原样工作，并且您的网站上已存在的任何Page Top或Page Bottom嵌入代码也将按原样工作。

访问 **[!UICONTROL 环境]** 从library edit屏幕中，页面或查看环境安装说明以查找新的嵌入代码。 每个新的受支持托管区域都显示在 [!UICONTROL 标准] 托管区域(用于世界上无Experience Platform标签支持的区域（中国）)。 以下屏幕截图显示了用于“中国”区域的嵌入代码，该代码使用 `.cn` 作为其顶级域(TLD)。

![中国地区的嵌入代码](../../images/ui/publishing/premium-cdn/embed-codes.png)

为网页选择相应的嵌入代码，并将其粘贴到 `<head>` 标记之前。 有关使用嵌入代码安装标记库的更多信息，请参阅 [环境用户界面指南](./environments.md#installation).

## 后续步骤

本指南介绍如何为标签实施启用和安装Experience Platform标签（中国）功能。 有关在Web和移动资产上安装和测试标记库的更多信息，请参阅 [发布概述](./overview.md).
