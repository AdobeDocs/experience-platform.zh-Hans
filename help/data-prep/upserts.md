---
keywords: Experience Platform；主页；热门主题；数据准备；数据准备；流；更新插入；流更新插入
title: 使用数据准备将部分行更新发送到实时客户个人资料
description: 了解如何使用数据准备将部分行更新发送到Real-Time Customer Profile。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---

# 使用[!DNL Real-Time Customer Profile]将部分行更新发送到[!DNL Data Prep]

>[!IMPORTANT]
>
>* 已弃用通过DCS入口为配置文件更新摄取体验数据模型(XDM)实体更新消息(使用JSON PATCH操作)。 作为替代方法，请遵循本指南中概述的步骤。
>
>* 您还可以使用HTTP API源[将原始数据摄取到DCS入口](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection)，并指定必要的数据映射以将您的数据转换为符合XDM标准的消息以进行配置文件更新。
>
>* 在流式更新插入中使用数组时，必须明确使用`upsert_array_append`或`upsert_array_replace`来定义操作的明确意图。 如果缺少这些函数，您可能会收到错误。

使用[!DNL Data Prep]中的流更新插入向[!DNL Real-Time Customer Profile]数据发送部分行更新，同时通过单个API请求创建和建立新的标识链接。

通过流式处理更新插入，您可以在引入期间将数据转换为[!DNL Real-Time Customer Profile]个PATCH请求时保留数据的格式。 根据您提供的输入，[!DNL Data Prep]允许您发送单个API有效负载并将数据转换为[!DNL Real-Time Customer Profile] PATCH和[!DNL Identity Service] CREATE请求。

