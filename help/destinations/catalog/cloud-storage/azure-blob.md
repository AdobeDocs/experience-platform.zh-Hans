---
keywords: Azure Blob;Blob目标；s3;Azure Blob目标
title: Azure Blob连接
description: 创建到Azure Blob Storage的实时出站连接，以定期从Adobe Experience Platform导出CSV数据文件。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# [!DNL Azure Blob] 连接

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>通过测试版的导出数据集功能和改进的文件导出功能，您现在可能会看到两个 [!DNL Azure Blob] 目标目录中的信息卡。
>* 如果您已经将文件导出到 **[!UICONTROL Azure Blob]** 目标：请为新数据流创建新数据流 **[!UICONTROL Azure Blob测试版]** 目标。
>* 如果您尚未为 **[!UICONTROL Azure Blob]** 目标，请使用新 **[!UICONTROL Azure Blob测试版]** 将文件导出到卡 **[!UICONTROL Azure Blob]**.


![并排视图中两个Azure Blob目标卡的图像。](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

改进了新 [!DNL Azure Blob] 目标卡包括：

* [数据集导出支持](/help/destinations/ui/export-datasets.md).
* 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 能够通过 [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

[!DNL Azure Blob] (以下简称 [!DNL Blob])是Microsoft的云对象存储解决方案。 本教程提供了创建 [!DNL Blob] 目标使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Blob] 目标位置，您可以跳过本文档的其余部分，并继续阅读上的教程 [将区段激活到您的目标](../../ui/activate-batch-profile-destinations.md).

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支持以下要导出到的文件格式 [!DNL Azure Blob]:

* 逗号分隔值(CSV):当前，对导出数据文件的支持仅限于以逗号分隔的值。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA公钥"
>abstract="或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 在下面的文档链接中查看格式正确的键值示例。"

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 连接字符串]**:访问Blob存储中的数据时需要使用连接字符串。 的 [!DNL Blob] 连接字符串模式以开头： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 有关配置 [!DNL Blob] 连接字符串，请参阅 [为Azure存储帐户配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) (在Microsoft文档中)。
* **[!UICONTROL 加密密钥]**:或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 查看下图中格式正确的加密密钥示例。

   ![显示UI中格式正确的PGP键示例的图像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 容器]**:输入 [!DNL Azure Blob Storage] 容器。
* **[!UICONTROL 文件类型]**:选择导出文件应使用的Experience Platform格式。 此选项仅适用于 **[!UICONTROL Azure Blob测试版]** 目标。 选择 [!UICONTROL CSV] 选项，您还 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**:选择Experience Platform应用于导出文件的压缩类型。 此选项仅适用于 **[!UICONTROL Azure Blob测试版]** 目标。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读 [导出数据集教程](/help/destinations/ui/export-datasets.md).

## 导出的数据 {#exported-data}

对于 [!DNL Azure Blob Storage] 目标， [!DNL Platform] 创建 `.csv` 文件。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。