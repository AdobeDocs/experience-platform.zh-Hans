---
title: 使用流服务API将数据登陆区连接到Adobe Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到数据登陆区。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 3%

---

# 使用流服务API将[!DNL Data Landing Zone]连接到Adobe Experience Platform

>[!IMPORTANT]
>
>此页面特定于Experience Platform中的[!DNL Data Landing Zone] *源*&#x200B;连接器。 有关连接到[!DNL Data Landing Zone] *目标*&#x200B;连接器的信息，请参阅[[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone]是一种安全的基于云的文件存储工具，可将文件导入Adobe Experience Platform。 数据会在七天后自动从[!DNL Data Landing Zone]中删除。

本教程将指导您完成有关如何使用[!DNL Data Landing Zone]API[[!DNL Flow Service] 创建](https://www.adobe.io/experience-platform-apis/references/flow-service/)源连接的步骤。 本教程还提供了有关如何检索[!DNL Data Landing Zone]以及查看和刷新凭据的说明。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

本教程还要求您阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南，了解如何对Experience Platform API进行身份验证并解释文档中提供的示例调用。

以下部分提供使用[!DNL Data Landing Zone] API成功创建[!DNL Flow Service]源连接所需了解的其他信息。

## 检索可用的登陆区域

>[!IMPORTANT]
>
>您必须具有&#x200B;**[!UICONTROL Manage Sources]**&#x200B;访问控制权限才能使用[!DNL Data Landing Zone] API并检索`type=user_drop_zone`。 有关详细信息，请阅读[访问控制概述](../../../../../access-control/home.md)或联系您的产品管理员以获取所需的权限。

使用API访问[!DNL Data Landing Zone]的第一步是向`/landingzone` API的[!DNL Connectors]端点发出GET请求，同时将`type=user_drop_zone`作为请求标头的一部分提供。

**API格式**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`类型允许API将登陆区域容器与您可用的其他类型容器区分开来。 |

**请求**

以下请求将检索现有的登陆区域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**响应**

根据您的提供商，成功的请求会返回以下内容：

>[!BEGINTABS]

>在Azure上[!TAB 响应]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您检索到的登陆区域的名称。 |
| `containerTTL` | 适用于登陆区域内数据的过期时间（以天为单位）。 七天后，会删除给定登陆区域内的任何区域。 |


>在AWS上[!TAB 响应]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## 检索[!DNL Data Landing Zone]凭据

要检索[!DNL Data Landing Zone]的凭据，请向`/credentials` API的[!DNL Connectors]端点发出GET请求。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**请求**

以下请求示例检索现有登陆区域的凭据。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

根据您的提供商，成功的请求会返回以下内容：

>[!BEGINTABS]

>在Azure上[!TAB 响应]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | [!DNL Data Landing Zone]的名称。 |
| `SASToken` | [!DNL Data Landing Zone]的共享访问签名令牌。 此字符串包含授权请求所需的所有信息。 |
| `storageAccountName` | 存储帐户的名称。 |
| `SASUri` | [!DNL Data Landing Zone]的共享访问签名URI。 此字符串是您正在接受身份验证的[!DNL Data Landing Zone]的URI及其对应的SAS令牌的组合。 |
| `expiryDate` | SAS令牌的过期日期。 您必须在到期日期之前刷新您的令牌，以便继续在您的应用程序中使用它来将数据上载到[!DNL Data Landing Zone]。 如果您没有在规定的到期日之前手动刷新令牌，则会在执行GET凭据调用时自动刷新并提供新令牌。 |

>在AWS上[!TAB 响应]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| 属性 | 描述 |
| --- | --- |
| `credentials.clientId` | 在AWS中[!DNL Data Landing Zone]的客户端ID。 |
| `credentials.awsAccessKeyId` | 在AWS中[!DNL Data Landing Zone]的访问密钥ID。 |
| `credentials.awsSecretAccessKey` | 您的[!DNL Data Landing Zone]在AWS中的访问密钥。 |
| `credentials.awsSessionToken` | AWS会话令牌。 |
| `dlzPath.bucketName` | AWS存储段的名称。 |
| `dlzPath.dlzFolder` | 您正在访问的[!DNL Data Landing Zone]文件夹。 |
| `dlzProvider` | 您正在使用的[!DNL Data Landing Zone]提供程序。 对于Amazon，此值为[!DNL Amazon S3]。 |
| `expiryTime` | 到期时间（以unix时间为单位）。 |

>[!ENDTABS]

### 使用API检索必填字段

生成令牌后，您可以使用以下请求示例以编程方式检索必填字段：

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## 更新[!DNL Data Landing Zone]凭据

您可以通过向`SASToken` API的`/credentials`端点发出POST请求来更新[!DNL Connectors]。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | `user_drop_zone`类型允许API将登陆区域容器与您可用的其他类型容器区分开来。 |
| `refresh` | `refresh`操作允许您重置登陆区域凭据并自动生成新的`SASToken`。 |

**请求**

以下请求将更新您的登陆区域凭据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应返回您的`SASToken`和`SASUri`的更新值。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## 探索登陆区域文件结构和内容

您可以通过向`connectionSpecs` API的[!DNL Flow Service]端点发出GET请求来探索登陆区域的文件结构和内容。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 对应于[!DNL Data Landing Zone]的连接规范ID。 此固定ID为： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回在查询的目录中找到的文件和文件夹数组。 请记下要上传的文件的`path`属性，因为您需要在下一步中提供该属性以检查其结构。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 预览登陆区域文件结构和内容

要在登陆区域中检查文件的结构，请在提供文件的路径和类型作为查询参数的同时执行GET请求。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 对应于[!DNL Data Landing Zone]的连接规范ID。 此固定ID为： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |  |
| `{OBJECT_TYPE}` | 要访问的对象的类型。 | `file` |
| `{OBJECT}` | 要访问的对象的路径和名称。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 文件的类型。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 一个布尔值，定义是否支持文件预览。 | </ul><li>`true`</li><li>`false`</li></ul> |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回查询文件的结构，包括文件名和数据类型。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### 使用`determineProperties`自动检测[!DNL Data Landing Zone]的文件属性信息

在进行GET调用以浏览源的内容和结构时，可以使用`determineProperties`参数自动检测[!DNL Data Landing Zone]文件内容的属性信息。

#### `determineProperties`用例

下表概述了在使用`determineProperties`查询参数或手动提供文件信息时可能会遇到的不同情况。

| `determineProperties` | `queryParams` | 响应 |
| --- | --- | --- |
| True | 不适用 | 如果将`determineProperties`作为查询参数提供，则进行文件属性检测，响应将返回新的`properties`键，该键包括关于文件类型、压缩类型和列分隔符的信息。 |
| 不适用 | True | 如果文件类型、压缩类型和列分隔符的值作为`queryParams`的一部分手动提供，则它们将用于生成架构，并且相同的属性作为响应的一部分返回。 |
| True | True | 如果同时执行这两个选项，则会返回错误。 |
| 不适用 | 不适用 | 如果两个选项均未提供，则会返回错误，因为无法获取响应的属性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `determineProperties` | 此查询参数允许[!DNL Flow Service] API检测有关文件属性的信息，包括有关文件类型、压缩类型和列分隔符的信息。 | `true` |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回查询文件的结构，包括文件名和数据类型，以及包含有关`properties`、`fileType`和`compressionType`信息的`columnDelimiter`键。

+++单击我

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 属性 | 描述 |
| --- | --- |
| `properties.fileType` | 查询文件的相应文件类型。 支持的文件类型为： `delimited`、`json`和`parquet`。 |
| `properties.compressionType` | 用于查询文件的相应压缩类型。 支持的压缩类型包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用于查询文件的相应列分隔符。 任何单个字符值都是允许的列分隔符。 默认值为逗号`(,)`。 |


## 创建源连接

源连接创建和管理与摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和组织。

要创建源连接，请向`/sourceConnections` API的[!DNL Flow Service]端点发出POST请求。


**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | [!DNL Data Landing Zone]源连接的名称。 |
| `data.format` | 要带入Experience Platform的数据的格式。 |
| `params.path` | 要带到Experience Platform的文件的路径。 |
| `connectionSpec.id` | 对应于[!DNL Data Landing Zone]的连接规范ID。 此固定ID为： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 在下一个教程中，创建数据流时需要此ID。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 后续步骤

通过完成本教程，您已检索到[!DNL Data Landing Zone]凭据，探索了其文件结构以查找要带到Experience Platform的文件，并创建了源连接以开始将您的数据带到Experience Platform。 您现在可以继续下一教程，其中您将了解如何使用[API [!DNL Flow Service] 创建数据流以将云存储数据引入Experience Platform。](../../collect/cloud-storage.md)
