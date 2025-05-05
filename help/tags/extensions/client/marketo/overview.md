---
title: Marketo Munchkin扩展概述
description: 了解Adobe Experience Platform中的Marketo Munchkin标记扩展。
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 55%

---

# Marketo Munchkin扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用此扩展可将 [!DNL Marketo Munchkin] JavaScript 跟踪代码与您的资产相集成。[!DNL Marketo Munchkin] JavaScript 允许跟踪最终用户对 Marketo 登陆页面和外部网页的页面访问次数和导航次数。

## 安装 Marketo Munchkin 扩展

如果尚未安装[!DNL Marketo Munchkin]扩展，请打开您的属性，然后选择&#x200B;**[!UICONTROL 扩展>目录]**，将鼠标悬停在[!DNL Marketo Munchkin]扩展上，然后选择&#x200B;**[!UICONTROL 安装]**。

此扩展没有必需的配置。

## Marketo Munchkin 扩展操作类型

本节介绍[!DNL Marketo Munchkin]扩展中可用的操作类型。

### 初始化

![](../../../images/munchkin-Init.png)

**Munchkin ID：（必需）**&#x200B;位于“Admin”>“Integration”>“Munchkin”菜单下的 Munchkin 帐户 ID。

**Configurations：**&#x200B;[此处](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)介绍了所有可配置参数。

### 访问网页

![](../../../images/munchkin-visit-page.png)

**url：（必需）**&#x200B;用于记录页面访问的 URL 文件路径。

**params：**&#x200B;要记录的所需参数的查询字符串。

**name：**&#x200B;网页资产的自定义名称。

### 单击链接

![](../../../images/munchkin-click-link.png)

**href：（必需）**&#x200B;用于记录链接选择的 URL 文件路径。
