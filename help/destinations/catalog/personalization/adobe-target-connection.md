---
keywords: 目标个性化；目的地；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中提供基于AI的实时个性化和实验功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: ee9ed1c17a566f37b4ad79df7c66f8b2ffb4b879
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Adobe Target连接 {#adobe-target-connection}

## 概述 {#overview}

Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中提供基于AI的实时个性化和实验功能。

Adobe Target是Adobe Experience Platform中的一个个性化连接。

## 先决条件 {#prerequisites}

此集成由 [Adobe Experience Platform Web SDK](../../../edge/home.md). 您必须使用此SDK才能使用此目标。

## 导出类型 {#export-type}

**用户档案请求**  — 您正在为单个配置文件请求在Adobe Target目标中映射的所有区段。

## 用例 {#use-cases}

**个性化主页横幅**

一家房屋租赁和销售公司希望根据Adobe Experience Platform的客户细分资格，使用横幅个性化其主页。 该公司可以选择哪些受众应获得个性化体验，并将这些体验作为其Target选件的定位标准发送到Adobe Target。

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>在创建 [!DNL Adobe Target] 连接时，我们建议您阅读我们的指南 [为同一页面和下一页面个性化配置个性化目标](../../ui/configure-personalization-destinations.md). 本指南将引导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流ID"
>abstract="此选项确定区段在响应页面时将包含在哪些数据收集数据流中。 下拉菜单仅显示已启用目标配置的数据流。 必须先配置数据流，然后才能配置目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="了解如何配置数据流。"

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

Adobe Experience Platform会自动连接到您公司的Adobe Target实例。 无需进行身份验证。

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **名称**:填写此目标的首选名称。
* **描述**:输入目标的描述。 例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
* **数据流ID**:这可确定区段将包含在页面响应中的数据收集数据流。 下拉菜单仅显示已启用目标配置的数据流。 请参阅 [配置数据流](../../../edge/fundamentals/datastreams.md) 以了解更多详细信息。

## 将区段激活到此目标 {#activate}

读取 [将用户档案和区段激活到用户档案请求目标](../../ui/activate-profile-request-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

Adobe Target从Adobe Experience Platform边缘网络中读取用户档案数据，因此不会导出任何数据。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
