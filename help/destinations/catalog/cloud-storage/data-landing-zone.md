---
title: 数据登陆区目标
description: 了解如何连接到数据登陆区以激活受众和导出数据集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 4eef1804d6974fd54f5e74e0efe62257190f408b
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 2%

---

# 数据登陆区目标

>[!IMPORTANT]
>
>此文档页面参考[!DNL Data Landing Zone] *目标*。 源目录中还有[!DNL Data Landing Zone] *源*。 有关详细信息，请阅读[[!DNL Data Landing Zone] 源](/help/sources/connectors/cloud-storage/data-landing-zone.md)文档。


## 概述 {#overview}

[!DNL Data Landing Zone]是由Adobe Experience Platform设置的云存储界面，它授予您一个安全、基于云的文件存储工具的访问权限，以便将文件导出到Experience Platform中。 您有权访问每个沙盒一个[!DNL Data Landing Zone]容器，所有容器的总数据量以您的Experience Platform产品和服务许可证提供的总数据为限。 Experience Platform及其应用程序（如[!DNL Customer Journey Analytics]、[!DNL Journey Orchestration]、[!DNL Intelligent Services]和[!DNL Real-Time Customer Data Platform]）的所有客户都为每个沙盒配置一个[!DNL Data Landing Zone]容器。

Experience Platform对上传到[!DNL Data Landing Zone]容器的所有文件强制实施严格的七天生存时间(TTL)。 所有文件都会在七天后删除。

