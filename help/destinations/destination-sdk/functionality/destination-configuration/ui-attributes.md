---
description: 了解如何为使用Destination SDK构建的目标配置UI属性，如文档链接、目标卡类别以及目标连接类型和频率。
title: UI属性
exl-id: aed8d868-c516-45da-b224-c7e99e4bfaf1
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# UI属性

UI属性定义Adobe应在Adobe Experience Platform用户界面中为目标卡显示的可视化元素，例如目标平台徽标、指向文档页面的链接、目标描述及其类别和类型。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅中的图表 [配置选项](../configuration-options.md) 文档或参阅以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

时间 [创建目标](../../authoring-api/destination-configuration/create-destination-configuration.md) 通过Destination SDK， `uiAttributes` 部分定义目标卡的以下可视属性：

* 您的目标文档页面的URL，位于 [目标目录](../../../catalog/overview.md).
* 您托管要在目标目录信息卡中显示的图标的URL。
* 您的目标将显示在Platform UI中的类别。
* 目标的数据导出频率。
* 目标连接类型，如Amazon S3、Azure Blob等。

您可以通过以下方式配置UI属性 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的UI属性，并显示了客户将在Experience PlatformUI中看到的内容。

![显示Experience Platform界面中UI属性的用户界面屏幕截图](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 支持的参数 {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` 是一个字符串参数，它引用 [目标目录](../../../catalog/overview.md) 到你的目的地去。 Adobe Experience Platform中的每个产品化目标都必须具有相应的文档页面。 [了解如何创建目标文档页面](../../docs-framework/documentation-instructions.md) 到你的目的地去。 请注意，私有/自定义目标不需要此项。

使用以下格式： `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是目标的名称。 对于名为Moviestar的目标，您可以使用 `http://www.adobe.com/go/destinations-moviestar-en`.

用户可以从UI中的目标目录页面查看和访问您的文档链接。 他们需要浏览到您的目标卡，然后选择 **[!UICONTROL 更多操作]**，然后 **[!UICONTROL 查看文档]**，如下图所示。

![显示文档链接位置的UI图像。](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>此链接仅在Adobe将您的目标设置为实时状态并发布文档后生效。

### `category` {#category}

`category` 是一个字符串参数，引用在Adobe Experience Platform中分配给目标的类别。 有关详细信息，请阅读 [目标类别](../../../destination-types.md). 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

用户可以在目标目录的屏幕左侧看到目标类别的列表，如下图所示。

![显示目标类别位置的UI图像。](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` 是一个字符串参数，它根据目标来引用连接的类型。 支持的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

用户可以在以下位置查看目标连接类型： [浏览](../../../ui/destinations-workspace.md#browse) 目标工作区的选项卡。

![显示UI中连接类型位置的UI图像。](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` 是一个字符串参数，引用您的目标支持的数据导出类型。 设置为 `Streaming` 对于基于API的集成，或者 `Batch` 将文件导出到目标时。

用户可以在以下位置查看频率类型： **[!UICONTROL 数据流运行]** 每个目标连接的页面。

![显示UI中频率类型位置的UI图像。](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

如果通过Destination SDK创建的目标可供有限数量的客户使用，您可能需要将目标目录中的目标卡标记为测试版。

为此，您可以使用 `isBeta: "true"` 目标配置的UI属性部分中的参数，用于正确标记目标卡。

![显示标记为Beta版的目标卡片的UI图像。](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## 后续步骤 {#next-steps}

阅读本文后，您应该能够更好地了解可以为目标配置哪些UI属性，以及用户将在Platform UI中的何处看到这些属性。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [客户数据字段](customer-data-fields.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
