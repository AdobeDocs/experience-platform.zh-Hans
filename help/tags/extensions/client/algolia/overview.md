---
title: Algolia标记扩展概述
description: 了解Adobe Experience Platform中的Algolia Tags扩展。
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 1%

---

# [!DNL Algolia]标记扩展概述

[!DNL Algolia] Tags扩展使营销人员能够轻松设置规则以将用户交互数据发送到[!DNL Algolia]，从而帮助您提供更加个性化的AI搜索和发现体验。

此扩展由一项关键功能提供支持：

* **[!DNL Algolia]分析**：自动捕获用户交互事件并将其发送到[!DNL Algolia]，这可以实现强大的分析、个性化体验和改进的搜索相关性。

## 先决条件 {#prerequisites}

您必须拥有有效的[!DNL Algolia]帐户才能使用此扩展。 转到[[!DNL Algolia] 注册页面](https://dashboard.algolia.com/users/sign_up)创建帐户（如果尚未创建）。

### 收集所需的配置详细信息 {#configuration-details}

要将[!DNL Algolia]与Adobe Experience Platform连接，您需要以下信息：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 应用程序Id | 您的应用程序ID可在[仪表板的](https://www.algolia.com/account/api-keys/all)API密钥[!DNL Algolia]部分找到。 | 0ABCDEFG12 |
| 搜索API密钥 | 可在[仪表板的](https://www.algolia.com/account/api-keys/all)API密钥[!DNL Algolia]部分中找到您的搜索API密钥。 | 1234a12345678901b1234567890c1ab1 |

## 安装和配置[!DNL Algolia] Insights扩展 {#install-configure}

要安装[!DNL Algolia] Insights扩展，请导航到[!UICONTROL Data Collection UI]，然后从左侧导航中选择&#x200B;**[!UICONTROL Tags]**。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 搜索[!DNL Algolia]分析卡，然后选择&#x200B;**[!UICONTROL Install]**。

![](../../../images/extensions/client/algolia/install.png)

在显示的配置视图中，必须提供以下详细信息：

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Application ID] | 输入您之前在[!UICONTROL Application Id]配置详细信息[部分中收集的](#configuration-details)。 |
| [!UICONTROL Search API Key] | 输入您之前在[!UICONTROL Search API Key]配置详细信息[部分中收集的](#configuration-details)。 |
| [!UICONTROL Index Name] | [!UICONTROL Index Name]包含产品或内容。  此索引将用作默认索引。 |
| [!UICONTROL User Token Data Element] | 将返回用户令牌的数据元素。 |
| [!UICONTROL Authenticated User Token Data Element] | 设置将返回经过身份验证的用户令牌的数据元素。 |
| [!UICONTROL Currency Code] | 以ISO-4217格式输入货币代码，如USD或EUR。 此字段支持数据元素。 |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia] Insights扩展操作类型 {#action-types}

[!DNL Algolia]支持一组预定义的标准事件，每个事件都具有特定的上下文和属性。 [!DNL Algolia]扩展中可用的操作与这些事件类型一致，从而可轻松根据发送给[!DNL Algolia]的事件类型分类和配置这些事件。

### 加载分析 {#load-insights}

>[!NOTE]
>
>在大多数情况下，建议在您的网站的每个页面上加载[!DNL Algolia]分析。

根据规则的上下文将&#x200B;**[!UICONTROL Load Insights]**&#x200B;操作添加到最适合加载[!DNL Algolia]分析的标记规则中。 此操作将`search-insights.js`库加载到页面上。

创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Load Insights]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Insight Library Version] | [!DNL Algolia]分析版本。 默认值为 `2.17.3`。 |
| [!UICONTROL User Opt Out Data Element] | 捕获用户的跟踪首选项的数据元素。 |
| [!UICONTROL Use User Token Cookie] | 选中此框以允许[!DNL Algolia]生成用户令牌Cookie。 默认情况下，此选项设置为`true`。 |

![](../../../images/extensions/client/algolia/load-insights.png)

### 已单击 {#clicked}

将&#x200B;**[!UICONTROL Click]**&#x200B;操作添加到您的标记规则以将点击事件发送到[!DNL Algolia]。 创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Clicked]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Event Name] | 事件名称，可用于进一步细化此点击事件。 |
| [!UICONTROL Event Details Data Element] | 数据元素以JSON格式返回事件详细信息，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` （可选）</li><li>`positions` （可选）</li><li>`price` （可选）</li><li>`quantity` （可选）</li><li>`discount` （可选）</li><li>`objectData` （可选）</li><li>`currency` （可选）</li></ul> |


>[!NOTE]
>
>如果同时包括`queryID`和`positions`，则该事件在搜索&#x200B;**后将被分类为**&#x200B;已点击对象ID。 否则，它被分类为&#x200B;**点击的对象ID**&#x200B;事件。
><br>
>如果数据元素不提供`indexName`，则在发送事件时将使用&#x200B;**默认索引名称**。

![](../../../images/extensions/client/algolia/clicked.png)

有关事件类别的详细信息，请参阅搜索后的[点击对象ID](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
和[已单击对象ID](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/)参考线。

### 已转换 {#converted}

将&#x200B;**[!UICONTROL Converted]**&#x200B;操作添加到您的标记规则以将转换的事件发送到[!DNL Algolia]。 创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Converted]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Event Name] | 将用于进一步细化此&#x200B;**转换**&#x200B;事件的事件名称。 |
| [!UICONTROL Event Details Data Element] | 数据元素返回事件详细信息，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` （可选）</li><li>`recordID` （可选）</li></ul> |

>[!NOTE]
>
>如果数据元素包含`queryId`，则将该事件分类为&#x200B;**Converted after Search**。 否则，它将被分类为&#x200B;**转化的**&#x200B;事件。
><br>
>如果数据元素不提供`indexName`，则在发送事件时将使用&#x200B;**默认索引名称**。

![](../../../images/extensions/client/algolia/converted.png)

有关事件类别的详细信息，请参阅搜索[转换后的对象ID](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/)和[转换后的对象ID](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/)指南。

### 已添加到购物车 {#added-to-cart}

将&#x200B;**[!UICONTROL Added to Cart]**&#x200B;操作添加到您的标记规则，以将添加到购物车事件的内容发送至[!DNL Algolia]。 创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Added to cart]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Event Name] | 将用于进一步细化此&#x200B;**添加到购物车**&#x200B;事件的事件名称。 |
| [!UICONTROL Event Details Data Element] | 数据元素以JSON格式返回事件详细信息，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` （可选）</li><li>`queryID` （可选）</li><li>`currency` （可选）</li></ul>。 |

>[!NOTE]
>
>如果数据元素包含`queryId`，则该事件将被分类为&#x200B;**已添加到购物车对象ID（在搜索**&#x200B;之后）。 否则，它将被分类为&#x200B;**添加到购物车对象ID**&#x200B;事件。
><br>
>如果数据元素不提供`indexName`，则在发送事件时将使用&#x200B;**默认索引名称**。
><br>
>如果默认数据元素不符合您的要求，可以创建自定义一个数据元素以返回所需的事件详细信息。

![](../../../images/extensions/client/algolia/added-to-cart.png)

有关事件类别的详细信息，请参阅[在搜索后添加到购物车对象ID](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/)和[添加到购物车对象ID](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/)指南。

### 已购买 {#purchased}

将&#x200B;**[!UICONTROL Purchased]**&#x200B;操作添加到您的标记规则以将已购买的事件发送到[!DNL Algolia]。 创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Purchased]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Event Name] | 将用于进一步细化此&#x200B;**购买**&#x200B;事件的事件名称。 |
| [!UICONTROL Event Details Data Element] | 数据元素以JSON格式返回事件详细信息，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` （可选）</li><li>`queryID` （可选）</li><li>`currency` （可选）</li></ul>。 |

>[!NOTE]
>
>Purchased操作根据购买的项目ID从浏览器存储中检索事件数据。 如果任何购买的项目在其存储的数据中包含`queryID`，则该事件在搜索&#x200B;**后将被分类为**&#x200B;购买的对象ID。 否则，它将被分类为&#x200B;**购买的对象ID**&#x200B;事件。
><br>
>此方法允许购买事件自动包含用户之前与项目交互的所有相关上下文（查询ID、索引名称、价格、数量、折扣）。

![](../../../images/extensions/client/algolia/purchased.png)

有关事件类别的详细信息，请参阅搜索后的[购买对象ID](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
和[已购买对象ID](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/)指南。

### 已查看 {#viewed}

将&#x200B;**[!UICONTROL Viewed]**&#x200B;操作添加到您的标记规则以将已购买的事件发送到[!DNL Algolia]。 创建新标记规则或打开现有标记规则。 根据您的要求定义条件，然后选择&#x200B;**[!UICONTROL Algolia]**&#x200B;作为[!UICONTROL Extension]，选择&#x200B;**[!UICONTROL Viewed]**&#x200B;作为[!UICONTROL Action Type]。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Event Name] | 将用于进一步细化此&#x200B;**视图**&#x200B;事件的事件名称。 |
| [!UICONTROL Event Details Data Element] | 数据元素以JSON格式返回事件详细信息，包括： <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>如果数据元素不提供`indexName`，则在发送事件时将使用&#x200B;**默认索引名称**。

![](../../../images/extensions/client/algolia/viewed.png)

有关查看事件的详细信息，请参阅[已查看对象ID](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/)指南。

## [!DNL Algolia]个Insights扩展数据元素 {#data-elements}

[!DNL Algolia]支持一组预定义的数据元素，每个元素都具有特定的上下文和属性。 以下部分介绍了[!DNL Algolia] Insights扩展中可用的数据元素。

### 数据集 {#dataset}

数据集数据元素检索与HTML元素关联的数据，然后这些数据用于[!DNL Algolia]操作。 此数据元素会自动将检索到的事件数据存储在浏览器存储中，以供以后使用（例如在转化或购买事件中）。

**常规配置：**

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | 包含数据集属性的HTML元素名称和/或CSS类名称，这些数据集属性包括HTML元素上的`data-insights-object-id`以及可选的`data-insights-query-id`和`data-insights-position`。 |
| [!UICONTROL Index Name Element Div/Class Name] | 在HTML元素上具有数据集属性(`data-indexname`)的HTML元素名称和/或CSS类名称。 |

**Commerce配置（可选）：**

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Price Data Element] | 返回项目价格的数据元素。 如果提供，这将包含在存储的商业事件事件数据中。 |
| [!UICONTROL Quantity Data Element] | 返回项目数量的数据元素。 如果未提供，则默认为1。 |
| [!UICONTROL Discount Data Element] | 返回项目的折扣小数值的数据元素。 |
| [!UICONTROL Currency Code] | ISO-4217格式的货币代码。 如果未指定货币代码，则将使用扩展配置中的默认货币。 |

**覆盖（可选）：**

这些字段允许您覆盖从HTML数据集属性检索数据的默认行为。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 覆盖使用页面URL作为记录ID的默认方法。 记录ID用于存储和查找要发送到此产品/页面的[!DNL Algolia]的数据。 |
| [!UICONTROL Query ID Data Element] | 查询ID是从HTML元素上的数据集中检索的。 要覆盖此行为，请使用此属性提供将查询ID作为字符串返回的数据元素。 |
| [!UICONTROL Object IDs Data Element] | 从HTML元素上的数据集中检索对象ID。 要覆盖此行为，请使用此属性提供一个数据元素，该数据元素将对象ID作为数组返回。 |
| [!UICONTROL Positions Data Element] | 从HTML元素上的数据集中检索位置。 要覆盖此行为，请使用此属性提供一个数据元素，该数据元素会将Positions作为数组返回。 |
| [!UICONTROL Index Name Data Element] | 索引名称是从HTML元素上的数据集中检索的。 要覆盖此行为，请使用此属性提供一个数据元素，该数据元素将作为字符串返回索引名称。 |

![](../../../images/extensions/client/algolia/dataset.png)

此数据元素返回：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
}
```

包含数据集的HTML示例：

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### 查询字符串 {#query-string}

查询字符串数据元素从[!DNL Algolia]操作中使用的URL查询字符串中提取数据。

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Object ID Param Name] | 包含对象ID的查询参数名称。 |
| [!UICONTROL Index Name Param Name] | 包含“索引名称”的查询参数名称。 |
| [!UICONTROL Query ID Param Name] | 包含查询ID的查询参数名称。 |
| [!UICONTROL Position Param Name] | 包含职位的查询参数名称。 |

![](../../../images/extensions/client/algolia/query-string.png)

此数据元素返回：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions
}
```

包含查询参数的HTML示例：

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### 存储 {#storage}

存储数据元素从浏览器会话存储中检索数据以用于[!DNL Algolia]操作。 此数据元素还可用于使用其他商业信息补充存储的数据。

此数据元素检索之前存储在会话存储中的事件详细信息（通常在点击事件期间由数据集数据元素存储）。 除非明确禁用数据删除，否则数据将在转换事件期间自动删除。

**覆盖（可选）：**

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 记录ID用作查找存储在浏览器存储中的事件数据的键。 页面URL是默认的记录ID。 要覆盖此行为，请使用此属性提供以字符串形式返回记录ID的数据元素。 |
| [!UICONTROL Price Data Element] | 返回项目价格的数据元素。 如果提供，这将会用价格信息更新存储的事件数据。 |
| [!UICONTROL Quantity Data Element] | 返回项目数量的数据元素。 如果提供，这将使用数量信息更新存储的事件数据。 |
| [!UICONTROL Discount Data Element] | 返回项目的折扣小数值的数据元素。 如果提供，这将使用折扣信息更新存储的事件数据。 |
| [!UICONTROL Currency Code] | 以ISO-4217格式输入货币代码。 如果提供，这将使用货币信息更新存储的事件数据。 |

![](../../../images/extensions/client/algolia/storage.png)

此数据元素返回会话存储中存储的内容，包括任何增强的商务数据：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## 搜索后已单击或已转换 {#clicked-converted-after-search}

搜索&#x200B;*后点击的*&#x200B;或搜索&#x200B;*后转换的*&#x200B;事件需要`queryID`，搜索`positions`后点击的&#x200B;*也需要*。 在InstantSearch和/或自动完成查询参数中启用`insights`标志时，这些属性可用。 请参阅以下资源，了解如何为网站配置Insights：

* [在自动完成时设置分析](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [在InstantSearch.js中设置分析](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [点击和转化事件入门](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [正在发送 [!DNL Algolia] 分析事件](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Launch扩展GitHub存储库](https://github.com/algolia/algolia-launch-extension)
* [InstantSearch.js文档](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] 分析API文档](https://www.algolia.com/doc/rest-api/insights/)
* [Algolia Launch扩展代码存储库](https://github.com/algolia/algolia-launch-extension)

## 后续步骤 {#next-steps}

本指南介绍了如何使用[!DNL Algolia]标记扩展将数据发送到[!DNL Algolia Insights]。 如果您还计划向[!DNL Algolia]发送服务器端事件，则现在可以继续安装和配置[[!DNL Conversions API] 事件转发扩展](../../server/algolia/overview.md)。

有关Experience Platform中标记的详细信息，请参阅[标记概述](../../../home.md)。