[!DNL Data Prep]使用标头参数区分插入和更新插入。 所有使用更新插入的行都必须有一个标题。 您可以使用更新服务器，无论是否包含标识描述符。 如果您正在使用带有身份的upsert，则必须按照[配置身份数据集](#configure-the-identity-dataset)一节中概述的配置步骤操作。 如果您使用的是没有身份的upsert，则不需要在请求中提供身份配置。 有关详细信息，请阅读有关[不带标识的流更新插入](#payload-without-identity-configuration)的部分。

>[!NOTE]
>
>若要利用更新插入功能，建议您在数据引入期间关闭与XDM兼容的配置，并使用[数据准备映射器](./ui/mapping.md)重新映射传入有效负载。

本文档提供了有关如何在[!DNL Data Prep]中流式传输更新插件的信息。

## 快速入门

此概述需要您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Data Prep]](./home.md)： [!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
* [实时客户个人资料](../profile/home.md)：根据来自多个来源的汇总数据，实时提供统一的客户个人资料。
* [源](../sources/home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。

## 在[!DNL Data Prep]中使用流更新插入 {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>以下源支持使用流更新插入：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 流更新插入高级工作流

[!DNL Data Prep]中的流更新插入按如下方式工作：

* 您必须首先创建并启用[!DNL Profile]使用情况的数据集。 有关详细信息，请参阅[启用 [!DNL Profile]](../catalog/datasets/enable-for-profile.md)的数据集的指南。
* 如果必须链接新标识，则还必须创建一个与您的&#x200B;**数据集具有相同架构**&#x200B;的其他数据集[!DNL Profile]。
* 准备好数据集后，必须创建一个数据流以将传入请求映射到[!DNL Profile]数据集；
* 接下来，必须更新传入请求以包含必要的标头。 这些标头定义：
   * 需要对[!DNL Profile]执行的数据操作： `create`、`merge`和`delete`。
   * 要对[!DNL Identity Service]执行的可选标识操作： `create`。

### 配置身份数据集 {#configure-the-identity-dataset}

如果必须关联新身份，则必须在传入有效负载中创建并传递其他数据集。 在创建身份数据集时，必须确保满足以下要求：

* 身份数据集必须具有其关联的架构作为[!DNL Profile]数据集。 架构不匹配可能导致系统行为不一致。
* 但是，您必须确保标识数据集不同于[!DNL Profile]数据集。 如果数据集相同，则将覆盖数据而不是更新数据。
* 虽然必须为[!DNL Profile]启用初始数据集，但不应为&#x200B;**启用标识数据集**&#x200B;[!DNL Profile]。 否则，数据也将被覆盖而不是更新。 但是，应该为&#x200B;**启用标识数据集**&#x200B;[!DNL Identity Service]。

#### 与身份数据集关联的架构中的必填字段 {#identity-dataset-required-fileds}

如果您的架构包含必填字段，则必须取消数据集验证，以使[!DNL Identity Service]仅接收标识。 您可以通过将`disabled`值应用于`acp_validationContext`参数来禁止验证。 请参阅以下示例：

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
| `flowId` | 用于标识数据流的唯一ID。 此数据流ID应该对应于使用[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]或[!DNL HTTP API]创建的源连接。 此数据流还应具有启用了[!DNL Profile]的数据集作为目标数据集。 **注意**：已启用[!DNL Profile]的目标数据集的ID也用作`datasetId`参数。 |
| `imsOrgId` | 与您的组织相对应的ID。 |
| `datasetId` | 您的数据流已启用[!DNL Profile]的目标数据集的ID。 **注意**：此ID与在数据流中找到的启用[!DNL Profile]的目标数据集ID相同。 |
| `operations` | 此参数概述了[!DNL Data Prep]将根据传入请求执行的操作。 |
| `operations.data` | 定义必须在[!DNL Real-Time Customer Profile]中执行的操作。 |
| `operations.identity` | 定义[!DNL Identity Service]对数据允许的操作。 |
| `operations.identityDatasetId` | （可选）仅当必须链接新身份时才需要的身份数据集的ID。 |

#### 支持的操作

[!DNL Real-Time Customer Profile]支持以下操作：

| 操作 | 描述 |
| --- | --- | 
| `create` | 默认操作。 这将为[!DNL Real-Time Customer Profile]生成XDM实体创建方法。 |
| `merge` | 这将为[!DNL Real-Time Customer Profile]生成XDM实体更新方法。 |
| `delete` | 这将为[!DNL Real-Time Customer Profile]生成XDM实体删除方法，并从[!DNL Profile store]中永久删除数据。 |

[!DNL Identity Service]支持以下操作：

| 操作 | 描述 |
| --- | --- |
| `create` | 此参数唯一允许的操作。 如果将`create`作为`operations.identity`的值传递，则[!DNL Data Prep]会为[!DNL Identity Service]生成XDM实体创建请求。 如果标识已存在，则忽略该标识。 **注意：**&#x200B;如果`operations.identity`设置为`create`，则还必须指定`identityDatasetId`。 将为此数据集ID生成由[!DNL Data Prep]组件内部生成的XDM实体创建消息。 |

### 没有标识配置的有效负载 {#payload-without-identity-configuration}

如果不需要链接新标识，则可以在操作中忽略`identity`和`identityDatasetId`参数。 这样做只向[!DNL Real-Time Customer Profile]发送数据并跳过[!DNL Identity Service]。 有关示例，请参阅以下有效负载：

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

对于XDM更新，必须为[!DNL Profile]启用架构并包含主标识。 您可以通过两种方式指定XDM架构的主要标识：

* 在XDM架构中指定一个静态字段作为主标识；
* 通过XDM架构中的身份映射字段组，将一个身份字段指定为主身份。

### 在XDM模式中指定一个静态字段作为主标识字段

在下面的示例中，`state`、`homePhone.number`和其他属性以其各自的给定值更新插入到[!DNL Profile]中，主标识为`sampleEmail@gmail.com`。 然后，流[!DNL Data Prep]组件生成了XDM实体更新消息。 然后，[!DNL Real-Time Customer Profile]确认XDM更新消息以更新插入用户档案记录。

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

在此示例中，标头包含具有`operations`和`identity`属性的`identityDatasetId`属性。 这允许将数据与[!DNL Real-Time Customer Profile]合并，也允许将标识传递到[!DNL Identity Service]。

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

下面概述了使用[!DNL Data Prep]流式传输更新插入时要考虑的已知限制列表：

* 仅当向[!DNL Real-Time Customer Profile]发送部分行更新时，才应使用流更新插入方法。 部分行更新&#x200B;**不是**&#x200B;被数据湖使用。
* 流更新插入方法不支持更新、替换和删除身份。 如果不存在新标识，则会创建新标识。 因此，必须始终将`identity`操作设置为创建。 如果标识已存在，则该操作是无操作。
* 流更新插入方法当前不支持[Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md)或[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)。

## 后续步骤

通过阅读本文档，您现在应该了解如何在[!DNL Data Prep]中流式传输更新内容，以便向[!DNL Real-Time Customer Profile]数据发送部分行更新，同时还可以创建标识并将其与单个API请求关联。 有关其他[!DNL Data Prep]功能的详细信息，请阅读[[!DNL Data Prep] 概述](./home.md)。 要了解如何在[!DNL Data Prep] API中使用映射集，请阅读[[!DNL Data Prep] 开发人员指南](./api/overview.md)。
