---
title: 使用来自DNL的天气数据天气频道
description: 使用来自DNL天气频道的天气数据来增强您通过数据流收集的数据。
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# 使用来自的天气数据 [!DNL The Weather Channel]

Adobe已与 [!DNL [The Weather Company]](https://www.ibm.com/weather) 为通过数据流收集的数据引入美国天气的额外上下文。 您可以将此数据用于Experience Platform中的分析、定位和区段创建。

有3种类型的数据可从以下位置获得： [!DNL The Weather Channel]：

* **[!UICONTROL 当前天气]**：用户的当前天气情况（基于其位置）。 这包括当前温度、沉降、云覆盖率等。
* **[!UICONTROL 预测天气]**：该预测包括用户位置的1、2、3、5、7和10天预测。
* **[!UICONTROL 触发器]**：触发器是映射到不同语义天气条件的特定组合。 有三种不同类型的天气触发器：

   * **[!UICONTROL 天气触发器]**：语义上有意义的情况，例如寒冷或雨天。 不同气候之间的定义可能有所不同。
   * **[!UICONTROL 产品触发器]**：导致购买不同类型产品的条件。 例如：寒冷的天气预报可能意味着购买雨衣的可能性更大。
   * **[!UICONTROL 恶劣天气触发程序]**：严重天气警告，例如冬季风暴或飓风警告。

## 先决条件 {#prerequisites}

在使用天气数据之前，请确保满足以下先决条件：

* 您必须从以下来源获取要使用的天气数据的许可证： [!DNL The Weather Channel]. 然后，他们将在您的帐户中启用它。
* 天气数据只能通过数据流使用。 要使用天气数据，您必须使用 [!DNL Web SDK]， [!DNL Mobile Edge Extension] 或 [服务器API](../../../server-api/overview.md) 以利用这些数据。
* 您的数据流必须具有 [[!UICONTROL 地理位置]](../configure.md#advanced-options) 已启用。
* 添加 [天气字段组](#schema-configuration) 到您使用的架构。

## 配置中 {#provisioning}

一旦您从获得数据许可 [!DNL The Weather Channel]，它们将允许您的帐户访问数据。 接下来，您必须联系Adobe客户关怀团队，才能在数据流上启用数据。 启用后，数据将自动附加。

您可以通过以下方法验证它是否正在添加：使用调试器运行Edge跟踪，或使用Assurance跟踪点击 [!DNL Edge Network].

### 架构配置 {#schema-configuration}

必须将天气字段组添加到与您在数据流中使用的Experience Platform数据集对应的事件架构中。 有五个可用的字段组：

* [!UICONTROL 预测天气]
* [!UICONTROL 当前天气]
* [!UICONTROL 产品触发器]
* [!UICONTROL 相对触发器]
* [!UICONTROL 恶劣天气触发程序]

## 访问天气数据 {#access-weather-data}

您的数据获得许可并可用后，您便可以在整个Adobe服务中以各种方式访问它。

### Adobe Analytics {#analytics}

In [!DNL Adobe Analytics]，则天气数据可通过处理规则进行映射，以及您的其余部分 [!DNL XDM] 架构。

您可以在以下位置找到可映射的字段列表： [天气参考](weather-reference.md) 页面。 与所有项目一样 [!DNL XDM] 架构，键值将带有前缀 `a.x`. 例如，一个名为的字段 `weather.current.temperature.farenheit` 将显示在 [!DNL Analytics] 作为 `a.x.weather.current.temperature.farenheit`.

![处理规则界面](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### 了解 Adobe Customer Journey Analytics {#cja}

In [!DNL Adobe Customer Journey Analytics]，则天气数据可在数据流中指定的数据集中使用。 只要天气属性为 [已添加到您的架构](#prerequisites-prerequisites)，它们将可用于 [添加到数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) 在 [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

天气数据可在 [Real-time Customer Data Platform](../../../rtcdp/overview.md)，以便在区段中使用。 天气数据会附加到事件。

![显示天气事件的区段生成器](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

由于天气条件经常变化，因此Adobe建议您在区段上设置时间限制，如上面的示例所示。 在最后一天或两天寒冷一天比六个月前寒冷一天的影响要大得多。

请参阅 [天气参考](weather-reference.md) 以获取可用字段。

### Adobe Target {#target}

In [!DNL Adobe Target]，您可以使用天气数据实时推动个性化。 天气数据传递到 [!DNL Target] 作为 [!UICONTROL mBox] 参数，您可以通过自定义 [!UICONTROL mBox] 参数。

![Target受众生成器](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

参数为 [!DNL XDM] 特定字段的路径。 请参阅 [天气参考](weather-reference.md) 的字段及其相应路径。

## 后续步骤 {#next-steps}

在阅读本文档后，您现在可以更好地了解如何跨各种Adobe解决方案使用天气数据。 要了解有关天气数据字段映射的更多信息，请参阅 [字段映射引用](weather-reference.md).
