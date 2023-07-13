---
solution: Experience Platform
title: 导入和使用外部受众
description: 阅读本教程，了解如何在Adobe Experience Platform中使用外部受众。
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 0%

---

# 导入和使用外部受众

>[!IMPORTANT]
>
>此文档包含来自受众文档早期版本的信息，因此已过期。

Adobe Experience Platform支持导入外部受众的功能，该受众随后可用作新受众的组件。 本文档提供了有关设置Experience Platform以导入和使用外部受众的教程。

## 快速入门

本教程需要对各种 [!DNL Adobe Experience Platform] 创建受众时涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [分段服务](../home.md)：用于根据实时客户档案数据构建受众。
- [Real-time Customer Profile](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [体验数据模型(XDM)](../../xdm/home.md)：Platform用于组织客户体验数据的标准化框架。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../../xdm/schema/best-practices.md).
- [数据集](../../catalog/datasets/overview.md)：用于Experience Platform中数据持久化的存储和管理结构。
- [流式摄取](../../ingestion/streaming-ingestion/overview.md)：Experience Platform如何实时从客户端和服务器端设备摄取和存储数据。

### 受众与区段定义

在开始导入和使用外部受众之前，请务必了解受众和区段定义之间的差异。

受众是指您尝试过滤的一组用户档案。 使用区段定义时，您可以通过创建区段定义来创建受众，该定义会将您的用户档案过滤到符合区段资格标准的子集。

区段定义包括名称、描述、表达式（如果适用）、创建日期、上次修改日期和ID等信息。 ID可将区段元数据链接到符合区段资格并属于生成受众的个别用户档案。

| 受众 | 区段定义 |
| --------- | ---------------- |
| 您正在尝试查找的一组配置文件。 使用区段定义时，这意味着它将是符合区段资格的一组用户档案。 | 一组规则，用于对所查找的受众进行分段。 |

## 为外部受众创建身份命名空间

使用外部受众的第一步是创建身份命名空间。 身份命名空间允许Platform关联受众源自何处。

