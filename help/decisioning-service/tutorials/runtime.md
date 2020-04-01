---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API使用决策服务运行时
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 使用API使用决策服务运行时

本文档提供了使用Adobe Experience Platform API与决策服务的运行时服务结合使用的教程。

## 入门指南

本教程需要对Experience Platform服务进行有效的理解，这些服务涉及决策和确定在客户体验过程中呈现的下一个最佳优惠。 在开始本教程之前，请查看以下文档：

- [决策服务](./../home.md):提供添加和删除优惠的框架，以及创建在客户体验期间选择最适合呈现的算法。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。
- [用户档案查询语(PQL)](../../segmentation/pql/overview.md):PQL用于定义规则和过滤器。
- [使用API管理决策对象和规则](./entities.md):在使用决策服务运行时之前，您需要设置相关实体。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../tutorials/authentication.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

运行时请求也需要：

- x-request-id: `{UUID}`

>[!NOTE] 是UUID `UUID` 格式的字符串，它全局唯一，不得对不同的API调用重用

决策服务由许多彼此相关的业务对象控制。 所有业务对象都存储在平台的业务对象存储库XDM核心对象存储库中。 此存储库的一个主要功能是API与业务对象类型正交。 除了使用指示其API端点中资源类型的POST、GET、PUT、PATCH或DELETE API，只有6个通用端点，但它们接受或返回一个参数，该参数指示当需要消歧时对象的类型。 模式必须向存储库注册，但除此之外，存储库还可用于一组开放式对象类型。

与开始的所有XDM核心对象存储库API的端点路径 `https://platform.adobe.io/data/core/ode/`。

端点后的第一个路径元素是 `containerId`。 此标识符通过XDM核心对象存储库根端点获取 `GET https://platform.adobe.io/data/core/xcore/`。

## 决策模型的汇编

业务逻辑实体的激活是自动和连续的。 一旦新选项保存在存储库中并标记为“approved”，它将成为包含这组可用选项的候选者。 更新决策规则后，规则集将重新组合并准备好以执行运行时。 在此自动激活步骤中，将评估由业务逻辑定义的任何不依赖于运行时上下文的约束。 此激活步骤的结果将发送到缓存，在缓存中决策服务运行时可用。

### 位置、过滤器和生命周期状态的影响

优惠是连续创建的，更改会在其生命周期状态中发生，或者可能会获得新的内容表示形式。 活动的优惠过滤器可能会更改，也可能匹配或过滤标签集已更新的优惠。 此过程可以相当地参与其中，应用程序和服务需要知道最终的活动候选集是什么。 决策运行时提供了一个活动到优惠API，它过滤器未批准的优惠、不匹配优惠过滤器或没有活动引用的放置的表示形式。

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

该参 `activityId` 数可在url中重复，一个请求中最多可提供30种不同的活动引用。 该响应将有助于发现由于设置而导致的任何意外情况，并且如下所示：

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

在对象更新时间和API响应反映活动到优惠映射的时间之间有几秒钟的小延迟。 响应中会给出每个对象的修订版本，以便客户端可以检查是否有对尚未反映的对象的更新。

### 诊断API和疑难解答

活动、优惠和合格规则编译为决策服务运行时使用的内部格式(运行时优惠目录)。 编译可以检测在存储对象和在XDM核心对象存储库中建立链接时执行的检查未捕获的错误。

提供诊断API以获取在该步骤中发生的任何编译错误，并且如果没有错误来获取关于上次重新编译规则和活动的时间的信息，则提供诊断API。

**请求**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

此API调用的唯一参数是 `containerId`。 结果是所有客户端的所有更新，这些客户端已修改该容器中的决策规则、优惠、活动或优惠过滤器。 在对象更新时间和编译完成时间之间有几秒的小延迟。 在响应诊断调用时，将返回上次更新时间戳和所有错误。

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

## 执行决策的REST API调用

REST API是运行在平台顶部的应用程序根据组织为其用户设置的规则、模型和约束获得最佳体验的路由之一。 应用程序发送用户档案的一个标识(用户档案ID和标识命名空间)，决策服务将查找该用户档案，并使用该信息应用业务逻辑。 可以将其他上下文数据传递给请求，如果业务规则中指定，则将包括在数据中以作出决定。

应用程序可以通过请求一次最多30个活动的决策来获得更好的性能。 活动的URI在同一请求中传递。 REST API是同步的，如果没有个性化选项满足限制，则将返回所有这些活动的建议选项或备用选项。

