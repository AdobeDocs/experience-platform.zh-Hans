---
title: 使用来自DNL The Weather Channel的天气数据
description: 使用DNL The Weather Channel中的天气数据来增强您通过数据流收集的数据。
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# 使用来自的天气数据 [!DNL The Weather Channel]

Adobe与 [!DNL [The Weather Company]](https://www.ibm.com/weather) 为通过数据流收集的数据带来美国天气的额外背景。 您可以将此数据用于分析、定位和区段创建中的Experience Platform。

有3种类型的数据可从 [!DNL The Weather Channel]:

* **[!UICONTROL 当前天气]**:用户的当前天气条件（基于其位置）。 这包括当前温度、枕头、云覆盖等。
* **[!UICONTROL 预测天气]**:预测包括用户地点的1、2、3、5、7和10天预测。
* **[!UICONTROL 触发器]**:触发器是映射到不同语义天气条件的特定组合。 天气触发器有三种类型：

   * **[!UICONTROL 天气触发器]**:语义上有意义的条件，如寒冷或雨天。 这些气候在不同气候中的定义可能不同。
   * **[!UICONTROL 产品触发器]**:导致购买不同类型产品的条件。 例如：天气预报可能意味着更有可能购买雨衣。
   * **[!UICONTROL 恶劣天气触发]**:严重的天气警告，如冬季风暴或飓风警告。

## 先决条件 {#prerequisites}

在使用天气数据之前，请确保满足以下先决条件：

* 您必须从 [!DNL The Weather Channel]. 然后，他们将在您的帐户上启用该功能。
* 天气数据仅通过数据流提供。 要使用天气数据，您必须使用 [!DNL Web SDK], [!DNL Mobile Edge Extension] 或 [服务器API](../../../server-api/overview.md) 来利用此数据。
* 您的数据流必须具有 [[!UICONTROL 地理位置]](../configure.md#advanced-options) 已启用。
* 添加 [气象组](#schema-configuration) 到您所使用的架构。

## 配置中 {#provisioning}

在您从 [!DNL The Weather Channel]，则会允许您的帐户访问数据。 接下来，您必须联系Adobe客户关怀团队，以在您的数据流中启用数据。 启用后，将自动附加数据。

您可以通过以下方法验证添加的点击：通过调试器运行边缘跟踪，或使用“保证”跟踪通过 [!DNL Edge Network].

### 架构配置 {#schema-configuration}

您必须将天气字段组添加到与您在数据流中使用的事件数据集对应的Experience Platform架构中。 有五个可用的字段组：

* [!UICONTROL 预测天气]
* [!UICONTROL 当前天气]
* [!UICONTROL 产品触发器]
* [!UICONTROL 相对触发器]
* [!UICONTROL 恶劣天气触发]

## 访问天气数据 {#access-weather-data}

在您的数据获得授权并可用后，您便可以在Adobe服务中以各种方式访问它。

### Adobe Analytics {#analytics}

在 [!DNL Adobe Analytics]，则可以通过处理规则以及 [!DNL XDM] 架构。

您可以在 [天气参考](weather-reference.md) 页面。 与所有 [!DNL XDM] 模式，键的前缀为 `a.x`. 例如，名为 `weather.current.temperature.farenheit` 会出现在 [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![处理规则界面](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### 了解 Adobe Customer Journey Analytics {#cja}

在 [!DNL Adobe Customer Journey Analytics]，则天气数据在数据流中指定的数据集中可用。 只要天气属性 [已添加到您的架构](#prerequisites-prerequisites)，则它们将可用于 [添加到数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

天气数据可在 [Real-time Customer Data Platform](../../../rtcdp/overview.md)，以在区段中使用。 天气数据会附加到事件。

![显示天气事件的区段生成器](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

由于天气条件经常更改，因此Adobe建议您对区段设置时间限制，如上面的示例所示。 与6个月前的寒冷日相比，在最后一两天里过冷日更有影响力。

请参阅 [天气参考](weather-reference.md) 的双曲余切值。

### Adobe Target {#target}

在 [!DNL Adobe Target]，则可以使用天气数据推动实时个性化。 天气数据将传递到 [!DNL Target] as [!UICONTROL mBox] 参数，您可以通过自定义 [!UICONTROL mBox] 参数。

![Target受众生成器](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

参数为 [!DNL XDM] 特定字段的路径。 请参阅 [天气参考](weather-reference.md) ，用于可用字段及其相应路径。

## 后续步骤 {#next-steps}

在阅读本文档后，您现在可以更好地了解如何在各种Adobe解决方案中使用天气数据。 要了解有关天气数据字段映射的更多信息，请参阅 [字段映射引用](weather-reference.md).