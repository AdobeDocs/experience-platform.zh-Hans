---
title: （测试版）Azure数据湖存储第2代连接
description: 了解如何连接到Azure Data Lake Storage Gen2以激活区段和导出数据集。
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# （测试版） [!DNL Azure Data Lake Storage Gen2] 连接

>[!IMPORTANT]
>
>此目标当前为测试版，仅适用于数量有限的客户。 请求对 [!DNL Azure Data Lake Storage Gen2] 连接时，请联系您的Adobe代表并提供 [!DNL Organization ID].

## 概述 {#overview}

阅读本页以了解如何创建与 [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])数据湖，以定期从Experience Platform导出数据文件。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您正在导出区段的所有成员，以及在的 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](/help/destinations/ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL URL]**:的端点 [!DNL Azure Data Lake Storage Gen2]. 端点模式为： `https://<accountname>.dfs.core.windows.net`.
* **[!UICONTROL 租户]**:包含您的应用程序的租户信息。
* **[!UICONTROL 服务主体ID]**:应用程序的客户端ID。
* **[!UICONTROL 服务主密钥]**:应用程序的密钥。
* **[!UICONTROL 加密密钥]**:或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64-encoded] 字符串。 在下面的文档链接中查看格式正确且基本64编码的键值的示例。 为简便起见，缩短了中间部分。

   ![该图像显示了UI中格式正确且基本64加密的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 计划 {#scheduling}

在 **[!UICONTROL 计划]** 步骤 [设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) , [!DNL Azure Data Lake Storage Gen2] 目标，您还 [配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 映射属性和标识 {#map}

在 **[!UICONTROL 映射]** 步骤中，您可以选择要为配置文件导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为任何您希望的友好名称。 有关更多信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) （在激活批处理目标UI教程中）。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读 [导出数据集教程](/help/destinations/ui/export-datasets.md).

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Azure Data Lake Storage Gen2] 并确保导出的文件包含预期的用户档案群体。