要创建身份命名空间，请按照 [身份命名空间指南](../../identity-service/namespaces.md#manage-namespaces). 创建身份命名空间时，请将源详细信息添加到身份命名空间，并标记其 [!UICONTROL 类型] as a **[!UICONTROL 非人员标识符]**.

![非人员标识符在创建身份命名空间模式中突出显示。](../images/tutorials/external-audiences/identity-namespace-info.png)

## 为区段元数据创建架构

创建身份命名空间后，您需要为将创建的区段创建新架构。

要开始构成架构，请先选择 **[!UICONTROL 架构]** 左侧导航栏中，其后是 **[!UICONTROL 创建架构]** 位于架构工作区的右上角。 从此处选择 **[!UICONTROL 浏览]** 查看所有可用的架构类型。

![创建架构和浏览都会突出显示。](../images/tutorials/external-audiences/create-schema-browse.png)

由于您正在创建区段定义（一个预定义类），因此请选择 **[!UICONTROL 使用现有类]**. 现在，选择 **[!UICONTROL 区段定义]** 类，随后是 **[!UICONTROL 分配类]**.

![区段定义类会突出显示。](../images/tutorials/external-audiences/assign-class.png)

现在您的架构已创建，您将需要指定哪个字段将包含区段ID。 此字段应标记为主要身份，并分配给您之前创建的命名空间。

![架构编辑器中突出显示将选定字段标记为主要标识的复选框。](../images/tutorials/external-audiences/mark-primary-identifier.png)

标记 `_id` 字段作为主标识，选择架构的标题，然后选择标记为的切换 **[!UICONTROL 个人资料]**. 选择 **[!UICONTROL 启用]** 启用架构 [!DNL Real-Time Customer Profile].

![架构编辑器中会突出显示用于为配置文件启用架构的切换开关。](../images/tutorials/external-audiences/schema-profile.png)

现在，为配置文件启用此架构，并将主标识分配给您创建的非人员标识命名空间。 因此，这意味着使用此架构导入到Platform的区段元数据将被摄取到配置文件中，而不会与其他人员相关的配置文件数据合并。

## 为架构创建数据集

配置架构后，您将需要为区段元数据创建一个数据集。

要创建数据集，请按照 [数据集用户指南](../../catalog/datasets/user-guide.md#create). 您应遵循 **[!UICONTROL 从架构创建数据集]** 选项，使用您之前创建的架构。

![要作为数据集基础的架构会突出显示。](../images/tutorials/external-audiences/select-schema.png)

创建数据集后，请继续按照 [数据集用户指南](../../catalog/datasets/user-guide.md#enable-profile) 为实时客户档案启用此数据集。

![在“数据集”活动页面中，会突出显示为配置文件启用架构的切换开关。](../images/tutorials/external-audiences/dataset-profile.png)

## 设置和导入受众数据

启用数据集后，现在可以通过UI或使用Experience PlatformAPI将数据发送到Platform。 您可以通过批量连接或流连接摄取此数据。

### 使用批处理连接引入数据

要创建批处理连接，可以按照通用中的说明进行操作 [本地文件上传UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 有关可结合使用摄取数据的可用源的完整列表，请参阅 [源概述](../../sources/home.md).

### 使用流连接引入数据

要创建流连接，您可以按照 [api教程](../../sources/tutorials/api/create/streaming/http.md) 或 [用户界面教程](../../sources/tutorials/ui/create/streaming/http.md).

创建流连接后，您将有权访问可将数据发送到的唯一流端点。 要了解如何将数据发送到这些端点，请阅读 [有关流记录数据的教程](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![流连接的流端点会在源详细信息页面中突出显示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 受众元数据结构

创建连接后，您现在可以将数据摄取到Platform。

外部受众有效负载的元数据示例如下所示：

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef` | 架构 **必须** 请参阅之前为区段元数据创建的架构。 |
| `datasetId` | 数据集ID **必须** 请参阅之前为刚刚创建的架构创建的数据集。 |
| `xdmEntity._id` | ID **必须** 引用您用作外部受众的相同区段ID。 |
| `xdmEntity.identityMap` | 本节 **必须** 包含创建以前创建的命名空间时使用的身份标签。 |
| `{IDENTITY_NAMESPACE}` | 这是以前创建的身份命名空间的标签。 因此，例如，如果您将身份命名空间称为“externalAudience”，则可以将其用作数组的键。 |
| `segmentName` | 您希望外部受众作为分段的依据的区段名称。 |

## 使用导入的受众生成区段

设置导入的受众后，可在分段过程中使用这些受众。 要查找外部受众，请转到区段生成器，然后选择 **[!UICONTROL 受众]** 在中选项卡 **[!UICONTROL 字段]** 部分。

![区段生成器中的外部受众选择器会突出显示。](../images/tutorials/external-audiences/external-audiences.png)

## 后续步骤

现在，您可以在区段中使用外部受众，接下来可以使用区段生成器来创建区段。 要了解如何创建区段，请阅读 [有关创建区段的教程](./create-a-segment.md).

## 附录

除了使用导入的外部受众元数据并使用它们创建区段之外，您还可以将外部区段成员资格导入Platform。

### 设置外部区段成员资格目标架构

要开始构成架构，请先选择 **[!UICONTROL 架构]** 左侧导航栏中，其后是 **[!UICONTROL 创建架构]** 位于架构工作区的右上角。 从此处选择 **[!UICONTROL XDM个人资料]**.

![“XDM单个配置文件”区域会突出显示。](../images/tutorials/external-audiences/create-schema-profile.png)

现在已创建架构，您需要添加区段成员资格字段组作为架构的一部分。 要执行此操作，请选择 [!UICONTROL 区段成员资格详细信息]，后接 [!UICONTROL 添加字段组].

![区段成员资格详细信息字段组会突出显示。](../images/tutorials/external-audiences/segment-membership-details.png)

此外，请确保架构已标记为 **[!UICONTROL 个人资料]**. 要实现此目的，您需要将字段标记为主要标识。

![架构编辑器中会突出显示用于为配置文件启用架构的切换开关。](../images/tutorials/external-audiences/external-segment-profile.png)

### 设置数据集

创建架构后，您将需要创建一个数据集。

要创建数据集，请按照 [数据集用户指南](../../catalog/datasets/user-guide.md#create). 您应遵循 **[!UICONTROL 从架构创建数据集]** 选项，使用您之前创建的架构。

![用于创建数据库的模式会突出显示。](../images/tutorials/external-audiences/select-schema.png)

创建数据集后，请继续按照 [数据集用户指南](../../catalog/datasets/user-guide.md#enable-profile) 为实时客户档案启用此数据集。

![为配置文件启用架构的切换开关会在创建数据集工作流中突出显示。](../images/tutorials/external-audiences/dataset-profile.png)

## 设置和导入外部受众会员资格数据

启用数据集后，现在可以通过UI或使用Experience PlatformAPI将数据发送到Platform。 您可以通过批量连接或流连接摄取此数据。

### 使用批处理连接引入数据

要创建批处理连接，可以按照通用中的说明进行操作 [本地文件上传UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 有关可结合使用摄取数据的可用源的完整列表，请参阅 [源概述](../../sources/home.md).

### 使用流连接引入数据

要创建流连接，您可以按照 [api教程](../../sources/tutorials/api/create/streaming/http.md) 或 [用户界面教程](../../sources/tutorials/ui/create/streaming/http.md).

创建流连接后，您将有权访问可将数据发送到的唯一流端点。 要了解如何将数据发送到这些端点，请阅读 [有关流记录数据的教程](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![流连接的流端点会在源详细信息页面中突出显示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 区段成员资格结构

创建连接后，您现在可以将数据摄取到Platform。

外部受众成员资格有效负载的示例如下所示：

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef` | 架构 **必须** 有关区段成员资格数据，请参阅之前创建的架构。 |
| `datasetId` | 数据集ID **必须** 请参阅之前创建的数据集，了解您刚刚创建的成员资格架构。 |
| `xdmEntity._id` | 一个合适的ID，用于唯一标识数据集中的记录。 |
| `{TENANT_NAME}.identities` | 此部分用于将自定义标识的字段组与您之前导入的用户连接。 |
| `segmentMembership.{IDENTITY_NAMESPACE}` | 这是之前创建的自定义身份命名空间的标签。 因此，例如，如果您将身份命名空间称为“externalAudience”，则可以将其用作数组的键。 |

>[!NOTE]
>
>默认情况下，外部受众成员资格仅保留30天。 如要保留超过30天，请使用 `validUntil` 字段。 有关此字段的更多信息，请阅读 [区段成员资格详细信息架构字段组](../../xdm/field-groups/profile/segmentation.md).