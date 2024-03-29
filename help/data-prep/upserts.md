---
keywords: Experience Platform；主页；热门主题；数据准备；数据准备；流；更新插入；流更新插入
title: 使用数据准备将部分行更新发送到实时客户个人资料
description: 了解如何使用数据准备将部分行更新发送到Real-Time Customer Profile。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---

# 将部分行更新发送至 [!DNL Real-Time Customer Profile] 使用 [!DNL Data Prep]

>[!WARNING]
>
>已弃用通过DCS入口摄取用于配置文件更新的体验数据模型(XDM)实体更新消息(包含JSONPATCH操作)。 作为替代方法，您可以 [将原始数据摄取到DCS入口](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) 并指定必要的数据映射，以将您的数据转换为符合XDM标准的消息以进行配置文件更新。

流更新插入于 [!DNL Data Prep] 允许您将部分行更新发送到 [!DNL Real-Time Customer Profile] 数据，同时通过单个API请求创建和建立新的身份链接。

通过流式传输更新插入，您可以保留数据的格式，同时将数据转换为 [!DNL Real-Time Customer Profile] 摄取期间的PATCH请求。 根据您提供的输入， [!DNL Data Prep] 允许您发送单个API有效负载并将数据转换为两者 [!DNL Real-Time Customer Profile] PATCH和 [!DNL Identity Service] 创建请求。

>[!NOTE]
>
>要利用更新插入功能，建议您在数据摄取期间关闭与XDM兼容的配置，并使用重新映射传入有效负载 [数据准备映射器](./ui/mapping.md).

本文档提供了有关如何在中流式传输更新插件的信息 [!DNL Data Prep].

## 快速入门