使用Azure或Amazon Web服务云支持的客户可以使用[!DNL Data Landing Zone]目标连接器。 由于配置了目标的云不同，身份验证机制也不同，有关目标及其用例的所有其他内容都相同。 有关[对Azure Blob中配置的数据登陆区域进行身份验证](#authenticate-dlz-azure)和[对AWS配置的数据登陆区域进行身份验证](#authenticate-dlz-aws)部分中提供的两个不同身份验证机制的更多信息。

![图表显示了基于云支持的数据登陆区目标实施有何不同。](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png "由云支持提供的Data Landing Zone目标实现"){zoomable="yes"}

## 通过API或UI连接到您的[!UICONTROL 数据登陆区]存储 {#connect-api-or-ui}

* 要使用Experience Platform用户界面连接到您的[!UICONTROL 数据登陆区域]存储位置，请阅读下面的[连接到目标](#connect)和[将受众激活到此目标](#activate)部分。
* 若要以编程方式连接到[!UICONTROL 数据登陆区域]存储位置，请阅读[使用流服务API教程](../../api/activate-segments-file-based-destinations.md)将受众激活到基于文件的目标。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段（例如，PPID），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 如何使用Experience Platform用户界面[导出数据集](/help/destinations/ui/export-datasets.md)。
* 如何使用流服务API[以编程方式](/help/destinations/api/export-datasets.md)导出数据集。

## 导出数据的文件格式 {#file-format}

导出&#x200B;*受众数据*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.csv`、`parquet`或`.json`文件。 有关这些文件的更多信息，请参阅Audience Activation教程中的[导出的支持文件格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)部分。

导出&#x200B;*数据集*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.parquet`或`.json`文件。 有关这些文件的更多信息，请参阅导出数据集教程中的[验证成功的数据集导出](../../ui/export-datasets.md#verify)部分。

## 对Azure Blob中配置的数据登陆区进行身份验证 {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>本节适用于在Microsoft Azure上运行的Experience Platform的实施。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。

您可以通过[!DNL Azure Storage Explorer]或命令行界面将文件读取和写入容器。

[!DNL Data Landing Zone]支持基于SAS的身份验证，其数据受标准[!DNL Azure Blob]存储安全机制的静态和传输保护。 SAS代表[共享访问签名](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers)。

要通过公共Internet连接保护您的数据，请使用基于SAS的身份验证来安全地访问您的[!DNL Data Landing Zone]容器。 访问[!DNL Data Landing Zone]容器不需要更改网络，这意味着您不需要为网络配置任何允许列表或跨区域设置。

### 将您的[!DNL Data Landing Zone]容器连接到[!DNL Azure Storage Explorer]

您可以使用[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/)管理[!DNL Data Landing Zone]容器的内容。 若要开始使用[!DNL Data Landing Zone]，您必须首先检索凭据，在[!DNL Azure Storage Explorer]中输入凭据，然后将[!DNL Data Landing Zone]容器连接到[!DNL Azure Storage Explorer]。

在[!DNL Azure Storage Explorer] UI中，选择左侧导航栏中的连接图标。 出现&#x200B;**选择资源**&#x200B;窗口，为您提供连接选项。 选择&#x200B;**[!DNL Blob container]**&#x200B;以连接到[!DNL Data Landing Zone]存储。

![选择Azure UI中突出显示的资源。](/help/sources/images/tutorials/create/dlz/select-resource.png)

接下来，选择&#x200B;**共享访问签名URL (SAS)**&#x200B;作为连接方法，然后选择&#x200B;**下一步**。

![选择在Azure UI中高亮显示的连接方法。](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供与&#x200B;**容器对应的**&#x200B;显示名称&#x200B;**[!DNL Blob]和**&#x200B;容器SAS URL[!DNL Data Landing Zone]。

>[!BEGINSHADEBOX]

### 检索[!DNL Data Landing Zone]的凭据 {#retrieve-dlz-credentials}

您必须使用Experience Platform API检索您的[!DNL Data Landing Zone]凭据。 用于检索凭据的API调用描述如下。 有关获取标头所需值的信息，请参阅[Adobe Experience Platform API快速入门](/help/landing/api-guide.md)指南。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 查询参数 | 描述 |
| --- | --- |
| `dlz_destination` | `dlz_destination`类型允许API将登陆区域目标容器与您可用的其他类型容器区分开来。 |

{style="table-layout:auto"}

**请求**

以下请求示例检索现有登陆区域的凭据。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应返回登陆区域的凭据信息，包括当前的`SASToken`和`SASUri`以及与登陆区域容器对应的`storageAccountName`。

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您的登陆区域的名称。 |
| `SASToken` | 登陆区域的共享访问签名令牌。 此字符串包含授权请求所需的所有信息。 |
| `SASUri` | 登陆区域的共享访问签名URI。 此字符串是您要进行身份验证的登陆区域的URI及其对应的SAS令牌的组合， |

{style="table-layout:auto"}

### 更新[!DNL Data Landing Zone]凭据 {#update-dlz-credentials}

您还可以在需要时刷新凭据。 您可以通过向`SASToken` API的`/credentials`端点发出POST请求来更新[!DNL Connectors]。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 查询参数 | 描述 |
| --- | --- |
| `dlz_destination` | `dlz_destination`类型允许API将登陆区域目标容器与您可用的其他类型容器区分开来。 |
| `refresh` | `refresh`操作允许您重置登陆区域凭据并自动生成新的`SASToken`。 |

{style="table-layout:auto"}

**请求**

以下请求将更新您的登陆区域凭据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
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
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

提供显示名称(`containerName`)和[!DNL Data Landing Zone] SAS URL（如上述API调用中所返回），然后选择&#x200B;**下一步**。

![输入在Azure UI中突出显示的连接信息。](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

此时将显示&#x200B;**摘要**&#x200B;窗口，其中提供了设置的概述，包括有关[!DNL Blob]端点和权限的信息。 准备就绪后，选择&#x200B;**连接**。

![Azure UI中显示的设置摘要。](/help/sources/images/tutorials/create/dlz/summary.png)

成功连接将更新包含[!DNL Azure Storage Explorer]容器的[!DNL Data Landing Zone]用户界面。

![Azure UI中突出显示的DLZ用户容器摘要。](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

在将[!DNL Data Landing Zone]容器连接到[!DNL Azure Storage Explorer]后，您现在可以开始将文件从Experience Platform导出到[!DNL Data Landing Zone]容器。 要导出文件，必须在Experience Platform UI中建立与[!DNL Data Landing Zone]目标的连接，如以下部分所述。

## 对AWS设置的数据登陆区进行身份验证 {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。

执行以下操作以获取在AWS上配置的[!DNL Data Landing Zone]实例的凭据。 然后，使用选择的客户端连接到[!DNL Data Landing Zone]实例。

>[!BEGINSHADEBOX]

### 检索[!DNL Data Landing Zone]的凭据 {#retrieve-dlz-credentials-aws}

您必须使用Experience Platform API检索您的[!DNL Data Landing Zone]凭据。 用于检索凭据的API调用描述如下。 有关获取标头所需值的信息，请参阅[Adobe Experience Platform API快速入门](/help/landing/api-guide.md)指南。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| 查询参数 | 描述 |
| --- | --- |
| `dlz_destination` | 添加`dlz_destination`查询参数以指定您希望检索[!DNL Data Landing Zone] *目标*&#x200B;类型的容器凭据。 要连接和检索数据登陆区域&#x200B;*源*&#x200B;的凭据，请查看[源文档](/help/sources/connectors/cloud-storage/data-landing-zone.md)。 |

{style="table-layout:auto"}

**请求**

以下请求示例检索现有登陆区域的凭据。

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**响应**

以下响应返回登陆区域的凭据信息，包括当前的`awsAccessKeyId`、`awsSecretAccessKey`和其他信息。

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| 属性 | 描述 |
| --- | --- |
| `credentials` | 此对象包括Experience Platform用来将文件导出到已设置数据登录区位置的`awsAccessKeyId`、`awsSecretAccessKey`和`awsSessionToken`。 |
| `dlzPath` | 此对象包括在Adobe设置的AWS位置中存储导出文件的路径。 |
| `dlzProvider` | 指示这是由Amazon S3配置的数据登陆区。 |
| `expiryTime` | 指示`credentials`对象中的凭据何时到期。 要刷新凭据，请再次执行请求。 |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

确保已按照[!DNL Data Landing Zone]先决条件[!DNL Azure Storage Explorer]部分中的说明将您的[容器连接到](#prerequisites)。 由于[!DNL Data Landing Zone]是Adobe配置的存储，您无需在Experience Platform UI中执行任何进一步步骤即可向目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 加密密钥]**： （可选）您可以附加RSA格式的公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。
  ![显示UI中格式正确的PGP密钥示例的图像。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)
* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 文件夹路径]**：输入将承载导出文件的目标文件夹的路径。
* **[!UICONTROL 文件类型]**：选择Experience Platform应用于导出文件的格式。 在选择[!UICONTROL CSV]选项时，您还可以[配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为`manifest-<<destinationId>>-<<dataflowRunId>>.json`。 查看[样本清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)。 清单文件包含以下字段：
   * `flowRunId`：生成导出文件的[数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中保存导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（字节）。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 日程计划

在&#x200B;**[!UICONTROL 计划]**&#x200B;步骤中，您可以[为](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)目标设置导出计划[!DNL Data Landing Zone]，还可以[配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 映射属性和身份 {#map}

在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，您可以为配置文件选择要导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看激活批处理目标UI教程中的[映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 验证数据导出是否成功 {#exported-data}

要验证是否已成功导出数据，请检查您的[!DNL Data Landing Zone]存储并确保导出的文件包含预期的配置文件人口。
