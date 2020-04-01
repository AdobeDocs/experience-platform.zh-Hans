---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# (Alpha)计算属性

>[!IMPORTANT]
>此文档中概述的计算属性功能当前位于alpha中，并且不适用于所有用户。 文档和功能可能会发生更改。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算的属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。

每个计算的属性都包含一个表达式（或“规则”），它计算传入数据并将所得值存储在用户档案属性或事件中。 这些计算可以帮助您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂计算。

本指南将帮助您更好地了解Adobe Experience Platform中的计算属性，并包括使用端点执行基本CRUD操作的示例API调 `/config/computedAttributes` 用。

## 入门指南

本指南中使用的API端点是实时客户用户档案API的一部分。 在继续之前，请查阅实 [时客户用户档案开发人员指南](getting-started.md)。

特别是，用户档案开发人 [员指南的入门部分](getting-started.md) ，包括指向相关主题的链接、阅读本文档中示例API调用的指南以及成功调用任何Experience Platform API所需的标题的重要信息。

## 了解计算属性

Adobe Experience Platform使您能够轻松导入和合并来自多个来源的数据，以生成实时客户用户档案。 每个用户档案都包含与个人相关的重要信息，如其联系信息、偏好和购买历史记录，为客户提供360度全方位视图。

直接读取数据字段（例如，“名”）时容易理解用户档案中收集的某些信息，而其他数据需要执行多次计算或依赖其他字段和值来生成信息（例如，“终身购买总数”）。 为了使这些数据更易于一目了然地理解，Platform允许您创建可自动执行 **这些引用和计算的计算属性** ，并在相应的字段中返回值。

计算的属性包括创建对传入数据操作的表达式（或“规则”），并将所得值存储在用户档案属性或事件中。 表达式可以通过多种不同的方式进行定义，从而允许您指定规则仅评估传入事件、传入事件和用户档案数据，或传入事件、用户档案数据和历史事件。

### 用例

计算属性的用例范围从简单计算到非常复杂的引用。 以下是计算属性的几个示例用例：

1. **百分比：** 一个简单的计算属性可以包括在记录中取两个数字字段，并将它们分成一个百分比。 例如，您可以将发送给个人的电子邮件总数除以个人打开的电子邮件数。 查看结果计算的属性字段将快速显示个人打开的电子邮件总数的百分比。
1. **应用程序使用：** 另一个示例包括聚合用户打开应用程序的次数的功能。 通过跟踪应用程序打开总数，根据个人的开放事件，您可以在用户第100次打开时向用户发送特殊优惠或消息，从而鼓励更深入地与您的品牌互动。
1. **生命周期值：** 收集持续的总数（如客户的终身购买价值）可能非常困难。 这要求每次出现新购买事件时更新历史总数。 计算属性允许您通过将生命周期值保留在单个字段中而更轻松地完成此操作，该字段会在与客户相关的每个成功购买事件后自动更新。

## 配置计算属性

为了配置计算的属性，您首先需要标识将包含计算属性值的字段。 可以使用混音将字段添加到现有模式，或通过选择已在模式中定义的字段来创建此字段。

>[!NOTE]
>计算的属性无法添加到Adobe定义的混音中的字段。 该字段必须在命名空间中， `tenant` 这意味着它必须是您定义并添加到模式中的字段。

为了成功定义计算的属性字段，必须为模式启用该模式，并作为该用户档案所基于的类的合并模式的一部分显示。 有关支持用户档案的模式和合并的详细信息，请查阅模式注册处开发人员指南部分中关于启用 [用户档案和查看合并模式的部分](../../xdm/api/getting-started.md)。 还建议查看模式构图基 [础文档中关于合并](../../xdm/schema/composition.md) 的部分。

