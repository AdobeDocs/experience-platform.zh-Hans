---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: 使用API使用决策服务运行时
topic: tutorial
description: '本文档提供了使用Adobe Experience PlatformAPI使用决策服务运行时服务的教程。 '
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---


# 使用API使用决策服务运行时

本文档提供了使用Adobe Experience PlatformAPI的运行时服 [!DNL Decisioning Service] 务的教程。

## 入门指南

本教程需要对决策和确定在客 [!DNL Experience Platform] 户体验过程中要展示的下一个最佳优惠所涉及的服务进行有效的了解。 在开始本教程之前，请查看以下文档：

- [[!DNL决策服务]](./../home.md):提供添加和删除优惠的框架，以及创建在客户体验期间选择最适合呈现的算法。
- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):平台组织客户体验数据的标准化框架。
- [[!DNL用户档案查询语言(PQL)]](../../segmentation/pql/overview.md):PQL用于定义规则和过滤器。
- [使用API管理决策对象和规则](./entities.md):在使用决策服务运行时之前，您需要设置相关实体。

以下各节提供了成功调用API所需了解的其他信 [!DNL Platform] 息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../tutorials/authentication.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

运行时请求也需要：

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID` 是UUID格式的字符串，它全局唯一，不能对不同的API调用重用

[!DNL Decisioning Service] 由多个彼此相关的业务对象控制。 所有业务对象都存储在 [!DNL Platform’s] 业务对象存储库XDM核心对象存储库中。 此存储库的一个主要功能是API与业务对象类型正交。 除了使用POST、GET、PUT、PATCH或DELETEAPI来指示其API端点中资源的类型，它们只有6个通用端点，但它们接受或返回一个参数，该参数在需要消歧时指示对象的类型。 模式必须向存储库注册，但除此之外，存储库还可用于一组开放式对象类型。

所有XDM核心对象存储库API开始的端点路 `https://platform.adobe.io/data/core/ode/`径。

端点后的第一个路径元素是 `containerId`。 此标识符通过XDM核心对象存储库根端点获取 `GET https://platform.adobe.io/data/core/xcore/`。

## 决策模型汇编

业务逻辑实体的激活自动、连续地发生。 一旦新选项保存在存储库中并标记为“已批准”，它将成为包含一组可用选项的候选选项。 更新决策规则后，规则集将重新组合并准备用于运行时执行。 在此自动激活步骤中，将评估由业务逻辑定义的任何不依赖于运行时上下文的约束。 此激活步骤的结果将发送到运行时可用的缓存 [!DNL Decisioning Service] 中。

### 位置、过滤器和生命周期状态的影响

优惠是连续创建的，其生命周期状态中会发生更改，或者可能会得到新的内容表示形式。 活动的优惠过滤器可能会更改，也可能匹配或过滤标签集已更新的优惠。 此过程可以相当地参与其中，应用程序和服务需要知道最终的候选活动集将是什么。 决策运行时提供一个活动到优惠API，它过滤器未批准、与优惠过滤器不匹配或没有活动所引用的位置的表示形式。

**请求**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**响应**

该参 `activityId` 数可以在url中重复，并且一个请求中最多可以提供30种不同的活动引用。 该响应将有助于发现由于设置而导致的任何意外情况，并且如下所示：

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

在对象更新时间和API响应反映活动到优惠映射的时间之间有几秒钟的小延迟。 每个对象的修订版本都在响应中提供，这样客户端就可以检查是否有对尚未反映的对象的更新。

### 诊断API和疑难解答

活动、优惠和合格规则编译为决策服务运行时使用的内部格式(运行时优惠目录)。 编译可以检测在存储对象和在XDM核心对象存储库中建立链接时执行的检查未捕获的错误。

提供诊断API以获取在该步骤中发生的任何编译错误，并且在没有错误的情况下获取关于上次重新编译规则和活动的时间的信息。

**请求**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

此API调用的唯一参数是 `containerId`。 结果是所有客户端的所有更新，这些客户端在该容器中修改了决策规则、优惠、活动或优惠过滤器。 在对象更新时间和编译完成时间之间有几秒钟的小延迟。 在响应诊断调用时，将返回上次更新时间戳和所有错误。

**响应**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## 用于执行决策的REST API调用

REST API是运行在顶部的应用程序的路由之一 [!DNL Platform] ，根据组织为其用户设置的规则、模型和约束获得最佳体验。 应用程序会发送用户档案的身份(用户档案ID和身份命名空间) [!DNL Decisioning Service] 之一，查找用户档案，并使用信息应用业务逻辑。 可以将附加上下文数据传递给请求，如果业务规则中指定，则将包括在数据中以作出决定。

应用程序可以通过请求一次最多30个活动的决策来获得更好的性能。 活动的URI在同一请求中传递。 REST API是同步的，如果没有个性化选项满足限制，则将返回所有这些活动的建议选项或回退选项。

