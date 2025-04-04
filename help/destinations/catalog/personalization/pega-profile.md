---
title: Pega配置文件连接器
description: 使用Adobe Experience Platform中Amazon S3的Pega配置文件连接器将完整的或增量的（或同时使用两者）配置文件数据导出到Amazon S3云存储。 在Pega客户决策中心中，可以安排客户配置文件Designer中的数据作业，以定期从Amazon S3存储导入配置文件数据。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 4%

---

# Pega配置文件连接器

## 概述 {#overview}

在Adobe Experience Platform中使用[!DNL Pega Profile Connector]创建到[!DNL Amazon Web Services] (AWS) S3存储的实时出站连接，定期将配置文件数据导出到Adobe Experience Platform中的CSV文件，并导入到您自己的S3存储桶中。 在 [!DNL Pega Customer Decision Hub] 中，您可以安排数据作业从 S3 存储中导入该轮廓数据，以更新[!DNL Pega Customer Decision Hub]轮廓。

此连接器可帮助设置配置文件数据的初始导出，并帮助定期将新配置文件同步到[!DNL Pega Customer Decision Hub]中。  在客户决策中心保存最新数据可让您更好地了解客户群，从而做出下一个最佳决策。

>[!IMPORTANT]
>
>此目标连接器和文档页面由Pegasystems创建和维护。 如有任何查询或更新请求，请直接在[此处](mailto:support@pega.com)联系Pega。

## 用例

为了帮助您更好地了解您应如何以及何时使用[!DNL Pega Profile Connector]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例1

营销人员最初想要使用从Adobe Experience Platform加载的配置文件数据设置[!DNL Pega Customer Decision Hub]。 这是初始满负荷，然后按计划增加负荷。

### 用例2

营销人员希望在[!DNL Pega Customer Decision Hub]中提供Adobe Experience Platform的最新配置文件数据，以便持续增强关于客户配置文件的Pega见解。

## 先决条件 {#prerequisites}

使用此目标将数据从Adobe Experience Platform导出并将配置文件导入[!DNL Pega Customer Decision Hub]之前，请确保您完成以下先决条件：

* 配置[!DNL Amazon S3]存储段以及要用于导出和导入数据文件的文件夹路径。
* 配置[!DNL Amazon S3]访问密钥和[!DNL Amazon S3]密钥：在[!DNL Amazon S3]中，生成一个`access key - secret access key`对以授予Experience Platform对您的[!DNL Amazon S3]帐户的访问权限。
* 若要成功连接数据并将其导出到您的[!DNL Amazon S3]存储位置，请在[!DNL Amazon S3]中为[!DNL Experience Platform]创建标识和访问管理(IAM)用户，并分配`s3:DeleteObject`、`s3:GetBucketLocation`、`s3:GetObject`、`s3:ListBucket`、`s3:PutObject`、`s3:ListMultipartUploadParts`等权限
* 确保您的[!DNL Pega Customer Decision Hub]实例已升级到8.8或更高版本。

## 支持的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub]支持激活下表中描述的自定义用户ID。 有关详细信息，请参阅[标识](/help/identity-service/features/namespaces.md)。

| 目标身份 | 描述 |
|---|---|
| *客户ID* | 在[!DNL Pega Customer Decision Hub]和Adobe Experience Platform中唯一标识配置文件的通用用户标识符 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

* **[!DNL Amazon S3]访问密钥**&#x200B;和&#x200B;**[!DNL Amazon S3]密钥**：在[!DNL Amazon S3]中，生成一个`access key - secret access key`对以授予Adobe Experience Platform对您[!DNL Amazon S3]帐户的访问权限。 请参阅[Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)以了解详情。

### 填写目标详细信息 {#destination-details}

建立与[!DNL Amazon S3]的身份验证连接后，提供目标的以下信息：

![显示Pega配置文件连接器目标详细信息的已完成字段的UI屏幕图像](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

要配置目标的详细信息，请填写必填字段并选择&#x200B;**[!UICONTROL 下一步]**。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入有助于识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 存储段名称]**：输入要由此目标使用的[!DNL Amazon S3]存储段的名称。
* **[!UICONTROL 文件夹路径]**：输入将承载导出文件的目标文件夹的路径。
* **[!UICONTROL 压缩类型]**：选择GZIP或NONE压缩类型。

>[!TIP]
>
>在连接目标工作流中，您可以在Amazon S3存储中为每个导出的受众文件创建一个自定义文件夹。 有关说明，请阅读[使用宏在存储位置](/help/destinations/catalog/cloud-storage/overview.md#use-macros)中创建文件夹。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 映射属性和身份 {#map}

在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，您可以为配置文件选择要导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看激活批处理目标UI教程中的[映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 验证数据导出 {#exported-data}

对于[!DNL Pega Profile Connector]目标，[!DNL Experience Platform]会在您提供的Amazon S3存储位置中创建一个`.csv`文件。 有关这些文件的详细信息，请参阅受众激活教程中的[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

从S3成功导入配置文件数据会在[!DNL Pega Customer]配置文件数据存储中插入数据。 可以在[!DNL Pega Customer Profile Designer]中验证导入的客户配置文件数据，如下图所示。
![UI屏幕的图像，您可以在其中验证客户个人资料Designer中的Adobe个人资料数据](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在[!DNL Pega Customer Decision Hub]中，数据管理员可以将[!DNL Customer Profile Designer]中的数据作业配置为定期从S3导入配置文件数据，如下图所示。 有关如何配置数据作业以从[!DNL Amazon S3]导入配置文件数据的详细信息，请参阅[其他资源](#additional-resources)。
![用于在客户个人资料Designer中配置数据作业的UI屏幕图像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他资源 {#additional-resources}

查看[!DNL Pega Customer Decision Hub]中的[导入数据作业](https://academy.pega.com/topic/import-data-jobs/v1)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
