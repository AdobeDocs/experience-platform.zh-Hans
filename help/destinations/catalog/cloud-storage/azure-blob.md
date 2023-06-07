---
title: Azure Blob连接
description: 创建到Azure Blob存储的实时出站连接，定期从Adobe Experience Platform导出CSV数据文件。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 8890fd137cfe6d35dcf6177b5516605e7753a75a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# [!DNL Azure Blob] 连接

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>通过测试版的导出数据集功能和改进的文件导出功能，您现在可能会看到两个 [!DNL Azure Blob] 目标目录中的信息卡。
>* 如果您已经将文件导出到 **[!UICONTROL Azure Blob]** 目标：请为新的数据集创建新的数据流 **[!UICONTROL Azure Blob测试版]** 目标。
>* 如果您尚未创建任何数据流到 **[!UICONTROL Azure Blob]** 目标，请使用新的 **[!UICONTROL Azure Blob测试版]** 用于导出文件的信息卡 **[!UICONTROL Azure Blob]**.


![并排视图中两个Azure Blob目标卡的图像。](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

新版中的改进 [!DNL Azure Blob] 目标卡包括：

* [数据集导出支持](/help/destinations/ui/export-datasets.md).
* 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 能够通过以下方式设置导出文件中的自定义文件标头： [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

[!DNL Azure Blob] (以下简称： [!DNL Blob])是Microsoft的云对象存储解决方案。 本教程提供了用于创建 [!DNL Blob] 目标使用 [!DNL Platform] 用户界面。

## 连接到您的 [!UICONTROL Azure Blob] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 连接到您的 [!UICONTROL Azure Blob] 存储位置使用Platform用户界面，请阅读部分 [连接到目标](#connect) 和 [将区段激活到此目标](#activate) 下面的。
* 连接到您的 [!UICONTROL Azure Blob] 存储位置以编程方式读取 [使用流服务API教程将区段激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Blob] 目标，您可以跳过本文档的其余部分，并继续阅读关于的教程 [将区段激活到目标](../../ui/activate-batch-profile-destinations.md).

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支持导出到的以下文件格式 [!DNL Azure Blob]：

* 逗号分隔值(CSV)：当前，对导出数据文件的支持仅限于逗号分隔值。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 连接字符串]**：需要连接字符串才能访问Blob存储中的数据。 此 [!DNL Blob] 连接字符串模式开头为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 有关配置的详细信息 [!DNL Blob] 连接字符串，请参见 [为Azure存储帐户配置连接字符串](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) 在Microsoft文档中。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 在下图中查看正确格式化的加密密钥示例。

   ![图像显示UI中格式正确的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 文件夹路径]**：输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 容器]**：输入 [!DNL Azure Blob Storage] 此目标使用的容器。
* **[!UICONTROL 文件类型]**：选择导出文件应使用的格式Experience Platform。 此选项仅适用于 **[!UICONTROL Azure Blob测试版]** 目标。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。 此选项仅适用于 **[!UICONTROL Azure Blob测试版]** 目标。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 此选项仅适用于 **[!UICONTROL Azure Blob测试版]** 目标。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出数据集](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 导出的数据 {#exported-data}

对象 [!DNL Azure Blob Storage] 目标， [!DNL Platform] 创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在区段激活教程中。