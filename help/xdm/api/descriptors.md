---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 描述符
topic: developer guide
translation-type: tm+mt
source-git-commit: c3d23ce0081932e61f50d426ac6d98ab7f4dfa3b
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 1%

---


# 描述符

模式定义数据实体的静态视图，但不提供关于基于这些模式（例如数据集）的数据如何彼此关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述模式的这些关系和其他解释性元数据。

模式描述符是租户级元数据，这意味着它们是IMS组织特有的，所有描述符操作都在租户容器中进行。

每个模式可以有一个或多个模式描述符实体应用到它。 每个模式描述符实体都包 `@type` 括一个描 `sourceSchema` 述符及其应用。 应用这些描述符后，这些描述符将应用于使用该模式创建的所有数据集。

此文档提供描述符的示例API调用，以及可用描述符的完整列表以及定义每种类型所需的字段。

>[!NOTE] 描述符需要用唯一的“接受”标 `xed` 头替换， `xdm`但在其它方面与“接受”标题在模式注册表中其他位置使用非常相似。 以下示例调用中包含了正确的接受标头，但要确保使用正确的标头，请格外小心。

## 列表描述符

单个GET请求可用于返回由您的组织定义的所有描述符的列表。

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

响应格式取决于请求中发送的接受头。 请注意，该 `/descriptors` 端点使用的接受标头与模式注册表API中的所有其他端点不同。

描述符接受标头 `xed` 替换 `xdm`为，并优惠 `link` 描述符特有的选项。

| 接受 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |

**响应**

该响应包括每个具有定义描述符的描述符类型的数组。 换句话说，如果没有某个定义的描述 `@type` 符，注册表将不会返回该描述符类型的空数组。

使用“接 `link` 受”标头时，每个描述符都以数组项的形式显示 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## 查找描述符

如果要视图特定描述符的详细信息，可以使用其查找(GET)单个描述符 `@id`。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 查找的描述符的名称。 |

**请求**

描述符未版本化，因此在查找请求中不需要“接受”标头。

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

## 创建描述符

模式注册表允许您定义几种不同的描述符类型。 每个描述符类型都要求在POST请求中发送其自己的特定字段。 描述符的完整列表以及定义描述符所需的字段，可在定义描述符的附录部分 [中找到](#defining-descriptors)。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例模式的“电子邮件地址”字段上定义标识描述符。 这会告知Experience Platform将电子邮件地址用作标识符，以帮助拼合有关个人的信息。

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

成功的响应会返回HTTP状态201（已创建）和新创建描述符的详细信息，包括其详细信 `@id`息。 是 `@id` 由模式注册表分配的只读字段，用于在API中引用描述符。

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

## 更新描述符

可以通过发出引用要在请求路径中更新的 `@id` 描述符的PUT请求来更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 更新的描述符的名称。 |

**请求**

此请求基 _本上重写描述符_ ，因此请求主体必须包括定义该类型的描述符所需的所有字段。 换言之，要更新描述符的请求有效负荷(PUT)与要创建相同类型描述符的有效负荷(POST)相同。

在此示例中，标识描述符正被更新为引 `xdm:sourceProperty` 用其他（“手机”）并将 `xdm:namespace` 其更改为“Phone”。

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

有关属性和 `xdm:namespace` 详细 `xdm:property`信息（包括如何访问属性）的详细信息，请参阅定义描 [述符的附录部分](#defining-descriptors)。

**响应**

成功的响应会返回HTTP状态201（已创建） `@id` 和更新的描述符(应与请求中发 `@id` 送的描述符匹配)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行查找(GET)请求以视图描述符将显示字段现已更新以反映PUT请求中发送的更改。

## 删除描述符

有时您可能需要从模式注册表中删除已定义的描述符。 这是通过引用要删除的描 `@id` 述符的DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 删除的描述符的名称。 |

**请求**

删除描述符时，不需要接受标头。

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

要确认描述符已被删除，您可以对描述符执行查找请求 `@id`。 该响应返回HTTP状态404（未找到），因为描述符已从模式注册表中删除。

## 附录

下节提供有关在模式注册表API中使用描述符的其他信息。

### 定义描述符

以下各节概述了可用的描述符类型，包括定义每种类型的描述符所需的字段。

#### 标识描述符

标识描述符表示“sourceSchema”的“sourceProperty”是Adobe Experience Platform Identity Service描述的 [“标识”字段](../../identity-service/home.md)。

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
| `xdm:namespace` | 标 `id` 识命名空间 `code` 的或值。 使用Identity Service API可以找到一列表 [命名空间](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。 |
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
| `meta:enum` | 如果由指示的字 `xdm:sourceProperty` 段是字符串字段， `meta:enum` 则确定Experience Platform UI中字段的建议值的列表。 请务必注意，不 `meta:enum` 要声明明细列表或为XDM字段提供任何数据验证。<br><br>这应仅用于Adobe定义的核心XDM字段。 如果源属性是您的组织定义的自定义字段，则应直接通过PATCH `meta:enum` 请求编辑该字段 [的属性](./update-resource.md)。 |

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

引用标识描述符为模式字段提供引用上下文，允许其与目标模式的主标识字段链接。 字段必须已用标识描述符进行标记，然后才能将引用描述符应用于这些字段。

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