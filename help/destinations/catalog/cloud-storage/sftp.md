---
title: SFTP连接
description: 创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 7%

---

# SFTP连接

## 目标更改日志 {#changelog}

在2023年7月发行的Experience Platform中，SFTP目标提供了新功能，如下所示：

* [支持导出数据集](/help/destinations/ui/export-datasets.md)。
* 额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。
* 可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

## 概述 {#overview}

创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。

>[!IMPORTANT]
>
> 虽然Experience Platform支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为[!DNL Amazon S3]和[!DNL Azure Blob]。

## 通过API或用户界面连接到SFTP {#connect-api-or-ui}

* 要使用Experience Platform用户界面连接到SFTP存储位置，请阅读下面的[连接到目标](#connect)和[将受众激活到此目标](#activate)部分。
* 要以编程方式连接到SFTP存储位置，请阅读[使用流服务API教程](../../api/activate-segments-file-based-destinations.md)将受众激活到基于文件的目标。

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
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

![目标目录中突出显示的基于配置文件的SFTP导出类型。](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 如何使用Experience Platform用户界面[导出数据集](/help/destinations/ui/export-datasets.md)。
* 如何使用流服务API[以编程方式](/help/destinations/api/export-datasets.md)导出数据集。

## 导出数据的文件格式 {#file-format}

导出&#x200B;*受众数据*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.csv`、`parquet`或`.json`文件。 有关这些文件的更多信息，请参阅Audience Activation教程中的[导出的支持文件格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)部分。

导出&#x200B;*数据集*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.parquet`或`.json`文件。 有关这些文件的更多信息，请参阅导出数据集教程中的[验证成功的数据集导出](../../ui/export-datasets.md#verify)部分。

## SFTP服务器连接要求 {#sftp-connection-requirements}

要确保成功导出数据，必须将目标SFTP服务器配置为允许有足够数量的并发连接。 如果SFTP服务器限制同时连接的数量，则可能会遇到导出作业失败的情况，尤其是同时导出多个受众或数据集时。

**推荐**
为获得最佳性能，SFTP服务器应为要导出的每个受众或数据集至少允许一个并发连接。 服务器至少应支持计划同时导出的受众或数据集总数的30%。

**示例**\
如果计划同时为100个受众或数据集导出，则SFTP服务器应允许至少30个并发连接。

正确配置SFTP服务器的连接限制有助于防止导出失败，并确保从Adobe Experience Platform可靠传送数据。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 身份验证信息 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="专用 SSH 密钥"
>abstract="私有 SSH 密钥的格式必须为 RSA 格式的 Base64 编码的字符串，并且不得受密码保护。"

如果选择&#x200B;**[!UICONTROL SFTP with password]**&#x200B;身份验证类型连接到SFTP位置：

![使用密码的SFTP目标基本身份验证。](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**： SFTP存储位置的地址；
* **[!UICONTROL Username]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL Port]**： SFTP存储位置使用的端口；
* **[!UICONTROL Password]**：用于登录到SFTP存储位置的密码。
* **[!UICONTROL Encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


如果选择&#x200B;**[!UICONTROL SFTP with SSH key]**&#x200B;身份验证类型连接到SFTP位置：

![SFTP目标SSH密钥身份验证。](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**：填写SFTP帐户的IP地址或域名
* **[!UICONTROL Port]**： SFTP存储位置使用的端口；
* **[!UICONTROL Username]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL SSH Key]**：用于登录到SFTP存储位置的私有SSH密钥。 私钥必须是RSA格式的Base64编码字符串，且不得受密码保护。
* **[!UICONTROL Encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目标详细信息 {#destination-details}

在建立与SFTP位置的身份验证连接后，提供目标的以下信息：

![SFTP目标的目标详细信息字段。](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**：输入一个名称，帮助您在Experience Platform用户界面中识别此目标；
* **[!UICONTROL Description]**：输入此目标的描述；
* **[!UICONTROL Folder path]**：在要导出文件的SFTP位置中输入文件夹的路径。
* **[!UICONTROL File type]**：选择Experience Platform应用于导出文件的格式。 在选择[!UICONTROL CSV]选项时，您还可以[配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL Compression format]**：选择Experience Platform应该用于导出文件的压缩类型。
* **[!UICONTROL Include manifest file]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为`manifest-<<destinationId>>-<<dataflowRunId>>.json`。 查看[样本清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)。 清单文件包含以下字段：
   * `flowRunId`：生成导出文件的[数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中保存导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（字节）。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查您的SFTP存储，并确保导出的文件包含预期的配置文件人口。

## IP地址允许列表 {#ip-address-allow-list}

如果您需要将Adobe 列入允许列表 IP添加到，请参阅[IP地址允许列表](ip-address-allow-list.md)一文。
