---
keywords: 目标个性化；目的地；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中提供基于AI的实时个性化和实验功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 46e732dfc630ad1875a57289a6e6cf9c964b9547
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---

# Adobe Target连接 {#adobe-target-connection}

## 概述 {#overview}

Adobe Target是一款应用程序，可在跨网站、移动设备应用程序等的所有入站客户交互中提供基于AI的实时个性化和实验功能。

Adobe Target是Adobe Experience Platform中的一个个性化连接。

## 先决条件 {#prerequisites}

配置Adobe Target连接时 [使用数据流ID](#parameters)，则必须具有 [Adobe Experience Platform Web SDK](../../../edge/home.md) 已实施。

在不使用数据流ID的情况下配置Adobe Target连接不需要您实施Web SDK。

>[!IMPORTANT]
>
>在创建 [!DNL Adobe Target] 连接，请阅读有关如何 [为同一页面和下一页面个性化配置个性化目标](../../ui/configure-personalization-destinations.md). 本指南将引导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。 同页和下一页个性化要求您在配置Adobe Target连接时使用数据流ID。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在为单个配置文件请求在Adobe Target目标中映射的所有区段。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 用例 {#use-cases}

**个性化主页横幅**

一家房屋租赁和销售公司希望根据Adobe Experience Platform的客户细分资格，使用横幅个性化其主页。 该公司可以选择哪些受众应获得个性化体验，并将这些体验作为其Target选件的定位标准发送到Adobe Target。

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流ID"
>abstract="此选项确定将包含区段的数据收集数据流。 下拉菜单仅显示启用了Target配置的数据流。 要使用边缘分段，必须选择数据流ID。 选择“无”会禁用使用边缘分段的所有用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="了解有关选择数据流的更多信息"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

Adobe Experience Platform会自动连接到您公司的Adobe Target实例。 无需进行身份验证。

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **名称**:填写此目标的首选名称。
* **描述**:输入目标的描述。 例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
* **数据流ID**:这可确定将包含区段的数据收集数据流。 下拉菜单仅显示启用了Target目标的数据流。 请参阅 [配置数据流](../../../edge/datastreams/overview.md#target) 有关如何为Adobe Target配置数据流的详细信息。
   * **[!UICONTROL 无]**:如果您需要配置Adobe Target个性化，但无法实施 [Experience PlatformWeb SDK](../../../edge/home.md). 使用此选项时，从Experience Platform导出到Target的区段仅支持下一会话个性化，并且会禁用边缘分段。 有关更多信息，请参阅下表。

| 未选择数据流 | 已选择数据流 |
|---|---|
| <ul><li>[边缘分割](../../../segmentation/ui/edge-segmentation.md) 不支持。</li><li>[同页和下一页个性化](../../ui/configure-personalization-destinations.md) 不受支持。</li><li>您只能将区段共享到生产沙盒的Adobe Target连接。</li><li>要在不使用数据流ID的情况下配置下一个会话的个性化，请使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>边缘分割可按预期工作。</li><li>[同页和下一页个性化](../../ui/configure-personalization-destinations.md) 。</li><li>其他沙箱支持区段共享。</li></ul> |

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [将用户档案和区段激活到用户档案请求目标](../../ui/activate-profile-request-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

Adobe Target从Adobe Experience Platform边缘网络中读取用户档案数据，因此不会导出任何数据。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
