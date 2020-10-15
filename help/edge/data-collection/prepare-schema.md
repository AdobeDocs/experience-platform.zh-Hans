---
title: 准备XDM模式
seo-title: 准备XDM模式
description: 帮助您在Adobe Experience Platform构建XDM模式的指南
seo-description: 帮助您在Adobe Experience Platform构建XDM模式的指南
keywords: XDM;schema;create schema;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 4%

---


# 准备模式

Experience Platform边缘网络使用体验数据模型(XDM)。 XDM是一种数据格式，允许您定义模式。 模式定义边缘网络希望数据的格式。 要发送数据，您必须定义模式。

1. [创建模式](../../xdm/tutorials/create-schema-ui.md)
2. 将AEP Mixin [!DNL Web SDK ExperienceEvent] 添加到您创建的模式。
3. 根据您创建的模式创建数据集。

以下视频旨在支持您为模式创建数据集、数据集和流源连接器。 [!DNL Web SDK]


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

登录Adobe Experience Platform Launch并安装AEP Web SDK扩展。 安装SDK时，系统会提示您配置扩展。 输入您在上面请求的配置ID。 该扩展将自动填充您的组织ID。

有关不同配置选项的更多详细信息，请 [参阅配置SDK](../fundamentals/configuring-the-sdk.md)。

[进一步了解如何构建模式](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/schema/composition.html)
