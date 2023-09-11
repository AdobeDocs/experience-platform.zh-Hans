---
title: Azure Blob连接
description: 创建到Azure Blob Storage的实时出站连接，定期从Adobe Experience Platform导出CSV数据文件。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 950370683f648771d91689e84c3d782824fb01f4
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 7%

---

# [!DNL Azure Blob] 连接

## 目标更改日志 {#changelog}

在2023年7月的Experience Platform版本中， [!DNL Azure Blob] 目标提供了新功能，如下所示：

* [!BADGE Beta]{type=Informative}[支持导出数据集](/help/destinations/ui/export-datasets.md)。
* 额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。
* 可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。
* [可自定义导出的 CSV 数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

## 概述 {#overview}

[!DNL Azure Blob] (以下简称： [!DNL Blob])是Microsoft的云对象存储解决方案。 本教程提供了用于创建 [!DNL Blob] 目标使用 [!DNL Platform] 用户界面。

## 连接到您的 [!UICONTROL Azure Blob] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 要连接到 [!UICONTROL Azure Blob] 存储位置使用Platform用户界面，请阅读以下章节 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下。
* 要连接到 [!UICONTROL Azure Blob] 存储位置以编程方式读取 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Blob] 目标，您可以跳过本文档的其余部分，并转到上的教程 [将受众激活到您的目标](../../ui/activate-batch-profile-destinations.md).

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

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支持以下要导出的文件格式 [!DNL Azure Blob]：

* 逗号分隔值(CSV)：对导出数据文件的支持当前仅限于逗号分隔值。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 向目标进行身份验证 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 连接字符串]**：访问Blob存储中的数据需要连接字符串。 此 [!DNL Blob] 连接字符串模式以下列内容开头： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 有关配置的详细信息 [!DNL Blob] 连接字符串，请参见 [为Azure存储帐户配置连接字符串](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) 请参阅Microsoft文档。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 文件夹路径]**：输入目标文件夹的路径，该文件夹将托管导出的文件。
* **[!UICONTROL 容器]**：输入 [!DNL Azure Blob Storage] 此目标要使用的容器。
* **[!UICONTROL 文件类型]**：选择导出的文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 查看 [示例清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 清单文件包含以下字段：
   * `flowRunId`：和 [数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 生成了导出的文件。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中存储导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（以字节为单位）。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

## (Beta)导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 导出的数据 {#exported-data}

对象 [!DNL Azure Blob Storage] 目标， [!DNL Platform] 创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在audience activation教程中。