此概述需要您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Data Prep]](./home.md)： [!DNL Data Prep] 允许数据工程师映射、转换和验证进出体验数据模型(XDM)的数据。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
* [Real-time Customer Profile](../profile/home.md)：根据来自多个来源的汇总数据，实时提供统一的客户个人资料。
* [源](../sources/home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。

## 在中使用流更新插入 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>以下源支持使用流更新插入：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 流更新插入高级工作流

流更新插入于 [!DNL Data Prep] 的工作方式如下：

* 您必须首先为以下项创建和启用数据集 [!DNL Profile] 消耗。 请参阅指南，网址为 [启用数据集 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 以了解更多信息。
* 如果必须链接新身份，则还必须创建一个其他数据集 **使用相同架构** 作为您的 [!DNL Profile] 数据集。
* 准备好数据集后，必须创建一个数据流以将传入请求映射到 [!DNL Profile] 数据集；
* 接下来，必须更新传入请求以包含必要的标头。 这些标头定义：
   * 需要执行的数据操作 [!DNL Profile]： `create`， `merge`、和 `delete`.
   * 要执行的可选身份操作 [!DNL Identity Service]： `create`.

### 配置身份数据集

如果必须关联新身份，则必须在传入有效负载中创建并传递其他数据集。 在创建身份数据集时，必须确保满足以下要求：

* 身份数据集必须具有与其关联的架构，作为 [!DNL Profile] 数据集。 架构不匹配可能导致系统行为不一致。
* 但是，您必须确保标识数据集与 [!DNL Profile] 数据集。 如果数据集相同，则将覆盖数据而不是更新数据。
* 虽然初始数据集必须启用 [!DNL Profile]，身份数据集 **不应启用** 对象 [!DNL Profile]. 否则，数据也将被覆盖而不是更新。 但是，身份数据集 **应该启用** 对象 [!DNL Identity Service].

#### 与身份数据集关联的架构中的必填字段 {#identity-dataset-required-fileds}

如果您的架构包含必填字段，则必须禁止验证数据集以启用 [!DNL Identity Service] 以仅接收身份。 可以通过应用 `disabled` 值到 `acp_validationContext` 参数。 请参阅以下示例：

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>如果与身份数据集关联的架构不含任何必填字段，则无需进行任何额外配置。

## 传入有效负荷结构

下面显示了建立新身份链接的传入有效负荷结构的示例。

### 具有身份配置的有效负载

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 用于标识数据流的唯一ID。 此数据流ID应该对应于使用创建的源连接 [!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]，或 [!DNL HTTP API]. 此数据流还应该具有 [!DNL Profile] — 启用数据集作为目标数据集。 **注意**：的ID [!DNL Profile]启用后的目标数据集也用作 `datasetId` 参数。 |
| `imsOrgId` | 与您的组织相对应的ID。 |
| `datasetId` | 的ID [!DNL Profile]启用数据流的目标数据集。 **注意**：此ID与 [!DNL Profile] — 在数据流中找到启用的目标数据集ID。 |
| `operations` | 此参数概述了 [!DNL Data Prep] 将根据传入的请求进行接收。 |
| `operations.data` | 定义必须在中执行的操作 [!DNL Real-Time Customer Profile]. |
| `operations.identity` | 通过以下方式定义对数据允许的操作 [!DNL Identity Service]. |
| `operations.identityDatasetId` | （可选）仅当必须链接新身份时才需要的身份数据集的ID。 |

#### 支持的操作

支持以下操作 [!DNL Real-Time Customer Profile]：

| 操作 | 描述 |
| --- | --- | 
| `create` | 默认操作。 这将为生成XDM实体创建方法 [!DNL Real-Time Customer Profile]. |
| `merge` | 这将为生成XDM实体更新方法 [!DNL Real-Time Customer Profile]. |
| `delete` | 这将为生成XDM实体删除方法 [!DNL Real-Time Customer Profile] 并从以下位置永久删除数据 [!DNL Profile Store]. |

支持以下操作 [!DNL Identity Service]：

| 操作 | 描述 |
| --- | --- |
| `create` | 此参数唯一允许的操作。 如果 `create` 作为值传递 `operations.identity`，则 [!DNL Data Prep] 为生成XDM实体创建请求 [!DNL Identity Service]. 如果标识已存在，则忽略该标识。 **注意：** 如果 `operations.identity` 设置为 `create`，然后 `identityDatasetId` 还必须指定。 XDM实体创建由内部生成的消息 [!DNL Data Prep] 将为此数据集id生成组件。 |

### 没有标识配置的有效负载

如果不需要关联新标识，则可以忽略 `identity` 和 `identityDatasetId` 操作中的参数。 这样做只会将数据发送到 [!DNL Real-Time Customer Profile] 并跳过 [!DNL Identity Service]. 有关示例，请参阅以下有效负载：

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## 动态传递主要身份

对于XDM更新，必须为启用架构 [!DNL Profile] 并包含一个主要身份。 您可以通过两种方式指定XDM架构的主要标识：

* 在XDM架构中指定一个静态字段作为主标识；
* 通过XDM架构中的身份映射字段组，将一个身份字段指定为主身份。

### 在XDM模式中指定一个静态字段作为主标识字段

在以下示例中， `state`， `homePhone.number` 和其他属性会以其各自的给定值更新插入到 [!DNL Profile] 主要标识为 `sampleEmail@gmail.com`. 然后，流生成XDM实体更新消息 [!DNL Data Prep] 组件。 [!DNL Real-Time Customer Profile] 然后确认XDM更新消息以更新用户档案记录。

>[!NOTE]
>
>在此示例中，不会将标识链接在一起，因为没有为标识定义任何操作。

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### 通过XDM架构中的身份映射字段组指定其中一个身份字段作为主身份

在此示例中，标头包含 `operations` 属性和 `identity` 和 `identityDatasetId` 属性。 这样可将数据与 [!DNL Real-Time Customer Profile] 以及要传递到的身份 [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## 已知限制和关键注意事项

下面概述了使用流式传输更新插入时要考虑的已知限制列表 [!DNL Data Prep]：

* 仅当向发送部分行更新时，才应使用流更新插入方法 [!DNL Real-Time Customer Profile]. 部分行更新为 **非** 被数据湖使用。
* 流更新插入方法不支持更新、替换和删除身份。 如果不存在新标识，则会创建新标识。 因此， `identity` 必须始终将操作设置为创建。 如果标识已存在，则该操作是无操作。
* 流更新插入方法当前不支持 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 和 [Adobe Experience Platform移动SDK](https://developer.adobe.com/client-sdks/documentation/).

## 后续步骤

通过阅读本文档，您现在应该了解如何在中流式传输更新插播 [!DNL Data Prep] 将部分行更新发送给 [!DNL Real-Time Customer Profile] 数据，同时还可以创建标识并将其与单个API请求关联。 有关其他的详细信息 [!DNL Data Prep] 功能，请阅读 [[!DNL Data Prep] 概述](./home.md). 要了解如何在中使用映射集 [!DNL Data Prep] API，请阅读 [[!DNL Data Prep] 开发人员指南](./api/overview.md).
