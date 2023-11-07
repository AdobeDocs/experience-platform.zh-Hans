---
description: 了解如何为使用Destination SDK构建的目标配置支持的目标身份。
title: 身份命名空间配置
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# 身份命名空间配置

Experience Platform使用身份命名空间来描述特定身份的类型。 例如，名为的身份命名空间 `Email` 标识如下值 `name@email.com` 作为电子邮件地址。

通过Destination SDK创建目标时，除了 [配置合作伙伴架构](schema-configuration.md) 用户可以将配置文件属性和身份映射到，您还可以定义目标平台支持的身份命名空间。

在执行此操作时，用户除了可以选择目标配置文件属性之外，还可以选择目标身份。

要详细了解Experience Platform中的身份命名空间，请参阅 [身份命名空间文档](../../../../identity-service/namespaces.md).

在为目标配置身份命名空间时，可以优化目标支持的目标身份映射，例如：

* 允许用户将XDM属性映射到身份命名空间。
* 允许用户映射 [标准身份命名空间](../../../../identity-service/namespaces.md#standard) 到您自己的身份命名空间。
* 允许用户映射 [自定义身份命名空间](../../../../identity-service/namespaces.md#manage-namespaces) 到您自己的身份命名空间。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅中的图表 [配置选项](../configuration-options.md) 文档或参阅指南，了解如何 [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以通过以下方式配置支持的身份命名空间： `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的身份命名空间配置选项，并显示客户将在Platform UI中看到的内容。

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

在定义目标支持的目标身份时，您可以使用下表所述的参数配置其行为。

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|---|------|
| `acceptsAttributes` | 布尔值 | 可选 | 指示客户是否可以将标准配置文件属性映射到您配置的身份。 |
| `acceptsCustomNamespaces` | 布尔值 | 可选 | 指示客户是否可以将自定义身份命名空间映射到您配置的身份命名空间。 |
| `acceptedGlobalNamespaces` | - | 可选 | 指示哪些 [标准身份命名空间](../../../../identity-service/namespaces.md#standard) (例如， [!UICONTROL IDFA])客户可以映射到您正在配置的身份。 |
| `transformation` | 字符串 | 可选 | 显示 [[!UICONTROL 应用转换]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 如果源字段是XDM属性或自定义身份命名空间，请选中Platform UI中的复选框。 使用此选项可让用户在导出时散列源属性。 要启用此选项，请将值设置为 `sha256(lower($))`. |
| `requiredTransformation` | 字符串 | 可选 | 当客户选择此源身份命名空间时， [[!UICONTROL 应用转换]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 复选框会自动应用于映射，而客户无法禁用它。 要启用此选项，请将值设置为 `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

您必须指明哪个 [!DNL Platform] 客户能够导出到目标的身份。 一些示例包括 [!DNL Experience Cloud ID]，经过哈希处理的电子邮件，设备ID ([!DNL IDFA]， [!DNL GAID])。 这些值为 [!DNL Platform] 客户可以映射到目标中的身份命名空间的身份命名空间。

身份命名空间不需要在 [!DNL Platform] 还有你的目的地。
例如，客户可以映射 [!DNL Platform] [!DNL IDFA] 命名空间更改为 [!DNL IDFA] 命名空间中的其他位置，或者他们可以映射相同的 [!DNL Platform] [!DNL IDFA] 命名空间更改为 [!DNL Customer ID] 命名空间中指定目标的URL。

有关身份的详细信息，请参阅 [身份命名空间概述](../../../../identity-service/namespaces.md).

## 映射注意事项

如果客户选择了源身份命名空间但未选择目标映射，则Platform会自动使用具有相同名称的属性填充目标映射。

## 配置可选源字段散列

Experience Platform客户可以选择以哈希格式或纯文本格式将数据摄取到Platform中。 如果您的目标平台接受经过哈希处理的数据和未经过哈希处理的数据，则可以让客户选择在将源字段值导出到目标时，Platform是否应对其进行哈希处理。

下面的配置启用可选的 [应用转换](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 选项，位于Platform UI的“映射”步骤中。

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

使用未进行哈希处理的源字段时选中此选项，让 Adobe Experience Platform 在激活时自动对它们进行哈希处理。

将未经过哈希处理的源属性映射到目标期望进行哈希处理的目标属性时(例如： `email_lc_sha256` 或 `phone_sha256`)，检查 **应用转换** 用于使Adobe Experience Platform在激活时自动哈希源属性的选项。

## 配置强制源字段散列

如果您的目标仅接受哈希数据，则可以配置导出的属性，使其由Platform自动进行哈希处理。 以下配置会自动检查 **应用转换** 选项，当 `Email` 和 `Phone` 标识已映射。

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为使用Destination SDK构建的目标配置身份命名空间。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2身份验证](oauth2-authorization.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
