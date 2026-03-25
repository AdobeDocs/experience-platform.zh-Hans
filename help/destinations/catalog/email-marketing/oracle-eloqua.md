---
keywords: 电子邮件；电子邮件；电子邮件目标；oracle eloqua；oracle
title: （文件）Oracle Eloqua连接
description: Oracle Eloqua是Oracle提供的用于营销自动化的软件即服务(SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售商机开发。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 3%

---

# [!DNL (Files) Oracle Eloqua]连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)是由[!DNL Oracle]提供的用于营销自动化的软件即服务(SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售商机开发。

若要将受众数据发送到[!DNL Oracle Eloqua]，您必须先在[中](#connect-destination)连接目标[!DNL Adobe Experience Platform]，然后[设置数据导入](#import-data-into-eloqua)（从您的存储位置导入[!DNL Oracle Eloqua]）。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
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

此目标支持以下连接类型：

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;连接，您必须提供：
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* 对于&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;连接，您必须提供：
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到&#x200B;**[!UICONTROL Key]**&#x200B;部分下的导出文件。 您的公钥必须编写为[!DNL Base64]编码字符串。
* **[!UICONTROL Name]**：为您的目标选择相关的名称。
* **[!UICONTROL Description]**：输入目标的描述。
* **[!UICONTROL Folder Path]**：提供Experience Platform将导出数据作为CSV文件存储到的存储位置中的路径。
* **[!UICONTROL File Format]**：选择&#x200B;**CSV**&#x200B;以将CSV文件导出到您的存储位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

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

对于[!DNL Oracle Eloqua]目标，Experience Platform会在您提供的存储位置创建一个`.csv`文件。 有关这些文件的详细信息，请参阅受众激活教程中的[验证受众激活](../../ui/activate-batch-profile-destinations.md#verify)。

## 设置数据导入到[!DNL Oracle Eloqua] {#import-data-into-eloqua}

将[!DNL Experience Platform]连接到[!DNL SFTP]存储后，您必须设置从存储位置到[!DNL Oracle Eloqua]的数据导入。 要了解如何完成此操作，请参阅[中的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)导入联系人或帐户[!DNL Oracle Eloqua Help Center]。