本教程中的工作流使用一个启用用户档案的模式，并按照以下步骤定义包含计算的属性字段的新混音并确保它是正确的命名空间。 如果已在启用用户档案的模式中有一个字段处于正确的命名空间中，则可以直接继续执行创建计算属性 [的步骤](#create-a-computed-attribute)。

### 视图模式

接下来的步骤使用Adobe Experience Platform用户界面来查找模式、添加混音和定义字段。 如果您希望使用模式注册API，请参阅 [模式注册开发人员指南](../../xdm/api/getting-started.md) ，了解有关如何创建混音、向模式添加混音以及启用模式以与实时客户用户档案一起使用的步骤。

在用户界面中，单击 **左边栏中的模式**** ，然后使用“浏览”选项卡上的搜索栏快速找到要更新的模式。

![](../images/computed-attributes/Schemas-Browse.png)

找到模式后，单击其名称以打开模式编辑器，在该编辑器中可以编辑模式。

![](../images/computed-attributes/Schema-Editor.png)

### 创建混音

要创建新混音，请单 **击编辑器左侧** 的“合成 *”部分中*** “Mixins”旁边的“添加”。 此操作将打开“ **添加混音** ”对话框，您可以在该对话框中查看现有混音。 单击“创建新混音 **”单选按钮** ，以定义新混音。

为混音指定名称和说明，完成后单击“ **添加混音** ”。

![](../images/computed-attributes/Add-mixin.png)

### 向模式添加计算的属性字段

您的新混音现在应显示在“合 *成* ”下的“ *Mixins”部分*。 单击混音的名称，编辑器的“结构 **”部分将显示** 多个“添 ** 加”字段按钮。

选 **择模式名称旁边的“添加字段** ”，以添加顶级字段，或者您可以选择在模式中您喜欢的任意位置添加字段。

单击“ **添加字段** ”后，将打开一个新对象，该对象以您的租户ID命名，表明该字段处于正确的命名空间中。 在该对象中，将显示 *一个新字段* 。 如果要定义计算属性的字段为此字段，则为此。

![](../images/computed-attributes/New-field.png)

### 配置字段

使用编 *辑器右侧的* “字段属性”部分，为新字段提供必要的信息，包括其名称、显示名称和类型。

>[!NOTE]
>字段的类型必须与计算的属性值的类型相同。 例如，如果计算的属性值是字符串，则模式中定义的字段必须是字符串。

完成后，单 **击** “应用”，字段的名称及其类型将显示在编辑器的“结 *构* ”部分。

![](../images/computed-attributes/Apply.png)

### 启用模式进行用户档案

在继续之前，请确保模式已启用用户档案。 在编辑器的“结构”部分中单 *击模式名* ，以便显示“ *模式属性* ”选项卡。 如果 **用户档案** 滑块为蓝色，则模式已启用用户档案。

>[!NOTE]
>为用户档案启用模式是无法撤消的，因此，如果在启用滑块后单击该滑块，则不必冒险禁用它。

![](../images/computed-attributes/Profile.png)

您现在可以单 **击“保存** ”以保存更新的模式，并使用API继续学习教程的其余部分。

### 创建计算属性 {#create-a-computed-attribute}

在识别计算属性字段并确认已为模式启用用户档案后，您现在可以配置计算属性。

首先，向端点发出POST请求， `/config/computedAttributes` 请求主体包含您要创建的计算属性的详细信息。

**API格式**

```http
POST /config/computedAttributes
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 属性 | 描述 |
|---|---|
| `name` | 计算的属性字段的名称，作为字符串。 |
| `path` | 包含计算属性的字段的路径。 此路径位于模式的属 `properties` 性中，且路径中不应包含字段名。 编写路径时，忽略多个级别的属 `properties` 性。 |
| `{TENANT_ID}` | 如果您不熟悉您的租户ID，请参阅模式注册开发人员指南中查找租户ID [的步骤](../../xdm/api/getting-started.md#know-your-tenant_id)。 |
| `description` | 计算属性的描述。 在定义了多个计算属性后，这特别有用，因为它将帮助IMS组织中的其他人确定要使用的正确计算属性。 |
| `expression.value` | 有效的用户档案查询语言(PQL)表达式。 有关PQL的详细信息以及指向受支持查询的链接，请阅读 [PQL概述](../../segmentation/pql/overview.md)。 |
| `schema.name` | 包含计算的属性字段的模式所基于的类。 示例：用 `_xdm.context.experienceevent` 于基于XDM ExperienceEvent类的模式。 |

**响应**

成功创建的计算属性返回HTTP状态200(OK)和包含新创建的计算属性详细信息的响应主体。 这些详细信息包括系统生成的唯一只读 `id` 属性，可用于在其他API操作期间引用计算的属性。

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| 属性 | 描述 |
|---|---|
| `id` | 一个唯一的只读系统生成的ID，可用于在其他API操作期间引用计算的属性。 |
| `imsOrgId` | 与计算属性相关的IMS组织应与请求中发送的值匹配。 |
| `sandbox` | 沙箱对象包含在其中配置了计算属性的沙箱的详细信息。 此信息是从请求中发送的沙箱头中提取的。 有关详细信息，请参阅沙 [箱概述](../../sandboxes/home.md)。 |
| `positionPath` | 一个数组，其中包 `path` 含被解构到请求中发送的字段。 |
| `returnSchema.meta:xdmType` | 存储计算属性的字段的类型。 |
| `definedOn` | 一个数组，其中显示已定义计算的属性的合并模式。 每个合并模式包含一个对象，这意味着如果计算的属性已添加到基于不同类的多个模式，则数组中可能有多个对象。 |
| `active` | 一个布尔值，显示计算的属性当前是否处于活动状态。 默认情况下，该值为 `true`。 |
| `type` | 创建的资源类型（在此例中为“ComputedAttribute”）是默认值。 |
| `createEpoch` 和 `updateEpoch` | 分别创建和上次更新计算的属性的时间。 |


## 访问计算属性

使用API处理计算属性时，有两个选项可用于访问组织定义的计算属性。 第一种是列表所有计算的属性，第二种是视图特定的计算属性（其唯一性） `id`。

下面各节介绍了列出所有计算属性和查看特定计算属性的步骤。

### 列表计算属性 {#list-computed-attributes}

您的IMS组织可以创建多个计算属性，并且对端点执行GET请求 `/config/computedAttributes` 允许您列表组织的所有现有计算属性。

**API格式**

```http
GET /config/computedAttributes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应包括 `_page` 提供页面上计算的属性(`totalCount`)的总数和计算的属性(`pageSize`)的数。

该响应还包括由一个 `children` 或多个对象组成的数组，每个对象包含一个计算的属性的详细信息。 如果您的组织没有任何计算属性，则 `totalCount` 和 `pageSize` 将为0（零），并且数 `children` 组将为空。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 属性 | 描述 |
|---|---|
| `_page.totalCount` | IMS组织定义的计算属性总数。 |
| `_page.pageSize` | 在此结果页上返回的计算属性数。 如 `pageSize` 果等于， `totalCount`则表示只有一页结果，且已返回所有计算的属性。 如果它们不相等，则还有其他可访问的结果页面。 有关详 `_links.next` 细信息，请参阅。 |
| `children` | 由一个或多个对象组成的数组，每个对象包含单个计算属性的详细信息。 如果尚未定义计算属性，则数 `children` 组为空。 |
| `id` | 在创建计算的属性时，系统生成的唯一只读值会自动分配给该属性。 有关计算属性对象的组件的详细信息，请参阅本教程前面有关 [创建计算属性的一节](#create-a-computed-attribute) 。 |
| `_links.next` | 如果返回计算属性的单页，则 `_links.next` 为空对象，如上面的示例响应所示。 如果您的组织有许多计算属性，则这些属性将在您可以通过对值发出GET请求来访问的多个页面上 `_links.next` 返回。 |

### 视图计算的属性 {#view-a-computed-attribute}

您还可以通过向端点发出GET请求并在请求路径中包 `/config/computedAttributes` 括计算的属性ID来视图特定的计算属性。

**API格式**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要视图的计算属性的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## 更新计算的属性

如果您发现需要更新现有的计算属性，可以通过向端点发出PATCH请求并在请求路径中包含要更新的计算属性的ID来完成此操作。 `/config/computedAttributes`

**API格式**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要更新的计算属性的ID。 |

**请求**

此请求使 [用JSON修补程序格式](http://jsonpatch.com/) ，以更新“表达式”字段的“值”。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 属性 | 描述 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 有效的用户档案查询语言(PQL)表达式。 有关PQL的详细信息以及指向受支持查询的链接，请阅读 [PQL概述](../../segmentation/pql/overview.md)。 |

**响应**

成功的更新会返回HTTP状态204（无内容）和空的响应主体。 如果您希望确认更新成功，可以执行GET请求以按计算的属性ID视图该属性。

## 删除计算的属性

也可以使用API删除计算的属性。 这是通过向端点发出DELETE请求并在请 `/config/computedAttributes` 求路径中包括要删除的计算属性的ID来完成的。

>[!Note]
>删除计算的属性时请务必小心，因为该属性可能正在多个模式中使用，且DELETE操作无法撤消。

**API格式**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 参数 | 描述 |
|---|---|
| `{ATTRIBUTE_ID}` | 要删除的计算属性的ID。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**响应**

成功的删除请求将返回HTTP状态200(OK)和空的响应主体。 要确认删除成功，您可以执行GET请求以按其ID查找计算的属性。 如果删除了该属性，您将收到HTTP Status 404(Not Found)错误。

## 后续步骤

您已经学习了计算属性的基础知识，现在可以开始为组织定义这些属性了。