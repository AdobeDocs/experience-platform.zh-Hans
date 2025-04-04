---
title: Google Cloud Storage连接
description: 了解如何连接到Google Cloud Storage并激活受众或导出数据集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%

---

# [!DNL Google Cloud Storage]连接

## 概述 {#overview}

创建到[!DNL Google Cloud Storage]的实时出站连接，定期将数据文件从Adobe Experience Platform导出到您自己的存储桶中。

## 通过API或UI连接到您的[!DNL Google Cloud Storage]存储 {#connect-api-or-ui}

* 要使用Experience Platform用户界面连接到[!DNL Google Cloud Storage]存储位置，请阅读下面的[连接到目标](#connect)和[将受众激活到此目标](#activate)部分。
* 若要以编程方式连接到[!DNL Google Cloud Storage]存储位置，请阅读[使用流服务API教程](../../api/activate-segments-file-based-destinations.md)将受众激活到基于文件的目标。

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
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段，如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 如何使用Experience Platform用户界面](/help/destinations/ui/export-datasets.md)导出数据集[。
* 如何使用流服务API](/help/destinations/api/export-datasets.md)以编程方式[导出数据集。

## 导出数据的文件格式 {#file-format}

导出&#x200B;*受众数据*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.csv`、`parquet`或`.json`文件。 有关这些文件的更多信息，请参阅Audience Activation教程中的[导出的支持文件格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)部分。

导出&#x200B;*数据集*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.parquet`或`.json`文件。 有关这些文件的更多信息，请参阅导出数据集教程中的[验证成功的数据集导出](../../ui/export-datasets.md#verify)部分。

## 用于连接[!DNL Google Cloud Storage]帐户的必备设置 {#prerequisites}

为了将Experience Platform连接到[!DNL Google Cloud Storage]，您必须首先为您的[!DNL Google Cloud Storage]帐户启用互操作性。 要访问互操作性设置，请打开[!DNL Google Cloud Platform]并从导航面板的&#x200B;**[!UICONTROL 云存储]**&#x200B;选项中选择&#x200B;**[!UICONTROL 设置]**。

![突出显示了Cloud Storage和设置的Google Cloud Platform仪表板。](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

此时会显示&#x200B;**[!UICONTROL 设置]**&#x200B;页面。 在此处，您可以看到有关您的[!DNL Google]项目ID的信息以及有关您的[!DNL Google Cloud Storage]帐户的详细信息。 要访问互操作性设置，请从顶部标题中选择&#x200B;**[!UICONTROL 互操作性]**。

![ Google Cloud Platform仪表板中突出显示的“互操作性”选项卡。](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 互操作性]**&#x200B;页面包含有关身份验证、访问密钥以及与您的服务帐户关联的默认项目的信息。 要为您的服务帐户生成新的访问密钥ID和访问密钥，请选择&#x200B;**[!UICONTROL 为服务帐户创建密钥]**。

![Google Cloud Platform仪表板中突出显示的服务帐户控制的创建密钥。](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和访问密钥将[!DNL Google Cloud Storage]帐户连接到Experience Platform。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](/help/destinations/ui/connect-destination.md)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

* **[!UICONTROL 访问密钥ID]**：一个由61个字符组成的字母数字字符串，用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户。 有关如何获取此值的信息，请阅读上面的[先决条件](#prerequisites)部分。
* **[!UICONTROL 访问密钥]**：用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户的40字符base64编码字符串。 有关如何获取此值的信息，请阅读上面的[先决条件](#prerequisites)部分。
* **[!UICONTROL 加密密钥]**： （可选）您可以附加RSA格式的公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

有关这些值的更多信息，请阅读[Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成自己的访问密钥ID和访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL Bucket名称]**：输入要由此目标使用的[!DNL Google Cloud Storage]存储段的名称。
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

### 所需的[!DNL Google Cloud Storage]权限 {#required-google-cloud-storage-permission}

要成功连接数据并将其导出到您的[!DNL Google Cloud Storage]存储位置，您需要对存储桶拥有以下[!DNL Google Cloud Storage]权限：

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

详细了解[!DNL Google Cloud Storage]中的[访问控制和权限](https://cloud.google.com/storage/docs/access-control/iam-permissions)。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 计划中

在&#x200B;**[!UICONTROL 计划]**&#x200B;步骤中，您可以[为[!DNL Google Cloud Storage]目标设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)，还可以[配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 映射属性和身份 {#map}

在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，您可以为配置文件选择要导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看激活批处理目标UI教程中的[映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查您的[!DNL Google Cloud Storage]存储段并确保导出的文件包含预期的配置文件人口。

## IP地址允许列表 {#ip-address-allow-list}

如果您需要将Adobe 列入允许列表 IP添加到，请参阅[IP地址允许列表](ip-address-allow-list.md)一文。