---
description: 了解如何为使用Destination SDK构建的目标配置受众元数据设置。
title: 受众元数据配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# 受众元数据配置

将数据从Experience Platform导出到目标时，您可能需要在Experience Platform和目标之间共享特定受众元数据，例如区段名称或区段ID。

Destination SDK提供了一些工具，您可以使用这些工具以编程方式创建、更新或删除目标平台中的受众。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅 [配置选项](../configuration-options.md) 文档或参阅指南，了解如何 [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以通过以下方式配置受众元数据模板 `/authoring/audience-templates` 端点。 创建受众元数据配置后，您可以使用 `/authoring/destinations` 端点以配置 `audienceMetadataConfig` 部分。 此部分将向您的目标说明它应该映射到受众模板的区段元数据。

有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [创建受众模板](../../metadata-api/create-audience-template.md)
* [更新受众模板](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 支持的参数 {#supported-parameters}

在创建受众元数据配置时，您可以使用下表所述的参数来配置区段映射设置。

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布尔值 | 指示是否 [[!UICONTROL 映射Id]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目标激活工作流中的值应为Experience Platform区段名称。 |
| `mapExperiencePlatformSegmentId` | 布尔值 | 指示是否 [[!UICONTROL 映射Id]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目标激活工作流中的值应为Experience Platform区段ID。 |
| `mapUserInput` | 布尔值 | 启用或禁用以下项的用户输入 [[!UICONTROL 映射Id]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目标激活工作流中的值。 如果设置为 `true`， `audienceTemplateId` 不存在。 |
| `audienceTemplateId` | 布尔值 | 此 `instanceId` 的 [受众元数据模板](../../metadata-api/create-audience-template.md) 用于您的目标。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为目标配置受众元数据。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证配置](customer-authentication.md)
* [OAuth2身份验证](oauth2-authentication.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)