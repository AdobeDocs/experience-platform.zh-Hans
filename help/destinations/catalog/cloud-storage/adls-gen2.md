---
title: Azure Data Lake Storage Gen2连接
description: 了解如何连接到Azure Data Lake Storage Gen2以激活受众和导出数据集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---

# [!DNL Azure Data Lake Storage Gen2] 连接

## 概述 {#overview}

请阅读此页面，了解如何创建到 [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])数据湖，定期从Experience Platform导出数据文件。

## 连接到您的 [!DNL ADLS Gen2] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 要连接到 [!DNL ADLS Gen2] 存储位置使用Platform用户界面，请阅读以下章节 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下。
* 要连接到 [!DNL ADLS Gen2] 存储位置以编程方式读取 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

此目标支持激活通过Experience Platform生成的所有受众 [分段服务](../../../segmentation/home.md).

*此外*&#x200B;中，此目标还支持激活下表中描述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段（例如，PPID），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](/help/destinations/ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL URL]**：的端点 [!DNL Azure Data Lake Storage Gen2]. 端点模式为： `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL 租户]**：包含您的应用程序的租户信息。
* **[!UICONTROL 服务主体Id]**：应用程序的客户端ID。
* **[!UICONTROL 服务主体密钥]**：应用程序的键。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 文件夹路径]**：输入目标文件夹的路径，该文件夹将托管导出的文件。
* **[!UICONTROL 文件类型]**：选择导出的文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 计划 {#scheduling}

在 **[!UICONTROL 正在计划]** 步骤，您可以 [设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 您的 [!DNL Azure Data Lake Storage Gen2] 目标位置，您还可以 [配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 映射属性和身份 {#map}

在 **[!UICONTROL 映射]** 步骤，您可以为配置文件选择要导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批次目标UI教程中。

## (Beta)导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Azure Data Lake Storage Gen2] 存储并确保导出的文件包含预期的配置文件人口。
