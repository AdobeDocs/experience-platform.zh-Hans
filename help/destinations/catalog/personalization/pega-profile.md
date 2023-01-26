---
title: Pega配置文件连接器
description: 在Adobe Experience Platform中使用适用于Amazon S3的Pega Profile Connector将完整或增量配置文件数据导出到Amazon S3云存储，或将两者都导出。 在Pega客户决策中心，可以在客户配置文件设计器中计划数据作业，以定期从Amazon S3存储导入配置文件数据。
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Pega配置文件连接器

## 概述 {#overview}

使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中创建与 [!DNL Amazon Web Services] (AWS)S3存储，用于将配置文件数据定期从Adobe Experience Platform导出到CSV文件，并将其导出到您自己的S3存储段中。 在 [!DNL Pega Customer Decision Hub]，则可以计划数据作业以从S3存储导入此配置文件数据，以更新 [!DNL Pega Customer Decision Hub] 配置文件。

此连接器有助于设置配置文件数据的初始导出，还有助于定期将新配置文件同步到 [!DNL Pega Customer Decision Hub].  在客户决策中心拥有最新数据，可为下一最佳行动决策提供更好、更新的客户群视图。

>[!IMPORTANT]
>
>此文档页面由Pegassystems创建。 如有任何查询或更新请求，请直接联系Pega [此处](mailto:support@pega.com).

## 用例

为了帮助您更好地了解应如何以及何时应使用 [!DNL Pega Profile Connector] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例1

营销人员希望最初设置 [!DNL Pega Customer Decision Hub] 从Adobe Experience Platform加载的用户档案数据。 这是初始的完整负载，然后是按计划进行增量加载。

### 用例2

营销人员希望Adobe Experience Platform中提供最新的用户档案数据，该数据位于 [!DNL Pega Customer Decision Hub] 可持续增强对客户用户档案的Pega分析。

## 先决条件 {#prerequisites}

在您使用此目标将数据导出到Adobe Experience Platform并将用户档案导入之前， [!DNL Pega Customer Decision Hub]，请确保完成以下先决条件：

* 配置 [!DNL Amazon S3] 存储段和用于导出和导入数据文件的文件夹路径。
* 配置 [!DNL Amazon S3] 访问密钥和 [!DNL Amazon S3] 密钥：在 [!DNL Amazon S3]，生成 `access key - secret access key` 对，以授予对 [!DNL Amazon S3] 帐户。
* 要成功将数据连接并导出到 [!DNL Amazon S3] 存储位置，为创建Identity and Access Management(IAM)用户 [!DNL Platform] in [!DNL Amazon S3] 和分配权限，例如 `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* 确保 [!DNL Pega Customer Decision Hub] 实例已升级到8.8或更高版本。

## 支持的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支持激活下表所述的自定义用户ID。 有关更多详细信息，请参阅 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 |
|---|---|
| *客户ID* | 唯一标识中用户档案的通用用户标识符 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**:在 [!DNL Amazon S3]，生成 `access key - secret access key` 对授予Adobe Experience Platform访问 [!DNL Amazon S3] 帐户。 在 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 填写目标详细信息 {#destination-details}

在与建立身份验证连接后 [!DNL Amazon S3]，请提供目标的以下信息：

![UI屏幕的图像，显示Pega配置文件连接器目标详细信息的已完成字段](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**. UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 存储段名称]**:输入 [!DNL Amazon S3] 存储段供此目标使用。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 压缩类型]**:选择压缩类型为GZIP或“无”。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的区段文件在Amazon S3存储中创建自定义文件夹。 读取 [使用宏在存储位置中创建文件夹](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 中。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和标识 {#map}

在 **[!UICONTROL 映射]** 步骤中，您可以选择要为配置文件导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为任何您希望的友好名称。 有关更多信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) （在激活批处理目标UI教程中）。

## 验证数据导出 {#exported-data}

对于 [!DNL Pega Profile Connector] 目标， [!DNL Platform] 创建 `.csv` 文件存储在您提供的Amazon S3存储位置中。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。

成功从S3导入用户档案数据后，会在 [!DNL Pega Customer] 配置文件数据存储。 导入的客户用户档案数据可以在 [!DNL Pega Customer Profile Designer] ，如下图所示。
![UI屏幕图像，您可以在Customer Profile Designer中验证Adobe配置文件数据](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在 [!DNL Pega Customer Decision Hub]数据管理员可以在 [!DNL Customer Profile Designer] 要定期从S3导入用户档案数据，如下图所示。 请参阅 [其他资源](#additional-resources) 有关如何配置数据作业以从导入用户档案数据的更多信息 [!DNL Amazon S3].
![用于在Customer Profile Designer中配置数据作业的UI屏幕图像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他资源 {#additional-resources}

请参阅 [导入数据作业](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).



