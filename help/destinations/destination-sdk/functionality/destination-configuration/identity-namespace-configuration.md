---
description: 了解如何为使用Destination SDK构建的目标配置支持的目标身份。
title: 身份命名空间配置
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 3%

---

# 身份命名空间配置

Experience Platform使用身份命名空间来描述特定身份的类型。 例如，名为`Email`的标识命名空间将诸如`name@email.com`之类的值标识为电子邮件地址。

根据您创建的目标类型（流或基于文件），请牢记以下身份命名空间要求：

* 在通过Destination SDK创建实时（流）目标时，除了[配置用户可将配置文件属性和身份映射到的合作伙伴架构](schema-configuration.md)之外，还必须定义目标平台支持的至少&#x200B;*个*&#x200B;身份命名空间。 例如，如果您的目标平台接受经过哈希处理的电子邮件和[!DNL IDFA]，则必须将这两个标识定义为此文档](#supported-parameters)中进一步描述的[。

  >[!IMPORTANT]
  >
  >将受众激活到流式目标时，除了目标配置文件属性外，用户还必须映射&#x200B;_至少一个目标身份_。 否则，受众将不会激活到目标平台。

* 通过Destination SDK创建基于文件的目标时，身份命名空间的配置是&#x200B;_可选_。

要详细了解Experience Platform中的身份命名空间，请参阅[身份命名空间文档](../../../../identity-service/features/namespaces.md)。

在为目标配置身份命名空间时，可以优化目标支持的目标身份映射，例如：

* 允许用户将XDM属性映射到身份命名空间。
* 允许用户将[标准身份命名空间](../../../../identity-service/features/namespaces.md#standard)映射到您自己的身份命名空间。
* 允许用户将[自定义身份命名空间](../../../../identity-service/features/namespaces.md#manage-namespaces)映射到您自己的身份命名空间。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图，或参阅如何[使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)的指南。

您可以通过`/authoring/destinations`端点配置支持的身份命名空间。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的身份命名空间配置选项，并显示客户将在Experience Platform UI中看到的内容。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是（必需） |
| 基于文件（批处理）的集成 | 是（可选） |

## 支持的参数 {#supported-parameters}

在定义目标支持的目标身份时，您可以使用下表所述的参数配置其行为。

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|---|------|
| `acceptsAttributes` | 布尔值 | 可选 | 指示客户是否可以将标准配置文件属性映射到您配置的身份。 |
| `acceptsCustomNamespaces` | 布尔值 | 可选 | 指示客户是否可以将自定义身份命名空间映射到您配置的身份命名空间。 |
| `acceptedGlobalNamespaces` | - | 可选 | 指示客户可以将哪些[标准身份命名空间](../../../../identity-service/features/namespaces.md#standard)（例如[!UICONTROL IDFA]）映射到您正在配置的身份。 |
| `transformation` | 字符串 | 可选 | 当源字段是XDM属性或自定义身份命名空间时，在Experience Platform UI中显示[[!UICONTROL 应用转换]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)复选框。 使用此选项可让用户在导出时散列源属性。 要启用此选项，请将值设置为`sha256(lower($))`。 |
| `requiredTransformation` | 字符串 | 可选 | 当客户选择此源身份命名空间时，[[!UICONTROL 应用转换]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)复选框将自动应用于映射，客户无法禁用它。 要启用此选项，请将值设置为`sha256(lower($))`。 |

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

您必须指定客户能够导出到目标的[!DNL Experience Platform]身份。 例如，[!DNL Experience Cloud ID]、经过哈希处理的电子邮件、设备ID ([!DNL IDFA]、[!DNL GAID])。 这些值是[!DNL Experience Platform]个身份命名空间，客户可以从目标映射到身份命名空间。

身份命名空间不要求[!DNL Experience Platform]与您的目标之间有一对一的对应关系。
例如，客户可以将[!DNL Experience Platform] [!DNL IDFA]命名空间映射到目标中的[!DNL IDFA]命名空间，也可以将相同的[!DNL Experience Platform] [!DNL IDFA]命名空间映射到目标中的[!DNL Customer ID]命名空间。

有关[身份命名空间概述](../../../../identity-service/features/namespaces.md)中身份的详细信息。

## 映射注意事项

如果客户选择了源身份命名空间但未选择目标映射，则Experience Platform会自动使用具有相同名称的属性填充目标映射。

## 配置可选源字段散列

Experience Platform客户可以选择以哈希格式或纯文本将数据摄取到Experience Platform中。 如果您的目标平台同时接受经过哈希处理和未哈希处理的数据，则可以让客户自行选择在源字段值导出到目标时，Experience Platform是否应对其进行哈希处理。

下面的配置在映射步骤中启用了Experience Platform UI中的可选[应用转换](../../../ui/activate-segment-streaming-destinations.md#apply-transformation)选项。

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

将未经过哈希处理的源属性映射到目标期望进行哈希处理的目标属性时（例如： `email_lc_sha256`或`phone_sha256`），请选中&#x200B;**应用转换**&#x200B;选项，以使Adobe Experience Platform在激活时自动对源属性进行哈希处理。

## 配置强制源字段散列

如果您的目标仅接受哈希数据，则可以配置导出的属性，以使其由Experience Platform自动进行哈希处理。 在映射`Email`和`Phone`标识时，以下配置会自动检查&#x200B;**应用转换**&#x200B;选项。

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
* [OAuth2授权](oauth2-authorization.md)
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
