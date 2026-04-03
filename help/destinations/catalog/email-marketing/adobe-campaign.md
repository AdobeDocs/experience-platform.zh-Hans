---
keywords: 电子邮件；电子邮件；电子邮件目标；adobe campaign；campaign
title: Adobe Campaign连接
description: Adobe Campaign 是一套可以帮助您跨所有线上和线下渠道定制和投放营销活动的解决方案。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 5%

---

# [!DNL Adobe Campaign]连接

## 概述 {#overview}

[!DNL Adobe Campaign]是一组解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。 有关详细信息，请参阅[Campaign Classic入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)。

若要将受众数据发送到[!DNL Adobe Campaign]，您必须先在[中](#connect-destination)连接目标[!DNL Adobe Experience Platform]，然后[设置数据导入](#import-data-into-campaign)（从您的存储位置导入[!DNL Adobe Campaign]）。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
| ---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议将某些IP范围添加到SFTP允许列表。

如果需要将Adobe IP添加到您的，请参阅SFTP目标的[IP地址允许列表](../cloud-storage/ip-address-allow-list.md)。

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

[!DNL Adobe Campaign]支持以下连接类型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

将数据发送到[!DNL Adobe Campaign]的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL Amazon S3]**&#x200B;连接，您必须提供您的[!UICONTROL Access Key ID]和[!UICONTROL Secret Access Key]。
* 对于&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;连接，您必须提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL Password]。
* 对于&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;连接，您必须提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL SSH Key]。
* 对于&#x200B;**[!UICONTROL Azure Blob]**&#x200B;连接，必须提供连接字符串。
* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到&#x200B;**[!UICONTROL Key]**&#x200B;部分下的导出文件。 您的公钥必须编写为[!DNL Base64]编码字符串。
* **[!UICONTROL Name]**：为您的目标选择相关的名称。
* **[!UICONTROL Description]**：输入目标的描述。
* **[!UICONTROL Bucket Name]**： *用于S3连接*。 输入S3存储段的位置，[!DNL Experience Platform]会将您的导出数据存为CSV文件。
* **[!UICONTROL Folder Path]**：提供存储位置中的路径，其中[!DNL Experience Platform]会将导出数据存为CSV文件。
* **[!UICONTROL Container]**： *用于Blob连接*。 包含文件夹路径所在的Blob的容器。
* **[!UICONTROL File Format]**：选择&#x200B;**CSV**&#x200B;以将CSV文件导出到您的存储位置。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}


有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从[合并架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关详细信息，请参阅[将受众激活到电子邮件营销目标时的最佳实践](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Adobe Campaign]目标，[!DNL Experience Platform]会在您提供的存储位置中创建一个`.csv`文件。 有关这些文件的详细信息，请参阅Audience Activation教程中的[验证Audience Activation](../../ui/activate-batch-profile-destinations.md#verify)部分。

## 设置数据导入到[!DNL Adobe Campaign] {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 在执行此集成时，请记住[!DNL SFTP]合同规定的[!DNL Adobe Campaign]存储限制、数据库存储限制和活动配置文件限制。
>* 您需要使用[!DNL Adobe Campaign]工作流在[!DNL Campaign]中计划、导入和映射导出的区段。 请参阅[文档中的](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html)设置循环导入[!DNL Adobe Campaign Classic]和[文档中的](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html)关于数据管理活动[!DNL Adobe Campaign Standard]。
>* 将数据发送到[!DNL Adobe Campaign]的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。

将[!DNL Experience Platform]连接到[!DNL Amazon S3]或[!DNL Azure Blob]存储后，您必须设置从存储位置到[!DNL Adobe Campaign]的数据导入。 要了解如何完成此操作，请参阅以下[!DNL Adobe Campaign]文档页面：

* [数据导入和导出入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans)和[文档中的](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html)数据加载（文件）[!DNL Adobe Campaign Classic]。
* [开始使用流程和数据管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html)和[加载文件](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html)（在[!DNL Adobe Campaign Standard]文档中）。