有可能，两个不同的活动会提出与他们“最佳”相同的选择。 为避免重复合成的体验，默认情况下，决策服务会在同一请求中引用的活动之间进行仲裁。 仲裁意味着，对于每个活动，其前N个备选方案都将被考虑，但在这些活动中，不会多次提出任何备选方案。 如果两个活动有同样的最高排名选择，他们中的一个将被选为使用其次优或次优等。 这些重复数据消除规则会尽量避免任何活动必须使用其回退选项。

决策请求包含POST请求的正文的参数。 正文的格式设置为JSON `Content-Type` 标题值 `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

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

- **`xdm:dryRun`** -当此可选属性的值设置为true时，决策请求将遵守限制限制，但不会实际提取这些计数器，这就是预期调用者永远不打算向用户档案提出建议。 决策服务将不会将此主张记录为正式的XDM决策事件，并且它不会出现在报告数据集中。 此属性的默认值为false，如果忽略该属性，则不会将该决定视为测试运行，因此应向最终用户显示。
- **`xdm:validateContextData`** -此可选属性可打开或关闭上下文数据的验证。 如果打开了验证，则对于每个提供的上下文数据项，将从XDM注册表中获取模式（基于字段），并对 `@type``xdm:data` 象进行验证。

每个此模式的请求包含引用优惠活动的URI数组、用户档案标识和上下文数据项的数组：

- **`xdm:offerActivities`** -此必需属性是一个对象数组，其中每个项目都包含有关优惠活动的数据。 优惠活动具有以下属性：
   - **`xdm:offerActivity`** -活动的唯一标识符(URI)。 这是优惠活动的 `@id` 属性值。
- **`xdm:identityMap`** -包含符合XDM模式的JSON对象的必需属性 `https://ns.adobe.com/xdm/context/identitymap`。 该属性定义一个映射，其中该键是标识命名空间代码，该值是给定命名空间中的最终用户标识符的列表。 如果是。
- **`xdm:contextData`** -一个可选属性，其中包含通过对项目模式的引用描述的项目。 数组中的每个上下文数据项都必须具有以下属性：
   - **`@type`** -引用此项目中对象的XDM模式的必需属性。
   - **`xdm:data`** -一个必需属性，它包含属性中给定的XDM模式的对象属 `@type` 性。

## 决策请求中的动态上下文数据

上一节指明了如何将XDM对象传递到决策请求。 以下是此类上下文对象数组的示例：

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

模式必须由您的组织构建。 要了解构建模式，请参阅 [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md)。 你的模式会在命名空间里 `https://ns.adobe.com/{TENANT_ID}/schemas`。

模式注 [册表API开发人员指南介绍如何以编程方式访问模式](../../xdm/tutorials/create-schema-api.md) ，以及开发人员如何获取模式的租户ID和数字标识符。 版本号必填，也由模式注册表API提供。

由组织定义的模式通常具有名为的根属性 `_{TENANT_ID}`，也称为租户命名空间字符串。
请注意，从全局模式组件(如_`https://ns.adobe.com/xdm/context/product` )使用的属性具有命名空间前缀 `xdm:`。 在这种情况下，组织定义的属性是 `productDetails` 使用该数据类型构建的。 当租户属性嵌套在以租户命名空间命名的属性中时，全局可用的数据类型使用保留前缀来防止 `xdm:` 属性名称冲突。

属性中可以列出多个数据 `xdm:contextData` 对象。 每个对象都必须通过属性标识其 `@type` 类型。
上下文数据对象的值可用于PQL表达式，例如在合格规则条件中。 上下文数据对象必须通过特殊路径引用表达式进行寻址 `@{schemaId}`。 遵循此引用表达式的表达式是访问数据对象属性的常规路径表达式:

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

在上面的示例中，该变 `p` 量在标有 `@type` =的对象数组上迭代 `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`。

请注意，PQL语法不在属性名称中使用前缀。 默认情况下，全局属性只是引用而不带前 `xdm:` 缀。 您的组织定义的属性嵌套在以租户命名空间 **命名** （在由变量指示的示例中）的其他属性中 `{TENANT_ID}`。 为了能够直接引用自定义属性，变量将 `p` 绑定到引用附加嵌套属性的路径的结果。

## 使用用户档案记录

用户档案和体验事件实体的所有记录都已在用户档案商店中管理。 通过将一个或多个用户档案身份传递到请求，将识别和查找这些身份的用户档案。 然后，该数据自动地可用于由决策策略评估的决策规则和模型。

要检索用户档案和体验记录，将应用默认的合并策略。
请注意，将用户档案记录上传到平台数据之后，在查找用户档案记录之前会有轻微的延迟。 通过流式API摄取用户档案和体验记录也是如此，只需几秒钟，数据才可用于评估评估用户档案和体验事件数据的决策规则。