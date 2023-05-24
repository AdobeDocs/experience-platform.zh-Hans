---
title: Adobe Audience Manager擴充功能概觀
description: 了解 Adobe Experience Platform 中的 Adobe Audience Manager 标记扩展。
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 71%

---

# Adobe Audience Manager擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

透過Audience Manager標籤擴充功能，您可以整合Audience Manager所使用的DIL程式碼與Adobe Experience Platform中的屬性。

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

>[!NOTE]
>
>此擴充功能不適用於Adobe Analytics資料的事件轉送。 若要進行事件轉送，請使用 [Adobe Analytics擴充功能](../analytics/overview.md).

## 配置 Adobe Audience Manager 扩展

如果尚未安裝Adobe Audience Manager擴充功能，請開啟您的屬性，然後選取「 」 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在Adobe Audience Manager擴充功能上，然後選取「 」 **[!UICONTROL 安裝]**.

若要設定擴充功能，請開啟 [!UICONTROL 擴充功能] 索引標籤，將游標停留在擴充功能上，然後選取「 」 **[!UICONTROL 設定]**.

### DIL 设置

配置 DIL 设置。可以使用以下配置选项：

![](../../../images/ext-aam-config.png)

#### DIL Version

显示数据集成库 (DIL) 版本。

此设置无法更改。

#### Exclude Specific Paths

如果 URL 与任何排除的路径相匹配，则不会加载该扩展。

選取 **[!UICONTROL 新增路徑]** 以指定排除的URL。

如果 URL 是正则表达式，则启用 Regex。

#### Use DIL Site Catalyst Module

[SiteCatalyst 模块](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_sc_init.html)可与 DIL 配合使用，以将 Analytics 标记元素发送至 Audience Manager。

使用代码编辑器配置 siteCatalyst.init 文件。

您还可以创建一个注释，其中包含有关此配置的信息。

#### Use DIL Google Analytics Module

启用 [Google Analytics 模块](https://experiencecloud.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)。

#### DIL.create Initialization Properties

添加 [DIL.create](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html) 使用的初始化属性，以及 [visitorService 对象](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_visitor_service.html)的命名空间子属性。在代码编辑器中，代码注释包含两个示例用例。

選取 **[!UICONTROL 選擇專案]** 以新增其他屬性。

将鼠标悬停在“i”图标上，可了解每个属性的用途。您可以在 [Audience Manager DIL 文档](https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_create.html)中找到有关这些属性的更多信息。

選取 **[!UICONTROL 儲存]** 完成擴充功能設定後。

## Adobe Audience Manager 扩展操作类型

本主题介绍 Audience Manager 扩展中可用的操作类型。

Adobe Audience Manager 扩展在规则的 Then 部分中提供了以下操作：

### Run Custom Code

运行在代码编辑器中配置的自定义代码。

在代码编辑器中输入所需的代码，然后提供代码的名称。此代码将在规则生成器的 Then 部分中变得可用。

![](../../../images/ext-aam-then.png)

您还可以添加一个注释，其中包含有关配置的信息。
