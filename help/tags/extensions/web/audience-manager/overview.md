---
title: Adobe Audience Manager扩展概述
description: 了解Adobe Experience Platform中的Adobe Audience Manager标记扩展。
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 63%

---

# Adobe Audience Manager扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../../term-updates.md)。

使用Audience Manager标记扩展，您可以将Audience Manager使用的DIL代码与Adobe Experience Platform中的资产相集成。

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

>[!NOTE]
>
>此扩展不适用于Adobe Analytics数据的事件转发。 对于事件转发，请使用[Adobe Analytics扩展](../analytics/overview.md)。

## 配置 Adobe Audience Manager 扩展

如果尚未安装Adobe Audience Manager扩展，请打开您的资产，选择&#x200B;**[!UICONTROL Extensions > Catalog]**，将鼠标悬停在Adobe Audience Manager扩展上，然后选择&#x200B;**[!UICONTROL Install]**。

要配置该扩展，请打开[!UICONTROL Extensions]选项卡，将鼠标悬停在该扩展上，然后选择&#x200B;**[!UICONTROL Configure]**。

### DIL 设置

配置 DIL 设置。可以使用以下配置选项：

![](../../../images/ext-aam-config.png)

#### DIL Version

显示数据集成库 (DIL) 版本。

此设置无法更改。

#### Exclude Specific Paths

如果 URL 与任何排除的路径相匹配，则不会加载该扩展。

选择&#x200B;**[!UICONTROL 添加路径]**&#x200B;以指定排除的URL。

如果 URL 是正则表达式，则启用 Regex。

#### Use DIL Site Catalyst Module

[SiteCatalyst 模块](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html)可与 DIL 配合使用，以将 Analytics 标记元素发送至 Audience Manager。

使用代码编辑器配置 siteCatalyst.init 文件。

您还可以创建一个注释，其中包含有关此配置的信息。

#### Use DIL Google Analytics Module

启用 [Google Analytics 模块](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)。

#### DIL.create Initialization Properties

添加 [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) 使用的初始化属性，以及 [visitorService 对象](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html)的命名空间子属性。在代码编辑器中，代码注释包含两个示例用例。

选择&#x200B;**[!UICONTROL 选择项目]**&#x200B;以添加其他属性。

将鼠标悬停在“i”图标上，可了解每个属性的用途。您可以在 [Audience Manager DIL 文档](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html)中找到有关这些属性的更多信息。

配置完扩展后，选择&#x200B;**[!UICONTROL Save]**。

## Adobe Audience Manager 扩展操作类型

本主题介绍 Audience Manager 扩展中可用的操作类型。

Adobe Audience Manager 扩展在规则的 Then 部分中提供了以下操作：

### Run Custom Code

运行在代码编辑器中配置的自定义代码。

在代码编辑器中输入所需的代码，然后提供代码的名称。此代码将在规则生成器的 Then 部分中变得可用。

![](../../../images/ext-aam-then.png)

您还可以添加一个注释，其中包含有关配置的信息。
