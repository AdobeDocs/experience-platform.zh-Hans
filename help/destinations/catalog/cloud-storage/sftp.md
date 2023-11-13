---
title: SFTP连接
description: 创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 11%

---

# SFTP连接

## 目标更改日志 {#changelog}

在2023年7月发行的Experience Platform中，SFTP目标提供了新功能，如下所示：

* [支持导出数据集](/help/destinations/ui/export-datasets.md)。
* 额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。
* 可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。
* [可自定义导出的 CSV 数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

## 概述 {#overview}

创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。

>[!IMPORTANT]
>
> 虽然Experience Platform支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 通过API或用户界面连接到SFTP {#connect-api-or-ui}

* 要使用Platform用户界面连接到SFTP存储位置，请阅读以下部分 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下。
* 要以编程方式连接到SFTP存储位置，请阅读 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![基于配置文件的SFTP导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 身份验证信息 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="私有 SSH 密钥"
>abstract="私有 SSH 密钥的格式必须为 RSA 格式的 Base64 编码的字符串，并且不得受密码保护。"

如果您选择 **[!UICONTROL 包含密码的SFTP]** 用于连接到SFTP位置的身份验证类型：

![SFTP目标基本身份验证](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 域]**：SFTP存储位置的地址；
* **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL 端口]**：您的SFTP存储位置使用的端口；
* **[!UICONTROL 密码]**：用于登录到SFTP存储位置的密码。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


如果您选择 **[!UICONTROL 包含SSH密钥的SFTP]** 用于连接到SFTP位置的身份验证类型：

![SFTP目标SSH密钥身份验证](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 域]**：填写SFTP帐户的IP地址或域名
* **[!UICONTROL 端口]**：您的SFTP存储位置使用的端口；
* **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL SSH密钥]**：用于登录到SFTP存储位置的私有SSH密钥。 私有 密钥的格式必须为 RSA 格式的 Base64 编码的字符串，并且不得受密码保护。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目标详细信息 {#destination-details}

在建立与SFTP位置的身份验证连接后，提供目标的以下信息：

![SFTP目标的可用目标详细信息](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名称]**：输入有助于您在Experience Platform用户界面中识别此目标的名称；
* **[!UICONTROL 描述]**：输入此目标的描述；
* **[!UICONTROL 文件夹路径]**：输入要导出文件的SFTP位置中的文件夹路径。
* **[!UICONTROL 文件类型]**：选择导出的文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 查看 [示例清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 清单文件包含以下字段：
   * `flowRunId`：和 [数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 生成了导出的文件。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中存储导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（以字节为单位）。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 导出的数据 {#exported-data}

对象 [!DNL SFTP] 目标，平台创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在audience activation教程中。

## IP地址允许列表 {#ip-address-allow-list}

请参阅 [SFTP目标的IP地址允许列表](ip-address-allow-list.md) (如果需要将AdobeIP添加到允许列表)。
