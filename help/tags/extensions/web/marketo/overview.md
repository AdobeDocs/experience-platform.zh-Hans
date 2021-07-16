---
title: Marketo Munchkin 扩展 概述
description: 了解Adobe Experience Platform中的Marketo Munchkin标记扩展。
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 62%

---

# Marketo Munchkin扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../../term-updates.md)。

使用此扩展可将 [!DNL Marketo Munchkin] JavaScript 跟踪代码与您的资产相集成。[!DNL Marketo Munchkin] JavaScript 允许跟踪最终用户对 Marketo 登陆页面和外部网页的页面访问次数和导航次数。

## 安装 Marketo Munchkin 扩展

如果尚未安装[!DNL Marketo Munchkin]扩展，请打开您的资产，选择&#x200B;**[!UICONTROL Extensions > Catalog]**，将鼠标悬停在[!DNL Marketo Munchkin]扩展上，然后选择&#x200B;**[!UICONTROL Install]**。

此扩展没有必需的配置。

## Marketo Munchkin 扩展操作类型

此部分介绍了 [!DNL Marketo Munchkin] 扩展中可用的操作类型。

### 初始化

![](../../../images/munchkin-Init.png)

**Munchkin ID：（必需）**&#x200B;位于“Admin”>“Integration”>“Munchkin”菜单下的 Munchkin 帐户 ID。

**Configurations：**[此处](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)介绍了所有可配置参数。

### 访问网页

![](../../../images/munchkin-visit-page.png)

**url：（必需）**&#x200B;用于记录页面访问的 URL 文件路径。

**params：**&#x200B;要记录的所需参数的查询字符串。

**name：**&#x200B;网页资产的自定义名称。

### 单击链接

![](../../../images/munchkin-click-link.png)

**href：（必需）**&#x200B;用于记录链接选择的 URL 文件路径。
