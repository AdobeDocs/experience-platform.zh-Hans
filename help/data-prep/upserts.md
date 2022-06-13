---
keywords: Experience Platform；主页；热门主题；数据准备；数据准备；流；升级；流升级
title: 使用数据准备将部分行更新发送到用户档案服务
description: 本文档提供了有关如何使用数据准备将部分行更新发送到用户档案服务的信息。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 0f1b9cdde3452afdf8cf045cf0a6660ee0ce56cf
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 1%

---

# 将部分行更新发送到 [!DNL Profile Service] 使用 [!DNL Data Prep]

在中流式插入上插页 [!DNL Data Prep] 允许您将部分行更新发送到 [!DNL Profile Service] 数据，同时使用单个API请求创建和建立新的身份链接。

通过流式上插页，您可以在将数据转换为 [!DNL Profile Service] PATCH请求。 根据您提供的输入， [!DNL Data Prep] 允许您发送单个API负载，并将数据转换为 [!DNL Profile Service] PATCH和 [!DNL Identity Service] 创建请求。

本文档提供了有关如何在 [!DNL Data Prep].

## 快速入门

此概述需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
* [实时客户资料](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [源](../sources/home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。

## 在 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>以下源支持使用流上插页：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 流式上插页高级工作流

在中流式插入上插页 [!DNL Data Prep] 如下所示：

* 您必须先为 [!DNL Profile] 消费。 请参阅 [为 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 以了解更多信息；
* 如果必须关联新标识，则还必须创建一个额外的数据集 **使用相同的模式** 作为 [!DNL Profile] 数据集；
* 准备好数据集后，必须创建一个数据流，以将传入请求映射到 [!DNL Profile] 数据集；
* 接下来，您必须更新传入的请求以包含必需的标头。 这些标题定义：
   * 需要使用 [!DNL Profile]: `create`, `merge`和 `delete`;
   * 要通过 [!DNL Identity Service]: `create`.

### 配置身份数据集

如果必须关联新标识，则必须在传入有效负载中创建并传递其他数据集。 创建身份数据集时，必须确保满足以下要求：

* 身份数据集必须具有其关联的架构作为 [!DNL Profile] 数据集。 模式不匹配可能导致系统行为不一致；
* 但是，您必须确保身份数据集与 [!DNL Profile] 数据集。 如果数据集相同，则数据将被覆盖而不是更新；
* 而必须为 [!DNL Profile]，身份数据集 **不应** 为 [!DNL Profile]. 否则，数据也将被覆盖而不是更新。

#### 与身份数据集关联的架构中的必填字段 {#identity-dataset-required-fileds}

如果您的架构包含必填字段，则必须禁止验证数据集才能启用 [!DNL Identity Service] 来仅接收身份。 通过应用 `disabled` 值 `acp_validationContext` 参数。 请参阅以下示例：

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>如果与身份数据集关联的架构没有任何必填字段，则无需执行任何其他配置。

## 传入有效负载结构

下面显示了建立新身份链接的传入有效负载结构的示例。

### 具有身份配置的负载

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
| `flowId` | 用于标识数据流的唯一ID。 此数据流ID应与创建的源连接相对应 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]或 [!DNL HTTP API]. 此数据流还应具有 [!DNL Profile] — 已启用数据集作为目标数据集。 **注意**:的ID [!DNL Profile]-enabled target数据集也用作 `datasetId` 参数。 |
| `imsOrgId` | 与您的组织对应的ID。 |
| `datasetId` | 的ID [!DNL Profile]已启用数据流的目标数据集。 **注意**:此ID与 [!DNL Profile]在数据流中找到已启用的目标数据集ID。 |
| `operations` | 此参数概述了 [!DNL Data Prep] 将根据传入的请求接收。 |
| `operations.data` | 定义必须在 [!DNL Profile Service]. |
| `operations.identity` | 定义允许对数据执行的操作 [!DNL Identity Service]. |
| `operations.identityDatasetId` | （可选）仅当必须关联新身份时才需要的身份数据集的ID。 |

#### 支持的操作

支持以下操作 [!DNL Profile Service]:

| 操作 | 描述 |
| --- | --- | 
| `create` | 默认操作。 这会为生成XDM实体创建方法 [!DNL Profile Service]. |
| `merge` | 这会为生成XDM实体更新方法 [!DNL Profile Service]. |
| `delete` | 这会为生成XDM实体删除方法 [!DNL Profile Service] 并从 [!DNL Profile Store]. |

支持以下操作 [!DNL Identity Service]:

| 操作 | 描述 |
| --- | --- |
| `create` | 此参数唯一允许的操作。 如果 `create` 作为的值传递 `operations.identity`，则 [!DNL Data Prep] 为生成XDM实体创建请求 [!DNL Identity Service]. 如果标识已存在，则忽略该标识。 **注意：** 如果 `operations.identity` 设置为 `create`，则 `identityDatasetId` 也必须指定。 XDM实体创建由内部生成的消息 [!DNL Data Prep] 将为此数据集id生成组件。 |

### 无身份配置的负载

如果不需要链接新身份，则可以忽略 `identity` 和 `identityDatasetId` 参数。 这样做只会将数据发送到 [!DNL Profile Service] 然后跳过 [!DNL Identity Service]. 有关示例，请参阅下面的有效负载：

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

## 动态传递主标识

对于XDM更新，必须为 [!DNL Profile] 和包含主标识。 您可以通过两种方式指定XDM架构的主标识：

* 在XDM架构中指定静态字段作为主标识；
* 在XDM架构中，通过身份映射字段组将其中一个身份字段指定为主标识。

### 在XDM架构中将静态字段指定为主标识字段

在以下示例中， `state`, `homePhone.number` 和其他属性将随其各自的给定值一起更新到 [!DNL Profile] 的主要标识 `sampleEmail@gmail.com`. 然后，由流生成XDM实体更新消息 [!DNL Data Prep] 组件。 [!DNL Profile Service] 然后确认XDM更新消息以更新用户档案记录。

>[!NOTE]
>
>在此示例中，由于没有为身份定义操作，因此身份不会链接在一起。

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

### 在XDM架构中通过身份映射字段组将其中一个身份字段指定为主标识

在此示例中，标题包含 `operations` 属性 `identity` 和 `identityDatasetId` 属性。 这允许数据与 [!DNL Profile Service] 以及将身份传递到 [!DNL Identity Service].

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

以下概述了在对上插页进行流式处理时需要考虑的已知限制列表 [!DNL Data Prep]:

* 仅在向 [!DNL Profile Service]. 部分行更新包括 **not** 由数据湖使用。
* 流式更新插页方法不支持更新、替换和删除身份。 如果不存在新标识，则会创建新标识。 因此， `identity` 操作必须始终设置为创建。 如果标识已存在，则操作为“不执行操作”。
* 流上插页方法当前仅支持基元单值属性（如整数、日期、时间戳和字符串）和对象。 流上插页方法不支持替换、附加或覆盖数组属性和特定数组索引。
* 当前不支持流式更新插页方法 [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 和 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## 后续步骤

通过阅读本文档，您现在应该了解如何在 [!DNL Data Prep] 向 [!DNL Profile Service] 数据，同时还使用单个API请求创建和链接身份。 有关其他 [!DNL Data Prep] 功能，请阅读 [[!DNL Data Prep] 概述](./home.md). 了解如何在 [!DNL Data Prep] API，请阅读 [[!DNL Data Prep] 开发人员指南](./api/overview.md).