有可能有两个不同的活动提出与他们的“最佳”相同的选择。 为避免重复合成的体验，默认情况 [!DNL Decisioning Service] 下，在同一请求中引用的活动之间进行仲裁。 仲裁意味着，对于每个活动，其前N个选项都会被考虑，但在这些活动中，不会多次提出任何选项。 如果两个活动有相同的排名最高的选项，其中一个将被选为使用其排名第二的选项或排名第三的选项，依此类推。 这些重复数据消除规则会尽量避免任何活动必须使用其回退选项。

决策请求包含其POST请求主体的参数。 正文的格式为JSON标 `Content-Type` 题值 `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

此时支持的请求模式和版本 `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`。 今后将提供其他请求模式或版本。

**请求**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** -当此可选属性的值设置为true时，决策请求将遵守限制限制，但不会实际提取这些计数器，则期望调用者永远不打算向用户档案提出该建议。 该提 [!DNL Decisioning Service] 案不会作为正式的XDM决策事件记录，也不会出现在报告数据集中。 此属性的默认值为false，当忽略该属性时，该决定不被视为测试运行，因此应向最终用户显示。
- **`xdm:validateContextData`** -此可选属性可打开或关闭上下文数据的验证。 如果启用了验证，则对于每个提供的上下文模式项，将从XDM注册表 `@type` 中获取（基于字段），并 `xdm:data` 对象将对其进行验证。

此模式的请求包含引用优惠活动的URI数组、用户档案标识和上下文数据项的数组：

- **`xdm:offerActivities`** -此必需属性是对象的数组，其中每个项都包含有关优惠活动的数据。 优惠活动具有以下属性：
   - **`xdm:offerActivity`** -活动的唯一标识符(URI)。 这是优惠 `@id` 活动的属性值。
- **`xdm:identityMap`** -包含符合XDM模式的JSON对象的必需属性 `https://ns.adobe.com/xdm/context/identitymap`。 该属性定义一个映射，其中密钥是标识命名空间代码，而值是给定命名空间中的最终用户标识符的列表。 如果是。
- **`xdm:contextData`** -可选属性，包含通过引用项的模式来描述的项。 数组中的每个上下文数据项都必须具有以下属性：
   - **`@type`** -引用此项目中对象的XDM模式的必需属性。
   - **`xdm:data`** -包含属性中给定的XDM模式对象属性的必需 `@type` 属性。

## 决策请求中的动态上下文数据

上一节指明了如何将XDM对象传递给决策请求。 以下是此类上下文对象数组的示例：

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

模式一定是由您的组织构建的。 要了解如何构建模式，请参阅 [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md)。 你的模式会命名空间的 `https://ns.adobe.com/{TENANT_ID}/schemas`。

模式注 [册表API开发人员指南](../../xdm/tutorials/create-schema-api.md) ，介绍如何以编程方式访问模式以及开发人员如何获取模式的租户ID和数字标识符。 版本号是必需的，也由模式注册表API提供。

由组织定义的模式通常具有名为的根属性， `_{TENANT_ID}`也称为租户命名空间字符串。
请注意，从全局模式组件（如_）使用的属性`https://ns.adobe.com/xdm/context/product` 具有命名空间前缀 `xdm:`。 在这种情况下，组织定义的属性 `productDetails` 是使用该数据类型构建的。 当租户属性嵌套在以租户命名空间命名的属性中时，全局可用的数据类型使用保留前缀 `xdm:` 来防止属性名称冲突。

属性中可以列出多个数据 `xdm:contextData` 对象。 每个对象都必须通过属性标识其 `@type` 类型。
上下文表达式对象的值可用于PQL合格规则，例如在条件下。 上下文数据对象必须通过特殊路径引用表达式进行寻址 `@{schemaId}`。 遵循此引用表达式的表达式是访问数据对象属性的常规路径表达式:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

在上面的示例中，变 `p` 量在标有=的对象数组上 `@type` 迭代 `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`。

请注意，PQL语法不在属性名称中使用前缀。 默认情况下，全局属性只是引用时没有前 `xdm:` 缀。 您的组织定义的属性嵌套在 **以租户命名空间** （在变量指示的示例中）命名的其他属 `{TENANT_ID}`性中。 要能够直接引用自定义属性，该变 `p` 量将绑定到引用附加嵌套属性的路径结果。

## 用户档案记录的使用

用户档案实体和体验事件实体的所有记录都已在用户档案商店中进行管理。 通过向请求传递一个或多个用户档案身份，将识别和查找这些身份的用户档案。 然后，该数据被自动地可用于由决策策略评估的决策规则和模型。

要检索用户档案和体验记录，将应用默认的合并策略。
请注意，将用户档案记录上传到 [!DNL Platform] 之后，在查找用户档案记录之前会有轻微的延迟。 通过流式API接收用户档案和体验记录的情况也是如此，仅在几秒钟后，数据才可用于评估评估用户档案和体验事件数据的决策规则。