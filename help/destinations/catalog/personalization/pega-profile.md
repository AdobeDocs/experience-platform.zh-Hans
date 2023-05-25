---
title: Pega配置文件连接器
description: 使用Adobe Experience Platform中用于Amazon S3的Pega配置文件连接器将完整配置文件数据或（或）增量配置文件数据导出到Amazon S3云存储。 在Pega Customer Decision Hub中，可以在Customer Profile Designer中安排数据作业，以定期从Amazon S3存储中导入用户档案数据。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Pega配置文件连接器

## 概述 {#overview}

使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中创建到 [!DNL Amazon Web Services] (AWS) S3存储定期将配置文件数据从Adobe Experience Platform导出到CSV文件，并导入您自己的S3存储桶中。 In [!DNL Pega Customer Decision Hub]，您可以安排数据作业以从S3存储中导入此配置文件数据以更新 [!DNL Pega Customer Decision Hub] 个人资料。

此连接器有助于设置配置文件数据的初始导出，还有助于定期将新配置文件同步到 [!DNL Pega Customer Decision Hub].  在客户决策中心拥有最新数据可让您更好地了解客户群，从而做出下一个最佳决策。

>[!IMPORTANT]
>
>此文档页面由Pegasystems创建。 如有任何查询或更新请求，请直接联系Pega [此处](mailto:support@pega.com).

## 用例

为了帮助您更好地了解应该如何以及何时使用 [!DNL Pega Profile Connector] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例1

营销人员希望首先设置 [!DNL Pega Customer Decision Hub] ，并从Adobe Experience Platform加载配置文件数据。 这是初始满负荷，然后按计划进行增量负荷。

### 用例2

营销人员希望在Adobe Experience Platform中获取最新的配置文件数据 [!DNL Pega Customer Decision Hub] 能够持续增强Pega对客户个人资料的洞察。

## 先决条件 {#prerequisites}

使用此目标将数据从Adobe Experience Platform导出并将用户档案导入之前 [!DNL Pega Customer Decision Hub]，确保您完成了以下先决条件：

* 配置 [!DNL Amazon S3] 存储桶和用于导出和导入数据文件的文件夹路径。
* 配置 [!DNL Amazon S3] 访问密钥和 [!DNL Amazon S3] 密钥：在 [!DNL Amazon S3]，生成 `access key - secret access key` 配对以授予Platform对的访问权限 [!DNL Amazon S3] 帐户。
* 要成功连接数据并将其导出到 [!DNL Amazon S3] 存储位置，创建身份和访问管理(IAM)用户 [!DNL Platform] 在 [!DNL Amazon S3] 并分配权限，例如 `s3:DeleteObject`， `s3:GetBucketLocation`， `s3:GetObject`， `s3:ListBucket`， `s3:PutObject`， `s3:ListMultipartUploadParts`
* 确保您的 [!DNL Pega Customer Decision Hub] 实例已升级到8.8版本或更高版本。

## 支持的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支持激活下表中描述的自定义用户ID。 有关更多详细信息，请参阅 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 |
|---|---|
| *客户ID* | 唯一标识用户档案的通用用户标识符 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**： In [!DNL Amazon S3]，生成 `access key - secret access key` 对，以授予Adobe Experience Platform对的访问权限 [!DNL Amazon S3] 帐户。 了解详情，请参阅 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 填写目标详细信息 {#destination-details}

在建立与的身份验证连接后 [!DNL Amazon S3]，为目标提供以下信息：

![显示Pega配置文件连接器目标详细信息的已完成字段的UI屏幕的图像](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**. UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 存储段名称]**：输入 [!DNL Amazon S3] 要由此目标使用的存储段。
* **[!UICONTROL 文件夹路径]**：输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 压缩类型]**：将压缩类型选择为GZIP或NONE。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的区段文件在Amazon S3存储中创建自定义文件夹。 读取 [使用宏在您的存储位置中创建文件夹](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 以获取说明。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

在 **[!UICONTROL 映射]** 步骤，您可以选择为用户档案导出哪些属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批次目标UI教程中。

## 验证数据导出 {#exported-data}

对象 [!DNL Pega Profile Connector] 目标， [!DNL Platform] 创建 `.csv` 文件，该文件位于您提供的Amazon S3存储位置。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在区段激活教程中。

从S3成功导入配置文件数据会在 [!DNL Pega Customer] 配置文件数据存储。 可以在中验证导入的客户配置文件数据 [!DNL Pega Customer Profile Designer] ，如下图所示。
![可在其中验证Customer Profile Designer中Adobe配置文件数据的UI屏幕的图像](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

In [!DNL Pega Customer Decision Hub]，数据管理员可以在中配置数据作业 [!DNL Customer Profile Designer] 定期从S3导入配置文件数据，如下图所示。 请参阅 [其他资源](#additional-resources) 有关如何配置数据作业以从中导入配置文件数据的更多信息 [!DNL Amazon S3].
![用于在客户配置文件设计器中配置数据作业的UI屏幕图像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他资源 {#additional-resources}

参见 [导入数据作业](https://academy.pega.com/topic/import-data-jobs/v1) 在 [!DNL Pega Customer Decision Hub].

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).
