---
description: 了解如何在Experience Platform UI中创建输入字段，这些字段允许用户指定与如何将数据连接和导出到目标相关的各种信息。
title: 客户数据字段
exl-id: 7f5b8278-175c-4ab8-bf67-8132d128899e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 1%

---

# 通过客户数据字段配置用户输入

在Experience Platform UI中连接到目标时，您可能需要用户提供特定的配置详细信息或选择您向他们提供的特定选项。 在Destination SDK中，这些选项称为客户数据字段。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图或查看以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## 客户数据字段的用例 {#use-cases}

在需要用户将数据输入到Experience Platform UI中的各种用例中使用客户数据字段。 例如，当用户需要提供以下内容时，请使用客户数据字段：

* 云存储段名称和路径，用于基于文件的目标。
* 客户数据字段接受的格式。
* 用户可以选择的可用文件压缩类型。
* 实时（流）集成的可用端点列表。

您可以通过`/authoring/destinations`端点配置客户数据字段。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的客户数据字段配置类型，并显示了客户将在Experience Platform UI中看到的内容。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 支持的参数 {#supported-parameters}

在创建自己的客户数据字段时，您可以使用下表中描述的参数来配置其行为。

| 参数 | 类型 | 必需/可选 | 描述 |
|---------|----------|------|---|
| `name` | 字符串 | 必需 | 为您即将介绍的自定义字段提供一个名称。 此名称在Experience Platform UI中不可见，除非`title`字段为空或缺失。 |
| `type` | 字符串 | 必需 | 指示您即将引入的自定义字段的类型。 接受的值： <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | 字符串 | 可选 | 指示字段的名称，正如客户在Experience Platform UI中看到的那样。 如果此字段为空或缺失，则UI从`name`值继承字段名称。 |
| `description` | 字符串 | 可选 | 提供自定义字段的描述。 此描述在Experience Platform UI中不可见。 |
| `isRequired` | 布尔值 | 可选 | 指示是否要求用户在目标配置工作流中提供此字段的值。 |
| `pattern` | 字符串 | 可选 | 如果需要，为自定义字段实施模式。 使用正则表达式可强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请在此字段中输入`^[A-Za-z]+$`。 |
| `enum` | 字符串 | 可选 | 将自定义字段呈现为下拉菜单，并列出用户可用的选项。 |
| `default` | 字符串 | 可选 | 从`enum`列表中定义默认值。 |
| `hidden` | 布尔值 | 可选 | 指示客户数据字段是否显示在UI中。 |
| `unique` | 布尔值 | 可选 | 当您需要创建客户数据字段，且该字段的值在用户组织设置的所有目标数据流中必须是唯一的，请使用此参数。 例如，[自定义Personalization](../../../catalog/personalization/custom-personalization.md)目标中的&#x200B;**[!UICONTROL 集成别名]**&#x200B;字段必须是唯一的，这意味着流向此目标的两个单独的数据流不能具有此字段的相同值。 |
| `readOnly` | 布尔值 | 可选 | 指示客户是否可以更改字段值。 |

{style="table-layout:auto"}

在以下示例中，`customerDataFields`部分定义了用户在连接到目标时必须在Experience Platform UI中输入的两个字段：

* `Account ID`：目标平台的用户帐户ID。
* `Endpoint region`：它们将连接到的API的区域终结点。 `enum`部分创建一个下拉菜单，其中的值定义可供用户选择。

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

生成的UI体验如下图所示。

![显示客户数据字段示例的Ui图像。](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## 目标连接名称和描述 {#names-description}

创建新目标时，Destination SDK会自动将&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;字段添加到Experience Platform UI的目标连接屏幕中。 如上面的示例所示，**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;字段已在UI中呈现，但未包含在客户数据字段配置中。

>[!IMPORTANT]
>
>如果您在客户数据字段配置中添加&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;字段，用户将在UI中看到这些字段重复。

## 订购客户数据字段 {#ordering}

Experience Platform UI中反映了您在目标配置中添加客户数据字段的顺序。

例如，以下配置将相应地反映在UI中，选项按&#x200B;**[!UICONTROL 名称]**、**[!UICONTROL 描述]**、**[!UICONTROL 存储段名称]**、**[!UICONTROL 文件夹路径]**、**[!UICONTROL 文件类型]**、**[!UICONTROL 压缩格式]**&#x200B;的顺序显示。

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![显示Experience Platform UI中文件格式选项顺序的图像。](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## 分组客户数据字段 {#grouping}

您可以在一个部分中对多个客户数据字段进行分组。 在UI中设置与目标之间的连接时，用户可以查看类似字段的可视化分组并从中受益。

为此，请使用`"type": "object"`创建组，并在`properties`对象中收集所需的客户数据字段，如下图所示，其中高亮显示了&#x200B;**[!UICONTROL CSV选项]**&#x200B;分组。

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![显示UI中客户数据字段分组的图像。](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## 为客户数据字段创建下拉选择器 {#dropdown-selectors}

对于希望允许用户在多个选项之间进行选择的情况（例如，应使用哪个字符来分隔CSV文件中的字段），您可以向UI添加下拉字段。

为此，请使用如下所示的`namedEnum`对象，并为用户可以选择的选项配置`default`值。

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![屏幕录制，显示使用以上所示配置创建的下拉选择器示例。](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## 为客户数据字段创建动态下拉选择器 {#dynamic-dropdown-selectors}

对于要动态调用API并使用响应动态填充下拉菜单中的选项的情况，您可以使用动态下拉选择器。

动态下拉列表选择器与UI中的[常规下拉列表选择器](#dropdown-selectors)相同。 唯一的区别是这些值是从API动态检索的。

要创建动态下拉选择器，您必须配置两个组件：

**步骤1.** [为动态API调用创建具有`responseFields`模板的目标服务器](../../authoring-api/destination-server/create-destination-server.md#dynamic-dropdown-servers)，如下所示。

```json
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":" <--YOUR-API-ENDPOINT-PATH--> "
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

**步骤2.**&#x200B;使用`dynamicEnum`对象，如下所示。 在下面的示例中，使用动态服务器检索`User`下拉列表。


```json {line-numbers="true" highlight="13-21"}
"customerDataFields": [
  {
    "name": "integrationId",
    "title": "Integration ID",
    "type": "string",
    "isRequired": true
  },
  {
    "name": "userId",
    "title": "User",
    "type": "string",
    "isRequired": true,
    "dynamicEnum": {
      "queryParams": [
        "integrationId"
      ],
      "destinationServerId": "<~dynamic-field-server-id~>",
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "value": "$.list",
      "responseFormat": "NAME_VALUE"
    }
  }
]
```

将`destinationServerId`参数设置为您在步骤1中创建的目标服务器的ID。 您可以在[检索目标服务器配置](../../authoring-api/destination-server/retrieve-destination-server.md) API调用的响应中看到目标服务器ID。

## 创建嵌套式客户数据字段 {#nested-fields}

您可以为复杂的集成模式创建嵌套式客户数据字段。 这允许您为客户链接一系列选择。

例如，您可以添加嵌套的客户数据字段，以要求客户选择与您目标的集成类型，然后紧接着进行其他选择。 第二个选择是集成类型中的嵌套字段。

要添加嵌套字段，请使用`properties`参数，如下所示。 在下面的配置示例中，您可以在&#x200B;**您的目标 — 集成特定设置**&#x200B;客户数据字段中看到三个单独的嵌套字段。

>[!TIP]
>
>从2024年4月版本开始，您可以在嵌套字段中设置`isRequired`参数。 例如，在下面的配置代码片段中，前两个嵌套字段被标记为必填字段（高亮显示的第xxx行），客户无法继续操作，除非他们为该字段选择值。 详细了解[支持的参数](#supported-parameters)部分中的必填字段。

```json {line-numbers="true" highlight="11,20"}
    {
      "name": "yourdestination",
      "title": "Yourdestination - Integration Specific Settings",
      "type": "object",
      "properties": [
        {
          "name": "agreement",
          "title": "Advertiser data destination terms agreement. Enter I AGREE.",
          "type": "string",
          "isRequired": true,
          "pattern": "I AGREE",
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "account-name",
          "title": "Account name",
          "type": "string",
          "isRequired": true,
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "email",
          "title": "Email address",
          "type": "string",
          "isRequired": false,
          "pattern": "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$",
          "readOnly": false,
          "hidden": false
        }
      ],
      "isRequired": false,
      "readOnly": false,
      "hidden": false,
```

## 创建条件客户数据字段 {#conditional-options}

您可以创建条件客户数据字段，这些字段仅在用户选择特定选项时才会显示在激活工作流中。

例如，您可以创建条件文件格式选项，以使其仅在用户选择特定文件导出类型时显示。

以下配置将为CSV文件格式选项创建条件分组。 只有在用户选择CSV作为导出所需的文件类型时，才会显示CSV文件选项。

要将字段设置为条件字段，请使用`conditional`参数，如下所示：

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

在更广泛的上下文中，您可以看到以下目标配置中使用的`conditional`字段，以及在其中定义该字段的`fileType`字符串和`csvOptions`对象。 条件字段在`properties`参数中定义。

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

在下方，您可以根据上述配置查看生成的UI屏幕。 当用户选择文件类型CSV时，UI中会显示引用CSV文件类型的其他文件格式选项。

![显示CSV文件的条件文件格式选项的屏幕录制。](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## 访问模板化的客户数据字段 {#accessing-templatized-fields}

当目标需要用户输入时，您必须向用户提供一系列客户数据字段，用户可以通过Experience Platform UI填写这些字段。 然后，您必须配置目标服务器，以从客户数据字段中正确读取用户输入。 这可以通过模板化字段完成。

模板化字段使用格式`{{customerData.fieldName}}`，其中`fieldName`是从中读取信息的客户数据字段的名称。 所有模板化的客户数据字段前面都有`customerData.`，并包含在双大括号`{{ }}`中。

例如，我们来考虑以下Amazon S3目标配置：

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

此配置会提示您的用户在各自的客户数据字段中输入其[!DNL Amazon S3]存储段名称和文件夹路径。

为了使Experience Platform能够正确连接到[!DNL Amazon S3]，必须将目标服务器配置为从这两个客户数据字段中读取值，如下所示：

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

模板化的值`{{customerData.bucketName}}`和`{{customerData.path}}`读取用户提供的值，以便Experience Platform能够成功连接到目标平台。

有关如何配置目标服务器以读取模板化字段的更多信息，请参阅有关[硬编码字段与模板化字段](../destination-server/server-specs.md#templatized-fields)的文档。

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何允许用户在Experience Platform UI中通过客户数据字段输入信息。 您现在还知道如何为您的用例选择正确的客户数据字段，以及在Experience Platform UI中配置、排序和分组客户数据字段。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
