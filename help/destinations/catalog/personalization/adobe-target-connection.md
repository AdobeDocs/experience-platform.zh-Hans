---
keywords: 目标个性化；目的地；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中提供基于AI技术的实时个性化和实验。
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Adobe Target连接（测试版） {#adobe-target-connection}

## 概述 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe Target连接当前为测试版。 文档和功能可能会发生更改。

Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中，提供基于AI的实时1:1个性化和实验。

Adobe Target是Adobe Experience Platform中的一个个性化连接。

## 先决条件 {#prerequisites}

此集成由[Adobe Experience Platform Web SDK](../../../edge/home.md)提供支持。 您必须使用此SDK才能使用此目标。

## 导出类型 {#export-type}

**配置文件请求**  — 您正在为单个配置文件请求在Adobe Target目标中映射的所有区段。

## 用例 {#use-cases}

**个性化主页横幅**

一家房屋租赁和销售公司希望根据Adobe Experience Platform的客户细分资格，使用横幅个性化其主页。 该公司可以选择哪些受众应获得个性化体验，并将这些体验作为其Target选件的定位标准发送到Adobe Target。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

Adobe Experience Platform会自动连接到您公司的Adobe Target实例。 无需进行身份验证。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **名称**:填写此目标的首选名称。
* **描述**:输入目标的描述。例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
* **数据流ID**:这可确定区段将包含在页面响应中的数据收集数据流。下拉菜单仅显示已启用目标配置的数据流。 有关更多详细信息，请参阅[配置数据流](../../../edge/fundamentals/datastreams.md)。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到配置文件请求目标](../../ui/activate-profile-request-destinations.md)。

## 导出的数据 {#exported-data}

Adobe Target从Adobe Experience Platform边缘网络中读取用户档案数据，因此不会导出任何数据。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请阅读[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。
