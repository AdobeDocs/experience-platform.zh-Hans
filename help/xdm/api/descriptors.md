---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: 描述符
description: 模式注册表API中的/descriptors端点允许您以编程方式管理体验应用程序中的XDM描述符。
topic: developer guide
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 1%

---


# 描述符端点

模式定义数据实体的静态视图，但不提供关于基于这些模式（例如数据集）的数据如何彼此关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述模式的这些关系和其他解释性元数据。

模式描述符是租户级元数据，这意味着它们是IMS组织特有的，所有描述符操作都在租户容器中进行。

每个模式可以有一个或多个模式描述符实体应用到它。 每个模式描述符实体都包 `@type` 括一个描 `sourceSchema` 述符及其应用。 应用这些描述符后，这些描述符将应用于使用该模式创建的所有数据集。

API `/descriptors` 中的端点允许您 [!DNL Schema Registry] 以编程方式管理体验应用程序中的描述符。

## 入门指南

本指南中使用的端点是API的一 [[!DNL Schema Registry] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索描述符列表 {#list}

您可以通过向列表请求来GET组织定义的所有描述符 `/tenant/descriptors`。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

响应格式取决于在请 `Accept` 求中发送的标头。 请注意， `/descriptors` 端点使 `Accept` 用的头与API中的所有其他端点不 [!DNL Schema Registry] 同。

>[!IMPORTANT]
>
>描述符需要用 `Accept` 替换的唯一标 `xed` 头， `xdm`并且还要优惠描述符 `link` 特有的选项。 以下示 `Accept` 例调用中包含了正确的标题，但要确保在使用描述符时使用正确的标题，请务必格外小心。

| `Accept` 标题 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |
| `application/vnd.adobe.xdm-v2+json` | 必 `Accept` 须使用此头才能使用分页功能。 |

**响应**

该响应包括每个具有定义描述符的描述符类型的数组。 换句话说，如果没有某个定义的描述 `@type` 符，注册表将不会返回该描述符类型的空数组。

使用标题 `link` 时，每个 `Accept` 描述符都以格式显示为数组项 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

如果要视图特定描述符的详细信息，可以使用其查找(GET)单个描述符 `@id`。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 查找的描述符。 |

**请求**

以下请求按描述符的值检 `@id` 索描述符。 描述符未版本化，因此 `Accept` 在查找请求中不需要标头。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回描述符的详细信息，包括 `@type` 其 `sourceSchema`和的详细信息，以及根据描述符的类型而有所不同的其他信息。 返回的 `@id` 应与请求中提 `@id` 供的描述符匹配。

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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 创建描述符 {#create}

可以通过向端点发出POST请求来创建新的描 `/tenant/descriptors` 述符。

>[!IMPORTANT]
>
>它允 [!DNL Schema Registry] 许您定义几种不同的描述符类型。 每个描述符类型都需要在请求主体中发送其自己的特定字段。 有关描述 [符的完整列表](#defining-descriptors) ，请参阅附录以及定义它们所需的字段。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例模式的“电子邮件地址”字段上定义标识描述符。 这会告 [!DNL Experience Platform] 诉您使用电子邮件地址作为标识符来帮助拼合有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回HTTP状态201（已创建）和新创建描述符的详细信息，包括其详细信 `@id`息。 是 `@id` 由分配的只读字段，用 [!DNL Schema Registry] 于在API中引用描述符。

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

可以通过将描述符包含在PUT `@id` 请求的路径中来更新它。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 更新的描述符的名称。 |

**请求**

此请求实质上重写描述符，因此请求主体必须包括定义该类型的描述符所需的所有字段。 换言之，要更新(PUT)描述符的请求有效负荷与要创建()同 [一类型描述符的有效负荷](#create) (POST)相同。

>[!IMPORTANT]
>
>与使用POST请求创建描述符一样，每个描述符类型都要求在PUT请求负载中发送其自己的特定字段。 有关描述 [符的完整列表](#defining-descriptors) ，请参阅附录以及定义它们所需的字段。

以下示例更新标识描述符以引用其 `xdm:sourceProperty` 他(`mobile phone`)并将其 `xdm:namespace` 更改为 `Phone`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回HTTP状态201（已创建） `@id` 和更新的描述符(应与请求中发 `@id` 送的描述符匹配)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行查 [找(GET](#lookup) )请求以视图描述符将显示字段现已更新以反映PUT请求中发送的更改。

## 删除描述符 {#delete}

有时您可能需要删除已在中定义的描述符 [!DNL Schema Registry]。 这是通过引用要删除的描述符 `@id` 的DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 删除的描述符的名称。 |

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

要确认描述符已被删除，可以对描述符 [执行查](#lookup) 找请求 `@id`。 该响应返回HTTP状态404（未找到），因为描述符已从中删除 [!DNL Schema Registry]。

## 附录

下节提供有关在API中使用描述符的其他 [!DNL Schema Registry] 信息。

### 定义描述符 {#defining-descriptors}

以下各节概述了可用的描述符类型，包括定义每种类型的描述符所需的字段。

#### 标识描述符

标识描述符表示“[!UICONTROL sourceSchema]”的“sourceProperty[!UICONTROL ”是]由Adobe Experience Platform标识服务描 [!DNL Identity] 述的字段 [](../../identity-service/home.md)。

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
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定 `$id` 义描述符的模式的URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不以“/”结尾。 不要在路径中包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:namespace` | 标 `id` 识命名空间 `code` 的或值。 列表的命名空间可使用找到。 [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) |
| `xdm:property` | 或 `xdm:id` , `xdm:code`具体取决于使 `xdm:namespace` 用。 |
| `xdm:isPrimary` | 可选布尔值。 如果为true，则将字段指示为主标识。 模式只能包含一个主标识。 |

#### 友好名称描述符

友好的名称描述符允许用户修 `title`改核 `description`心库 `meta:enum` 模式字段的、和值。 在处理“eVar”和您希望标记为包含特定于您组织的信息的其他“通用”字段时特别有用。 UI可以使用这些字段显示更友好的名称或仅显示具有友好名称的字段。

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
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定 `$id` 义描述符的模式的URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不以“/”结尾。 不要在路径中包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:title` | 要为此字段显示的新标题，用标题大小写写写。 |
| `xdm:description` | 可以随标题一起添加可选描述。 |
| `meta:enum` | 如果以字符 `xdm:sourceProperty` 串字段表示， `meta:enum` 则确定UI中字段的建议值 [!DNL Experience Platform] 列表。 请务必注意，不 `meta:enum` 要声明明细列表或为XDM字段提供任何数据验证。<br><br>这应仅用于由Adobe定义的核心XDM字段。 如果源属性是您的组织定义的自定义字段，则应直接通过对字 `meta:enum` 段的父资源的PATCH请求来编辑字段的属性。 |

#### 关系描述符

关系描述符描述了两个不同模式之间的关系，这些关系基于和中描述的 `sourceProperty` 属性 `destinationProperty`。 有关详细信息，请 [参阅有关定义两个模式之间的关系](../tutorials/relationship-api.md) 的教程。

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
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定 `$id` 义描述符的模式的URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 源模式中定义关系的字段的路径。 应以“/”开头，而不以“/”结尾。 路径中不要包含“properties”（例如，“/personalEmail/address”，而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:destinationSchema` | 此描 `$id` 述符正在定义与的关系的目标模式的URI。 |
| `xdm:destinationVersion` | 目标模式的主版本。 |
| `xdm:destinationProperty` | 目标目标中模式字段的可选路径。 如果忽略此属性，则目标字段由包含匹配引用标识描述符的任何字段推断出来（请参阅下文）。 |


#### 引用标识描述符

引用标识描述符提供对模式字段主标识的引用上下文，允许其被其他模式中的字段引用。 字段必须已用标识描述符进行标记，然后才能将引用描述符应用于这些字段。

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
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定 `$id` 义描述符的模式的URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 源模式中定义描述符的字段的路径。 应以“/”开头，而不以“/”结尾。 路径中不要包含“properties”（例如，“/personalEmail/address”，而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:identityNamespace` | 源属性的标识命名空间代码。 |