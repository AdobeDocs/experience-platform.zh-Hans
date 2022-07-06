---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；架构注册；架构注册；描述符；描述符；描述符；描述符；标识符；身份；友好名称；友好名称；替代显示信息；引用；关系；关系
solution: Experience Platform
title: 描述符API端点
description: 通过架构注册表API中的/descriptors端点，您可以以编程方式管理体验应用程序中的XDM描述符。
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 65a6eca9450b3a3e19805917fb777881c08817a0
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 3%

---

# 描述符端点

架构定义数据实体的静态视图，但不提供有关基于这些架构（例如数据集）的数据如何彼此关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述这些关系以及有关架构的其他解释性元数据。

架构描述符是租户级别的元数据，这意味着它们对IMS组织是唯一的，所有描述符操作都在租户容器中进行。

每个模式可以应用一个或多个模式描述符实体。 每个模式描述符实体包括描述符 `@type` 和 `sourceSchema` 适用的。 应用后，这些描述符将应用于使用架构创建的所有数据集。

的 `/descriptors` 的端点 [!DNL Schema Registry] API允许您以编程方式管理体验应用程序中的描述符。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索描述符列表 {#list}

通过向发出GET请求，您可以列出贵组织定义的所有描述符 `/tenant/descriptors`.

**API格式**

```http
GET /tenant/descriptors
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

响应格式取决于 `Accept` 请求中发送的标头。 请注意， `/descriptors` 端点使用 `Accept` 与中所有其他端点不同的标头 [!DNL Schema Registry] API。

>[!IMPORTANT]
>
>描述符需要唯一 `Accept` 替换的标题 `xed` with `xdm`，并且还提供 `link` 描述符特有的选项。 适当 `Accept` 以下示例调用中包含标头，但请格外小心，以确保在使用描述符时使用正确的标头。

| `Accept` 标题 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |
| `application/vnd.adobe.xdm-v2+json` | 此 `Accept` 必须使用头才能利用分页功能。 |

{style=&quot;table-layout:auto&quot;}

**响应**

响应包括每个具有定义描述符的描述符类型的数组。 换句话说，如果没有某个 `@type` 定义时，注册表不会为该描述符类型返回空数组。

使用 `link` `Accept` 标头中，每个描述符都以数组项的形式显示 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## 查找描述符 {#lookup}

如果要查看特定描述符的详细信息，可以使用其查找(GET)单个描述符 `@id`.

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 要查找的描述符。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求通过其 `@id` 值。 描述符未版本化，因此没有 `Accept` 查找请求中需要标头。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回描述符的详细信息，包括其 `@type` 和 `sourceSchema`，以及根据描述符类型而异的其他信息。 返回的 `@id` 应与描述符匹配 `@id` 请求中提供。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 创建描述符 {#create}

您可以通过向 `/tenant/descriptors` 端点。

>[!IMPORTANT]
>
>的 [!DNL Schema Registry] 允许您定义多种不同的描述符类型。 每个描述符类型要求在请求正文中发送其自己的特定字段。 请参阅 [附录](#defining-descriptors) 以获取描述符和定义它们所需的字段的完整列表。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例架构的“email address”字段上定义标识描述符。 这说明 [!DNL Experience Platform] 将电子邮件地址用作标识符，以帮助拼合有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功响应会返回HTTP状态201（已创建）以及新创建描述符的详细信息，包括其 `@id`. 的 `@id` 是由 [!DNL Schema Registry] 和用于在API中引用描述符。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 更新描述符 {#put}

您可以通过包含 `@id` 在PUT请求的路径中。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 要更新的描述符的。 |

{style=&quot;table-layout:auto&quot;}

**请求**

此请求实质上会重写描述符，因此请求正文必须包含定义该类型描述符所需的所有字段。 换句话说，用于更新(PUT)描述符的请求有效负载与到的有效负载相同 [创建(POST)描述符](#create) 相同类型。

>[!IMPORTANT]
>
>与使用POST请求创建描述符一样，每个描述符类型要求在PUT请求负载中发送其自己的特定字段。 请参阅 [附录](#defining-descriptors) 以获取描述符和定义它们所需的字段的完整列表。

以下示例更新了标识描述符以引用其他 `xdm:sourceProperty` (`mobile phone`)并更改 `xdm:namespace` to `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功响应会返回HTTP状态201（已创建）和 `@id` 更新的描述符(应与 `@id` 发送)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行 [查找(GET)请求](#lookup) 要查看描述符，将显示字段现已更新，以反映在PUT请求中发送的更改。

## 删除描述符 {#delete}

有时，您可能需要从 [!DNL Schema Registry]. 这是通过发出引用的DELETE请求来完成的 `@id` 要删除的描述符。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 要删除的描述符。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

要确认已删除描述符，您可以执行 [查找请求](#lookup) 对象 `@id`. 响应会返回HTTP状态404（未找到），因为描述符已从 [!DNL Schema Registry].

## 附录

以下部分提供了有关在 [!DNL Schema Registry] API。

### 定义描述符 {#defining-descriptors}

以下各节概述了可用的描述符类型，包括定义每种类型的描述符的必填字段。

#### 身份描述符

标识描述符表示[!UICONTROL sourceProperty]“”[!UICONTROL sourceSchema]“是 [!DNL Identity] 字段，如 [Adobe Experience Platform Identity Service](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 定义的描述符类型。 对于标识描述符，必须将此值设置为 `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | 的 `$id` 定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不应以“/”结尾。 在路径中不要包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:namespace` | 的 `id` 或 `code` 标识命名空间的值。 使用 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | 任一 `xdm:id` 或 `xdm:code`，具体取决于 `xdm:namespace` 已使用。 |
| `xdm:isPrimary` | 可选布尔值。 当为true时，将字段指示为主标识。 架构只能包含一个主标识。 |

{style=&quot;table-layout:auto&quot;}

#### 友好名称描述符 {#friendly-name}

友好名称描述符允许用户修改 `title`, `description`和 `meta:enum` 核心库架构字段的值。 在使用“eVar”和您希望标记为包含特定于贵组织的信息的其他“通用”字段时，特别有用。 UI可以使用这些字段显示更友好的名称，或仅显示具有友好名称的字段。

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 定义的描述符类型。 对于友好名称描述符，必须将此值设置为 `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | 的 `$id` 定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不应以“/”结尾。 在路径中不要包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:title` | 您希望为此字段显示的新标题，在标题大小写中写成。 |
| `xdm:description` | 可以添加可选描述以及标题。 |
| `meta:enum` | 如果字段指示为 `xdm:sourceProperty` 是字符串字段， `meta:enum` 确定 [!DNL Experience Platform] UI。 请务必注意， `meta:enum` 不声明枚举或为XDM字段提供任何数据验证。<br><br>此字段应仅用于由Adobe定义的核心XDM字段。 如果源属性是由您的组织定义的自定义字段，则应该编辑该字段的 `meta:enum` 属性(通过PATCH请求)。 |

{style=&quot;table-layout:auto&quot;}

#### 关系描述符

关系描述符描述了两个不同模式之间的关系，这些模式基于 `sourceProperty` 和 `destinationProperty`. 请参阅 [定义两个架构之间的关系](../tutorials/relationship-api.md) 以了解更多信息。

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 定义的描述符类型。 对于关系描述符，必须将此值设置为 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 的 `$id` 定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 在源架构中定义关系的字段路径。 应以“/”开头，而不以“/”结尾。 在路径中不要包含“properties”（例如，“/personalEmail/address”，而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:destinationSchema` | 的 `$id` 此描述符正在定义与的关系的目标架构的URI。 |
| `xdm:destinationVersion` | 目标架构的主要版本。 |
| `xdm:destinationProperty` | 目标架构中目标字段的可选路径。 如果忽略此属性，则目标字段将由包含匹配引用标识描述符的任何字段推断（请参阅下文）。 |

{style=&quot;table-layout:auto&quot;}

#### 引用标识描述符

引用标识描述符提供对模式字段主标识的引用上下文，从而允许其他模式中的字段引用该字段。 目标架构必须已经定义了主标识字段，然后才能由其他架构通过此描述符引用该字段。

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 定义的描述符类型。 对于引用标识描述符，必须将此值设置为 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 的 `$id` 定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 源架构中用于引用目标架构的字段的路径。 应以“/”开头，而不以“/”结尾。 不要在路径中包含“properties”(例如， `/personalEmail/address` 而不是 `/properties/personalEmail/properties/address`)。 |
| `xdm:identityNamespace` | 源属性的标识命名空间代码。 |

{style=&quot;table-layout:auto&quot;}

#### 已弃用的字段描述符

您可以 [弃用自定义XDM资源中的字段](../tutorials/field-deprecation.md#custom) 通过添加 `meta:status` 属性设置为 `deprecated` 到相关字段。 但是，如果要弃用架构中标准XDM资源提供的字段，则可以为相关架构分配一个已弃用的字段描述符，以实现相同的效果。 使用 [正确 `Accept` 标题](../tutorials/field-deprecation.md#verify-deprecation)，则您可以在API中查找架构时，查看该架构已弃用的标准字段。

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 描述符的类型。 对于字段弃用描述符，必须将此值设置为 `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 将描述符应用到的架构。 |
| `xdm:sourceVersion` | 要将描述符应用到的架构的版本。 应设置为 `1`. |
| `xdm:sourceProperty` | 将描述符应用到的架构中属性的路径。 如果要将描述符应用于多个属性，可以以数组的形式提供路径列表(例如， `["/firstName", "/lastName"]`)。 |

{style=&quot;table-layout:auto&quot;}
