---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API管理决策服务实体
topic: tutorial
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# 使用API管理决策对象和规则

本文档提供了使用Adobe Experience Platform API与决策服务的业务实体协作的教程。

本教程分为两部分：

- 用于管理业务对象的通用存储库API在第一部分 [中介绍](#managing-repository-entities-using-apis)。 这些API在意义上是通用的，它们为任何类型的业务对象提供创建、读取、更新、删 **除** 和搜索功能。 描述了通用API模型，并解释了超文本应用语言(HAL)的关系。

- 应用有关存储库API的知识，第 [](#creating-and-managing-offer-decisioning-entities-using-apis) 二部分重点介绍通过存储库API管理的业务实体。 使用相同的API时，管理两个不同实体(如活动和业务规则)之间的唯一区别是请求和响应有效负荷，以及指示所管理对象类型的必要标头值。

## 入门指南

本教程需要对Experience Platform服务和API惯例有充分的了解。 平台存储库是其他几个平台服务用来存储业务对象和各种类型的元数据的服务。 它为管理和查询这些对象提供了一种安全、灵活的方式，以供多个运行时服务使用。 决策服务就是其中之一。 在开始本教程之前，请查看以下文档：

- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。
- [决策服务](./../home.md):介绍用于一般体验决策的概念和组件，特别是优惠决策。 说明了在客户体验期间选择最佳呈现选项时所使用的策略。
- [用户档案查询语(PQL)](../../segmentation/pql/overview.md):PQL是一种功能强大的语言，可编写XDM实例的表达式。 PQL用于定义决策规则。

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

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 存储库API惯例

决策服务由许多彼此相关的业务对象控制。 所有业务对象都存储在平台的业务对象存储库中。 此存储库的一个主要功能是API与业务对象类型正交。 除了使用指示其API端点中资源类型的POST、GET、PUT、PATCH或DELETE API，只有6个通用端点，但它们接受或返回一个参数，该参数指示当需要消歧时对象的类型。 模式必须向存储库注册，但除此之外，存储库还可用于一组开放式对象类型。

除了上面列出的标题之外，用于创建、读取、更新、删除和查询存储库对象的API还有以下约定：

- 所有与开始的存储库API的端点路径 `https://platform.adobe.io/data/core/xcore/`。

API有效负荷格式与或头协 `Accept` 商进 `Content-Type` 行。 表或标题中 `Accept` 的消息格 `Content-Type``application/vnd.adobe.platform.xcore.{FORMAT}+json` 式由{FORMAT}取决于特定存储库API请求或响应消息的值来指示。

| FORMAT变量 | 请求或响应实体的说明 |
| --- | --- |
| 后<br>跟参数 `schema={schemaId}` | 消息包含由JSON模式描述的实例，该实例由format参数模式指示。 该实例包含在JSON属性中 `_instance`。 响应有效负荷中的其他顶级属性指定所有资源可用的存储库信息。  符合HAL格式的消息有一个属 `_links` 性，该属性包含HAL格式的引用。 |
| `patch.hal` | 该消息包含JSON PATCH有效负荷，假定要修补的实例符合HAL。 这意味着不仅可以修补实例自己的实例属性，还可以修补实例的HAL链接。 请注意，客户端对哪些属性可以更新存在限制。 |
| `home.hal` | 该消息包含存储库的主文档资源的JSON格式表示形式。 |
| xdm.receipt | 该消息包含JSON格式的响应，用于创建、更新（完整和修补）或删除操作。 接收包含控制数据，这些控制数据以ETag的形式指示实例的修订。 |

每个格式变体 **的使用情况** 取决于特定的API:

| API | 内容类型标题 | 接受标题 |
| --- | --- | --- |
| 创建实例创 <br/>建容器 | `hal`<br/>具有模式参数 | `xdm.receipt` |
| 更新<br/>InstanceUpdate容器 | `hal`<br/>具有模式参数 | `xdm.receipt` |
| 修补程序实例 | `patch.hal` | `xdm.receipt` |
| 删除实<br/>例删除容器 | 不适用 | `xdm.receipt` |
| 读取实<br/>例读取容器 | 不适用 | `hal` 带参 `schema` 数 |
| 列表<br/>实例列表容器 | 不适用 | `hal` 具有特殊参 `schema` 数 `https://ns.adobe.com/experience/xcore/hal/results` |
| 搜索实例 | 不适用 | 带有特殊参数的 `schema` hal `https://ns.adobe.com/experience/xcore/hal/results` |
| 读取存储库根 | 不适用 | `home.hal` |

对于容器创建、更新和读取API,format参数模式具有值 `https://ns.adobe.com/experience/xcore/container`。

`ContainerId` 是实例API的第一个路径参数。 所有业务实体都居住在称为容器的地方。 容器是一种隔离机制，可以分开不同的疑虑。 存储库实例API的第一个路径元素是常规端点之后的元素 `containerId`。 从呼叫者可访问的容器的列表获得标识符。 例如，用于在容器中创建实例的API是 `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`。

可访问容器的列表是通过使用标准头使用HTTP GET请求调用存储库根端点“/”来获取的。

## 管理对容器的访问

管理员可以将类似的承担者、资源和访问权限分组到用户档案中。 这减轻了管理负担，并且 [Adobe的Admin Console UI支持](https://adminconsole.adobe.com)。 您必须是贵组织中Adobe Experience Platform和优惠的产品管理员，才能创建用户档案并为其分配用户。

只需一次性创建与某些权限匹配的产品用户档案，然后只需将用户添加到这些用户档案即可。 用户档案充当被授予权限的组，该组中的每个实际用户或技术用户都会继承这些权限。

### 列表容器可供用户访问和集成

当管理员授予普通用户访问容器或集成权限时，这些容器将显示在存储库的所谓“主页”列表中。 该列表对于不同用户或集成可能不同，因为它是呼叫者可以访问的所有容器的子集。 容器的列表可以通过其与产品上下文的关联来过滤。 过滤器参数被调用 `product` 并且可以重复。 如果提供了多个产品上下文过滤器，则将返回与任何给定产品上下文关联的容器的合并。 请注意，单个容器可以关联到多个产品上下文。

平台决策服务容器的上下文当前为 `dma_offers`。

>[!NOTE] 平台决策容器的情境即将变为现实 `acp`。 筛选是可选的，但过滤器只需在将 `dma_offers` 来的版本中进行编辑。 要准备进行此更改，客户端应不使用过滤器或应用两个产品上下文作为筛选器。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**响应**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

请注 `instanceId` 意结果项中列出的内容。 它用作API中 `containerId` 的参数以读取和操作常规业务对象。

已根据用户的访问权限过滤该列表，但可以通过属性查询进一步过滤。

## 用于管理实体的通用API

### 创建实例

用于在存储库中创建新实例的API采用 `containerId` path参数，并使用模式参数标识标题中实 `Content-Type` 例的类型。

实例属性在包含在属性中的有效负荷中 `_instance` 提供。 对于具有给定模式标识符的JSON模式，实例属性必须有效。

HAL属 `_links` 性必须存在，但可以为空。 这意味着没有为此实例定义自定义链接。

**请求**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**响应**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

响应包含刚刚创建的对象的instanceId。 此instanceId是不可变的，始终由存储库分配并且全局唯一。 该值用作物理标识符。

此外，如果模式具有此类属性，则在响 `@id` 应有效负荷的属性中返回通用资源标识符(URI)。 每个实例都应有一个用作URI的属性和实例的主键。 其他实例使用此标识符与新实例建立关系，包括跨不同类型。 在当前版本中，URI由存储库生成并包含在属性 `@id` 中。 将来的版本可能会放松此规则，允许客户端管理自己的URI值并命名包含该规则的属性。

请注意，这些URI不是URL，不提供直接检索资源的方法。 为了指示这一方面，URI的前缀为不指定检索协议的URI方案。 但是，URI可用于查找包含查询的实例。

REST响应将有一个位置标题，其中包含一个URL组件，该组件可用于检索刚刚创建的实例。 此组件是相对URI引用，需要应用于存储库的基本URI。 基本URI在标头中返 `Content-Base` 回。

该属 `repo:etag` 性指定实例的修订版。 此值可用于更新操作以实施一致性。 HTTP头可 `If-Match` 用于向PUT或PATCH API调用添加一个条件，以确保对实例没有可能意外覆盖的其他更改。 每次 `repo:etag` 创建、读取、更新、删除和查询调用都会返回该值。 根据RFC7232第3.1节，该值 ` If-Match` 用作 [标题中的值](https://tools.ietf.org/html/rfc7232#section-3.1)。

其余属性指示用于创建和上次修改实例的帐户和API密钥。 由于实例是由此调用创建的，因此相应的值是请求的值。

### 按ID查找实例

使用随“创建”调用返回的位置标题中的URL，应用程序可以查找实例。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE] 尽管 `instanceId` 应用程序被指定为路径参数，但应尽可能不要自己构建路径，而应遵循列表和搜索操作中包含的实例的链接。 有关详细信息，‎请参阅‎第6.4.4节和第6.4.6节。

**响应**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

实例的JSON属性包含在属性中，而 `_instance` 其他根级别属性包含有关实例的元数据。

该资源还包含一组JSON模式ID。 此数组表示已验证此实例的JSON模式。

每个实例都包含一个自关系类型的HAL链接，该链接与IANA注册的自关系(由 [RFC5988定义])相对应。

**测试实例的较新版本**

该实例 `eTag` 的当前值随响应一起返回，它允许客户端对该实例发出条件操作，以避免再次检索同一资源状态，或避免在客户端不知情的情况下覆盖稍后修订的值。

查找API允许客户端指定标 `If-None-Match` 头参数。 请参阅此标准HTTP参数 [RFC2616的定义]。 客户端指定的实体标记值是它通过最新响应(从更新、读取、列表或搜索API调用)接收的值。 请注意，该 `etag` 值对客户端应不透明，并且必须以字符串形式提供，并用引号括起来。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

当实例的上次修订版本是与给定的etag一起的版本时，存储库API将以状态304 Not Modified进行响应。

### 列表实例——排序和分页

客户端将无法跟踪正在创建的实例，因此无法通过其物理instanceId访问它们。 使用读取实例API将是例外。 客户端也不知道其他客户端已创建了哪些实例。

更典型的访问模式是翻页浏览所有实例集。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**响应**

响应取决于指定 `{schemaId}` 的。 例如，对于“https<span></span>://ns.adobe.com/experience/优惠管理/优惠活动&amp;id=xcore:优惠活动:fa24f9e8fc15c73”，响应如下所示。

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE] 结果包含给定模式或此列表的第一页的实例。 请注意，实例可以符合多个模式，因此可以出现在多个列表中。

页面资源为临时资源，为只读；无法更新或删除它们。 寻呼模型提供在延长的时间段内对大列表子集的随机访问，而不保持任何每个客户端状态。

要以这种方式按页访问实例列表，必须能够定义对该实例列表枚举的条目的稳定排序。 请注意，“stable”并不表示实例将显示在预定页面中。 事实上，当通过根据属性P对实例排序而形成页面顺序并且客户端更新了该属性P时，则另一客户端可以在通过列表进行分页时在不同的页面上再次到达该实例。 换句话说，该模型倾向于返回更新的结果。

但是，当排序顺序基于不可修改的属性时，“稳定”排序顺序保证到达寻呼操作开始时存在的所有实例（除非它们在到达其页面时被删除）。 当此排序顺序位于单调增加的属性上时，也将到达在寻呼操作开始后创建的实例。

客户端可以提供有关其所需页面大小的提示，但提供其返回的页面的实例数量，完全取决于存储库。 为保证顺序稳定，服务必须在页面中添加或删除项目，以便排序属性的值在页面边界上不同。 这样，下一页不会再包含最后一页中的某些项目，或者在最坏情况下，每个页面上的相同项目会卡在一起。

分页由以下参数控制：

- **`orderBy`**:包含以逗号分隔的有序属性列表，实例列表按该排序。 第一个属性用于主排序，第二个属性用于解析主排序中的关联，等等。 如果指定的属性每个实例具有唯一值，则不可能建立关系，并且每个项目之后都可能出现分页。 属性的名称可以前缀有指示升序 `+` 或指示该属 `-` 性的降序排序。 如果属性名未在前缀中添加前缀，则结果将按升序排序。 如果 `orderBy` 请求中未指定，则存储库将改用物理instanceId属性。
- **`start`**:客户端使用开始参数定义要检索的页面。 开始参数确定所需页面的开始。 响应将包含以属性值严格大于（对于升序）或严格小于（对于降序）指定值的实例开头的实例。 `orderBy` 如果未指定查询参数，则它默认为在第一个可能的实例标识符之前排序的instanceId值，因此从第一页中忽略此值。
- **`limit`**:指定一个正整数作为对给定请求应返回的最大项目数的提示。 由于需要提供可靠的开始参数操作，实际响应大小可以更小或更大

### 筛选列表

过滤列表结果是可能的，并且独立于寻呼机制而发生。 过滤器只需按列表的顺序跳过实例，或显式要求仅包括满足给定条件的实例。 客户端可以请求用作过滤器的属性表达式，也可以指定用作实例主键值的URI列表。

- **`property`**:包含属性名路径，后跟比较运算符，后跟值。 <br/>
返回的实例的列表包含表达式计算结果为true的实例。 例如，假定实例具有有效负荷属 `status` 性且可能的值为 `draft`, `approved`，然后 `archived``deleted``property=_instance.status==approved` 查询参数只返回状态已获批准的实例。 <br/>
<br/>
要与给定值进行比较的属性被标识为路径。 各个路径组件由“.”分隔，如：`_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

对于具有字符串、数字或日期／时间值的属性，允许的运算符包括： `==`、 `!=``<`、 `<=`和 `>``>=`。 此外，对于具有字符串值的属性，可以使 `~` 用运算符。 该运 `~` 算符根据常规表达式匹配给定属性。 该属性的字符串值必须与要包含在 **筛选结果中的实体的** 整个表达式相匹配。 例如，在属性值中的任 `cars` 意位置查找字符串需要常规表达式 `.*cars.*`。 如果没有前导或 `.*`尾部，则只有属性值分别以开始或结束的实体 `cars`才匹配。 对于运 `~` 算符，字母字符的比较不区分大小写。 对于所有其他运算符，比较区分大小写。<br/><br/>
不仅实例有效负荷属性可用于过滤器表达式。 以相同的方式比较封装属性，例如， `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
可<br/>`property` 以重复查询参数，以便应用多个过滤条件，例如返回在某个日期之后和某个日期之前最后修改的所有实例。 这些表达式中的值必须经过URL编码。 如果没有表达式，并且只列出了该属性的名称，则符合条件的项目是那些具有给定名称的属性的项目。<br/>
<br/>

- **`id`**:有时，列表需要按实例的URI过滤。 该 `property` 查询参数可用于过滤掉一个实例，但要获得多个实例，可向该请求提供URI的列表。 重复 `id` 该参数，且每个出现项指定一个URI值， `id={URI_1}&id={URI_2},…` URI值必须经过URL编码。

分页结果将作为特殊mime类型返回 `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**响应**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

响应包含JSON属性结果中结果项的列表，该结果旁边有两个属性，它们表示此页上的结果数以及筛选列表中从刚返回的页面开始的项总数。

### 全文搜索和结构化查询

如果客户端希望提供更复杂的过滤条件，并按字符串属性中包含的术语搜索实例，则存储库会优惠更强大的搜索API。

**请求**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

除了列表API中的分页和筛选参数之外，此API还允许客户端添加全文和布尔查询参数。

全文搜索由以下参数控制：

- **`q`**:包含一个以空格分隔的无序列表，这些术语在与实例的任何字符串属性匹配之前进行标准化。 对术语分析字符串属性，并且这些术语也进行标准化。 搜索查询将尝试匹配参数中指定的一个或多个术 `q` 语。 字符+、-、=和&amp;、||, >, &lt;,!,(,), {, }, [,],^, &quot;, ~, *, ?, :, /对于确定查询字符串内的单词边界具有特殊含义，在与字符匹配的代号中出现时，应使用反斜杠进行转义。 查询字符串可以用多次引号括起来，以实现精确字符串匹配和转义特殊字符。
- **`field`**:如果搜索词只应与属性的子集匹配，则字段参数可以指示该属性的路径。 可以重复该参数以指示应匹配的多个属性。
- **`qop`**:包含用于修改搜索的匹配行为的控制参数。 当参数设置为且随后所有搜索词必须匹配且参数不存在或其值设置为或随后任何术语可以计为匹配项时。

### 更新和修补实例

要更新实例，客户端可以一次覆盖属性的完整列表，或使用JSON PATCH请求处理包括列表在内的各个属性值。

在这两种情况下，请求的URL都指定物理实例的路径，并且在这两种情况下，响应都将是JSON接收有效负荷，就像创建操作返回的JSON [接收有效负荷](#create-instances)。 客户端最好将其从 `Location` 此对象的先前API调用中收到的头或HAL链接用作此API的完整URL路径。 如果这不可能，则客户端可以从和构建 `containerId` URL `instanceId`。

**请求** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**请求** （修补程序）

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

PATCH请求应用这些说明，然后根据模式和与PUT请求相同的实体和参照完整性规则验证生成的实体。

**控制属性值编辑**

您可以使用以下注释防止在创建和／或更新时设置属性：

- **`"meta:usereditable"`**:布尔值——当请求来自用户代理，该代理通过用户或技术帐户访问令牌标识调用者时，带有注释的属性 `"meta:usereditable": false` 不应出现在有效负荷中。 如果是，则它们的值不得与当前设置的值不同。 如果值不同，则更新或修补程序请求将被拒绝，状态为422“可不处理实体”。
- **`"meta:immutable"`**:Boolean —— 设置注释后，不 `"meta:immutable": true` 能更改这些属性。 这适用于来自最终用户、技术帐户集成或特殊服务的请求。

**并发更新测试**

存在多个客户端尝试同时更新实例的情况。 该存储库在计算节点群集上操作，而不需要中央事务管理。 为避免一个客户端同时写入另一个实例，客户端可以使用条件更新或修补请求。 通过在标 `etag` 题中指定字符串，存储库 `If-Match` 确保只有第一个请求成功，并且使用相同值的其他客户端的后续请求将 `etag` 失败。 值随 `etag` 实例的每次修改而改变。 客户端必须检索实例以获取最新值， `etag` 然后在尝试更新的众多客户端中只有一个客户端可以使用该值成功。 其他客户端将被拒绝，并显示消息409冲突。

### 删除实例

可以通过DELETE调用删除实例。 客户端最好将其从 `Location` 先前API调用中收到的头或HAL链接用作完整的URL路径。 如果这不可能，则客户端可以从和物理 `containerId` URL构建URL `instanceId`。

**请求**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**响应**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

当收到删除请求时，存储库检查任何模式的任何其他实例，仍引用要删除的实例。 在分布式、高可用性系统中，不能立即检查引用完整性。 定义外键关系时，将异步执行检查。 这导致对删除请求结果的回复稍有延迟。 当执行这些检查时，立即响应包括状态202“已接受”和用于检查标题中删除操作结果的链 `Location` 接。 然后，客户应检查该链接以获取结果。

如果发现一个实例引用了被删除的实例，则结果将是删除操作被拒绝。 如果未发现其他外键引用，则完成删除。 如果结果尚未确定，则响应将指示在202年接受的另一个具有相同标题的响应中， `Location` 并将要求客户继续检查。 当结果被确定时，响应将指示状态为200“确定”且响应的有效负荷将包含原始删除请求的结果。 请注意，200 Ok响应仅表示已知结果，且响应机构将包含确认或拒绝删除请求。

## 创建优惠及其子组件

上一节中描述的API统一适用于所有类型的业务对象。 创建优惠和活动之间的唯一区别是标题将JSON模式标记为符合模式的请求的JSON有效负荷。 `content-type` 因此，以下几节只需关注这些模式及其之间的关系。

当使用内容类型的API `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`时，实例自己的属性嵌入到其旁 `_instance` 边有属性的属 `_links` 性中。 这将是表示所有实例的常规格式：

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE] 出于简单原因，在所有JSON片段中，仅说明实例属性，并且仅在需要时显示封套属性和_links部分。

### 常规优惠属性

优惠是一种决策选项类型，优惠的JSON模式会继承每个选项实例将具有的标准选项属性。

- **`@id`** -每个选项的唯一标识符，它是主键，用于从其他对象引用该选项。 创建实例时，将分配此属性，该属性不可变且不可编辑。
- **`xdm:name`** -每个选项都有一个用于搜索和显示目的的名称。 该名称不是不可变的，不能用于唯一标识实例。 名称可以自由选择，但在优惠实例中应是唯一的。

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 该 `schemaId` 参数必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer` 或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果优惠是回退优惠。

每个优惠实例都可以有一组可选属性，这些属性只是该实例的特征。 不同的优惠可以有不同的键用于这些属性，但值必须是字符串。 这些属性可用于决策和分段规则。 他们还可以收集确定的体验以进一步自定义消息。

### 优惠生命周期

有一个简单的状态过渡流程，所有选项都将遵循。 他们以草案状态开始，准备好后，他们的州将被批准。 当其结束日期过后，可以将其移入存档状态。 在该状态下，通过再次将它们移入起草状态，可以删除或重用它们。

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** -此属性用于实例的生命周期管理。 该值表示一个工作流状态，用于指示优惠是否仍在建设中(value = draft)，运行时通常可以考虑(value = approved)，或者如果它不应再使用(value = archived)。

对实例执行简单的PATCH操作通常仅用于操作属 `xdm:status` 性：

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 该 `schemaId` 参数必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer` 或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果优惠是回退优惠。

### 展示和放置

优惠是具有内容表示的决策选项。 当作出决定时，选择该选项，并使用其标识符来获取需要提供的位置的内容或内容引用。 一个优惠可以有多个表示，但每个表示都需要具有不同的放置参照。 这可确保在给定位置下可以明确确定表示形式。
在判定操作期间，与活动对象一起确定放置。 没有以该位置作为参照的表示的优惠会自动从选择的列表中消除。

在将表示添加到优惠之前，放置实例必须存在。 这些实例将创建模式标识符`https://ns.adobe.com/experience/offer-management/offer-placement`。

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 该 `schemaId` 参数必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer` 或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果优惠是回退优惠。

Placement **实例** 可以具有以下属性：

- **`xdm:name`** -包含位置的指定名称，以在人机交互和用户界面中引用该位置。
- **`xdm:description`** -用于传达在整个消息投放中如何使用此位置中的内容的可读意图。 当投放渠道定义新位置时，他们可以在此属性中添加更多信息，以便内容创建者能够相应地创建或选择内容。 这些指令不会正式解释或执行。 此财产仅用作交流意图的场所。
- **`xdm:channel`** -渠道的URI。 该渠道指示要将动态内容交付到的位置。 渠道约束不仅用于传达优惠的使用位置，还用于确定用于体验的内容编辑器或验证程序。
- **`xdm:componentType`** -可在此位置描述的位置中显示的内容的模型标识符，即URI。 组件类型包括：图像链接、html或纯文本。 每个组件类型可能暗示内容项目可能具有的一组特定属性（模型）。 可以扩展组件类型的列表。 有三个预定义的组件类型值：
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**，此位置中预期元件的媒体类型的约束。 一种组件类型（如不同的图像格式）可能有多个媒体类型。

**优惠中** ，表示项在数组属性中具有对象结构 `xdm:representations`。 每个项目都可以具有以下属性：

- **`xdm:placement`** -此属性包含对放置实例的引用。 将表示法添加到优惠时，将检查该值。 具有该URI的放置实例必须存在，且不得标记为已删除。 此外，执行检查以确保优惠实例的放置参照没有两个具有相同值的表示。
- **`xdm:components`** -内容组件是与特定优惠呈现关联的片段。 这些片段稍后用于构建最终用户体验。 请注意，决策服务本身并不构成完整的最终用户体验。 以下属性是每个组件的模型的一部分。
   - **`@type`** -此属性标识组件类型。 此概念的另一个名称是内容片段模型。 组 `@type` 件只是由组合最终用户体验的应用程序或服务定义的模型的URI。
   - **`repo:id`** -此属性包含存储资产的存储库中组件的主资源的全局唯一、不可变的标识符。
   - **`repo:name`** -此属性包含存储库中资产的可读名称。 此名称由用户定义，不保证唯一。
   - **`repo:resolveURL`** -此属性包含用于读取内容存储库中资产的唯一资源定位器。 这样，在客户端不了解要调用的API的情况下，获取资产会更加容易。 URL返回资产主要资源的字节。
   - **`dc:format`** -此属性来自都柏林核心元数据计划。 格式可用于确定显示或操作资源所需的软件、硬件或其他设备。 建议的最佳实践是从受控词汇中选择一个值(例如，定义计算机媒体格式的Internet媒体类型的列表)。
   - **`dc:language`** -此属性包含资源的语言或语言。 语言在IETF RFC 3066中定义的语言代码中指定。

属性中表示有三种预定义的组件 `@type` 类型：

- https<span></span>://ns.adobe.com/experience/优惠管理/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/优惠管理/content-component-text
- https<span></span>://ns.adobe.com/experience/优惠管理/content-component-html

根据属性的值，将 `@type` 包含 `xdm:components` 其他属性：

- **`xdm:linkURL`** -当组件是图像链接时显示。 此属性将包含与图像关联的链接，并且当最 `user-agent` 终用户与优惠的内容交互时，该链接将导航到该链接。
- **`xdm:copyline`** -当组件是文本时使用。 除了引用文本资产(例如，对于可能包含格式的长表单文本优惠)之外，短文本字符串还可直接存储在xdm:copyline属性中。

客户端可以使用其他属性来设置和评估上下文处理说明。 例如，优惠UI库客户端添加了以下可选属性以更轻松地处理显示：

- 在阵列中的每个项 `xdm:components` 目中，优惠库UI客户端会添加以下属性。 在不了解对UI的影响的情况下，不应删除或处理这些属性：
   - **`offerui:previewThumbnail`** -这是优惠库UI用来显示资产呈现的可选属性。 此演绎版与资产本身不同。 例如，内容可以是HTML，再现是仅显示近似值的位图图像。 此（低质量）再现显示在优惠的表示块中。

优惠实例上的PATCH操作示例说明如何操作表示：

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 该 `schemaId` 参数必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer` 或 `https://ns.adobe.com/experience/offer-management/fallback-offer` 如果优惠是回退优惠。

当尚无属性时，PATCH操作可能会失 `xdm:representations` 败。 在这种情况下，上述添加操作前面可能还有另一个创建数组的添加操作， `xdm:representations` 或者单个添加操作直接设置数组。
描述的模式和属性用于所有优惠类型、个性化优惠和备用优惠。 以下两节介绍了个性化优惠各方面的约束和决策规则。

## 设置优惠约束

### 日历约束

通常，决策选项可以给出开始和结束日期和时间，作为日历约束。 属性嵌入在属性中 `xdm:selectionConstraint`:

- **`xdm:startDate`** -此属性指示开始日期和时间。 该值是按RFC 3339规则格式化的字符串，如以下时间戳：“2019-06-13T11:21:23.356Z”。
尚未达到其开始日期和时间的决策选项在决策中尚不符合资格。
- **`xdm:endDate`** -此属性指示结束日期和时间。 该值是按RFC 3339规则格式化的字符串，如以下时间戳：“2019-07-13T11:00:00.000Z”已通过其结束日期和时间的决策选项在决策过程中不再被认为是合格的。

更改日历约束可以通过以下PATCH调用实现：

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 回退优惠没有任何约束。

### 封闭约束

封顶约束是定义封顶参数的决策选项中的一个组件。 限制是限制一个用户档案以及所有用户档案可建议的选项次数的过程。 这些属性包含一个必须大于或等于1的整数值。 属性嵌套在属性中 `xdm:cappingConstraint`:

- **`xdm:globalCap`** -全局上限是限制优惠总体可建议多少次的限制。
- **`xdm:profileCap`** -用户档案上限是对向特定用户档案提议优惠的次数的限制。

在个性化优惠上设置或更改限制约束可以通过以下PATCH调用实现：

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 回退优惠没有任何约束。

要删除限制值，操作“add”将替换为操作“remove”。 请注意，限制值单独存在，也可以单独设置或删除。

### 资格限制

优惠可以在决策过程中有条件地被选择。 当个性化优惠引用合格规则时，对于给定用户档案，要考虑的优惠对象，该规则的条件必须计算为true。 这些合格规则是独立于决策选项创建和管理的，同一规则可以从多个个性化优惠中引用。

对规则的引用嵌入在属性中 `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** -此属性包含对合格规则的引用。 该值是模式https://ns.adobe.com/experience/offer-management/eligibility-rule `@id` 的实例。

添加和删除规则也可以通过PATCH操作完成：

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 回退优惠没有任何约束。

请注意，合格规则与日历约束一 `xdm:selectionConstraint` 起嵌入在属性中。 PATCH操作不应尝试删除整个属 `SelectionConstraint` 性。

## 设置优惠的优先级

将排列符合条件的决策选项，以确定给定用户档案的最佳选项。 为了支持等级并且在等级不能由另一个机制确定的情况下提供默认值，可以为每个个性化优惠设置基本优先级。
基本优先级嵌入到属性中 `xdm:rank`:

- **`xdm:priority`** -此属性表示在没有已知的优惠特定排名顺序时，选择一个用户档案而选择另一个排序的默认顺序。 如果比较优先级值之后，两个或两个以上个性化优惠仍然绑定，则随机选择一个个性化优惠建议并在该个性化区域中使用。 此属性的值必须是大于或等于0的整数。

通过以下PATCH调用可以调整基本优先级：

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer`。 备用优惠没有任何排名属性。

## 管理决策规则

合格规则保留被评估的条件，以确定给定的决策选项是否符合给定用户档案。 将规则附加到一个或多个决策选项隐含地定义，对于此选项，规则必须计算为true，才能为此用户考虑该选项。 该规则可以包含用户档案属性测试，可以评估与此用户档案的体验事件相关的表达式，并可以包含传递给决策请求的上下文数据。 例如，条件可以描述为：

> “包括那些拥有精英地位、在过去6个月中曾三次坐过航班的个人，他们的航班号码与当前航班的航班号相同。”

将使用模式标识符https://ns.adobe.com/experience/offer-management/eligibility-rule创建实例。 创建 `_instance` 或更新调用的属性如下所示：

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/eligibility-rule`。

规则的condition属性中的值包含PQL表达式。 上下文数据通过特殊路径表达式@{schemaID}引用。

规则自然地与Experience Platform中的区段对齐，通常，规则只需通过测试用户档案的属性来重复使用区段的意 `segmentMembership` 图。 该属 `segmentMembership` 性包含已评估的区段条件的结果。 这允许组织定义其特定域的受众一次，命名它们，然后评估条件一次。

## 管理优惠集合

### 创建标记和标记优惠

优惠可以组织到集合中，其中每个集合定义应用的过滤条件。 当前，集合中的筛选器表达式可以具有以下两种表单之一：

1. 优惠 `@id` 的参数必须与列表中的标识符中的一个匹配，才能使优惠位于集合中。 此过滤器只是集合中优惠的URI的明细列表。
2. 优惠可以具有标记引用的列表，集合的过滤器由一列表标记组成。 优惠位于集合中：\
   a.任何过滤器的标记都与优惠的标记之一匹配\
   b.过滤器的所有标记都与优惠的一个标记匹配

标记是可以链接到优惠实例的简单实例。 它们是自己的实例，并带有一个名称来显示它们。 该名称在实例中必须是唯一的，以便更轻松地在用户界面中显示它们。

标记对象用于在决策选项(优惠)中建立分类。 一个标签可以由许多优惠链接到，而一个优惠可以具有许多标签引用。 通过引用与给定标签实例集相关的所有优惠来建立优惠类别。

使用模式标识符https://ns.adobe.com/experience/offer-management/tag创建标记实例。 创建 `_instance` 或更新调用的属性如下所示：

```json
{
  "xdm:name": "credit card"
} 
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/tag`。


可以使用优惠引用创建列表实例，如：

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

或者，也可以修补优惠以更改其标记列表:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

对于这两种情况，请参 [阅更新实例和修补实例](#updating-and-patching-instances) ，以了解完整的cURL语法。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/personalized-offer`。

请注意， `xdm:tags` 要成功添加操作，该属性必须已存在。 实例中不存在标签，PATCH操作可以先添加数组属性，然后向该数组添加标签引用。

### 为优惠集合定义过滤器

过滤器实例是使用模式标识符https://ns.adobe.com/experience/offer-management/offer-filter创建的。 创建 `_instance` 或更新调用的属性可能如下：

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/offer-filter`。

- **`xdm:filterType`** -此属性指示过滤器是使用标记设置的，还是直接按其id引用优惠。 当过滤器设置为使用标记时，过滤器类型可进一步指示是否所有标记必须与特定优惠上的标记匹配，或者给定的标记中的任何一个足以使优惠符合筛选条件。 此enum属性的有效值为：
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** -属性包含URI数组，这些URI是对优惠实例或标记实例的引用，具体取决于的值 `xdm:filterType`。.

以下调用说明在直接引 `_instance` 用优惠时，创建或更新调用的属性的外观：

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## 管理活动

优惠活动用于控制决策过程。 它指定应用于总库存的优惠过滤器，以按主题/类别缩小优惠，将库存缩小到那些适合保留空间的优惠，并指定在组合约束取消所有可用的个性化选项(优惠)的资格时的备用选项。

将使用活动标识符创建模式实例`https://ns.adobe.com/experience/offer-management/offer-activity`。 创建 `_instance` 或更新调用的属性如下所示：

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/offer-activity`。

- **`xdm:name`** -此必填属性包含活动名。 该名称会显示在各种用户界面中。
- **`xdm:status`** -此属性用于实例的生命周期管理。 该值表示工作流状态，用于指示活动是否仍在构建中（值=草稿），运行时通常可以考虑（值=实时），或者如果它不应再使用（值=存档）。
- **`xdm:placement`** -包含对优惠置入的引用的必需属性，当决策成为本活动的上下文时，该置入应用于库存。 该值是所使用的优惠位`@id`置的URI()。
- **`xdm:filter`** -包含对优惠筛选器的引用的强制属性，当在本活动的上下文中做出决策时，该筛选器将应用于库存。 该值是所使用的优惠`@id`过滤器的URI()。
- **`xdm:fallback`** -包含对回退优惠的引用的必需属性。 当此活动的决策不符合任何个性化优惠时，将使用回退优惠。 该值是回退优惠实`@id`例的URI()。

### 管理备用优惠

在创建活动实例之前，必须存在有资格放置活动的备用优惠。 将使用优惠标识符创建回退模式实例`https://ns.adobe.com/experience/offer-management/fallback-offer`。 创 `_instance` 建或更新调用的属性包含个性化优惠具有的相同常规属性，但不能具有任何其他约束。

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

有关 [完整的cURL语法](#updating-and-patching-instances) ，请参阅更新和修补实例。 参数 `schemaId` 必须为 `https://ns.adobe.com/experience/offer-management/fallback-offer`。

