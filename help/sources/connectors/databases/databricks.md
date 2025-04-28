---
title: Azure数据库
description: 了解将Azure数据库连接到Experience Platform所需的先决步骤。
last-substantial-update: 2023-04-29T00:00:00Z
source-git-commit: 28de691c578998b21e67b5b08522988b3edc3424
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# [!DNL Azure Databricks]

[!DNL Azure Databricks]是一个基于云的平台，专为数据分析、机器学习和AI而设计。 您可以使用[!DNL Databricks]与[!DNL Azure]集成，并提供用于大规模构建、部署和管理数据解决方案的整体环境。

您可以使用[!DNL Databricks]源连接帐户并将[!DNL Databricks]数据摄取到Adobe Experience Platform。

## 先决条件

完成先决条件步骤以成功将您的[!DNL Databricks]帐户连接到Experience Platform。

### 检索容器凭据

检索您的Experience Platform [!DNL Azure Blob Storage]凭据，以使您的[!DNL Databricks]帐户以后能够访问它。

要检索您的凭据，请向[!DNL Connectors] API的`/credentials`端点发出GET请求。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**请求**

以下请求检索Experience Platform [!DNL Azure Blob Storage]的凭据。

+++查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应提供了您的凭据(`containerName`、`SASToken`、`storageAccountName`)，供以后在[!DNL Databricks]的[!DNL Apache Spark]配置中使用。

+++查看响应示例

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | [!DNL Azure Blob Storage]容器的名称。 稍后在完成[!DNL Databricks]的[!DNL Apache Spark]配置时将使用此值。 |
| `SASToken` | [!DNL Azure Blob Storage]的共享访问签名令牌。 此字符串包含授权请求所需的所有信息。 |
| `storageAccountName` | 存储帐户的名称。 |
| `SASUri` | [!DNL Azure Blob Storage]的共享访问签名URI。 此字符串是您正在接受身份验证的[!DNL Azure Blob Storage]的URI及其对应的SAS令牌的组合。 |
| `expiryDate` | SAS令牌的过期日期。 您必须在到期日期之前刷新您的令牌，以便继续在您的应用程序中使用它来将数据上载到[!DNL Azure Blob Storage]。 如果您没有在规定的到期日之前手动刷新令牌，则会在执行GET凭据调用时自动刷新并提供新令牌。 |

+++

### 刷新您的凭据

>[!NOTE]
>
>您刷新凭据后，现有凭据将被撤销。 因此，每次刷新存储凭据时，都必须相应地更新[!DNL Spark]配置。 否则，您的数据流将失败。

要刷新凭据，请发出POST请求并包含`action=refresh`作为查询参数。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**请求**

以下请求刷新您[!DNL Azure Blob Storage]的凭据。

+++查看请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

成功的响应将返回您的新凭据。

+++查看响应示例

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### 配置对您的[!DNL Azure Blob Storage]的访问权限

>[!IMPORTANT]
>
>* 如果群集已终止，服务将在流运行期间自动重新启动群集。 但是，在创建连接或数据流时，必须确保群集处于活动状态。 此外，如果您正在执行数据预览或探索等操作，则群集必须处于活动状态，因为这些操作无法提示自动重新启动已终止的群集。
>
>* 您的[!DNL Azure]容器包含一个名为`adobe-managed-staging`的文件夹。 为确保数据的无缝摄取，**不要**&#x200B;修改此文件夹。


接下来，必须确保您的[!DNL Databricks]群集具有访问Experience Platform [!DNL Azure Blob Storage]帐户的权限。 在执行此操作时，您可以使用[!DNL Azure Blob Storage]作为写入[!DNL delta lake]表数据的临时位置。

要提供访问权限，您必须在[!DNL Databricks]群集上将SAS令牌配置为[!DNL Apache Spark]配置的一部分。

在[!DNL Databricks]界面中，选择&#x200B;**[!DNL Advanced options]**，然后在[!DNL Spark config]输入框中输入以下内容。

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| 属性 | 描述 |
| --- | --- |
| 容器名称 | 容器的名称。 您可以通过检索[!DNL Azure Blob Storage]凭据获取此值。 |
| 存储帐户 | 存储帐户的名称。 您可以通过检索[!DNL Azure Blob Storage]凭据获取此值。 |
| SAS 令牌 | [!DNL Azure Blob Storage]的共享访问签名令牌。 您可以通过检索[!DNL Azure Blob Storage]凭据获取此值。 |

![Azure上的数据库UI。](../../images/tutorials/create/databricks/databricks-ui.png)

## 使用API将[!DNL Databricks]连接到Experience Platform

现在您已完成先决条件步骤，接下来可以继续阅读有关使用API [将您的 [!DNL Databricks] 帐户连接到Experience Platform](../../tutorials/api/create/databases/databricks.md)的指南。