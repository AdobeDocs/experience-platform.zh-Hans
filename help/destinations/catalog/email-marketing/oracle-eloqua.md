---
keywords: 电子邮件；电子邮件；电子邮件目标；oracle eloqua；oracle
title: （文件）Oracle Eloqua连接
description: Oracle Eloqua是Oracle提供的用于营销自动化的软件即服务(SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售商机开发。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---

# [!DNL (Files) Oracle Eloqua]连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)是由[!DNL Oracle]提供的用于营销自动化的软件即服务(SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售商机开发。

若要将受众数据发送到[!DNL Oracle Eloqua]，您必须先在Adobe Experience Platform中[连接目标](#connect-destination)，然后[设置数据导入](#import-data-into-eloqua)（从您的存储位置导入[!DNL Oracle Eloqua]）。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议向允许列表添加特定IP范围。

如果您需要将Adobe IP添加到允许列表，请参阅SFTP目标的[IP地址允许列表](../cloud-storage/ip-address-allow-list.md)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

此目标支持以下连接类型：

* 使用密码&#x200B;**[!UICONTROL SFTP]**
* 使用SSH密钥的&#x200B;**[!UICONTROL SFTP]**

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于使用密码&#x200B;**的** SFTP连接，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL 密码]
* 对于使用SSH密钥&#x200B;**连接的** SFTP，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL SSH密钥]

* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到&#x200B;**[!UICONTROL 密钥]**&#x200B;部分下的导出文件。 您的公钥必须编写为[!DNL Base64]编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* **[!UICONTROL 文件夹路径]**：提供Experience Platform将导出数据作为CSV文件存入的存储位置的路径。
* **[!UICONTROL 文件格式]**：选择&#x200B;**CSV**&#x200B;以将CSV文件导出到您的存储位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从[合并架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关详细信息，请参阅将受众激活到电子邮件营销目标时的最佳实践[&#128279;](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Oracle Eloqua]目标，Experience Platform会在您提供的存储位置创建一个`.csv`文件。 有关这些文件的详细信息，请参阅受众激活教程中的[验证受众激活](../../ui/activate-batch-profile-destinations.md#verify)。

## 设置数据导入到[!DNL Oracle Eloqua] {#import-data-into-eloqua}

将[!DNL Experience Platform]连接到[!DNL SFTP]存储后，您必须设置从存储位置到[!DNL Oracle Eloqua]的数据导入。 要了解如何完成此操作，请参阅[!DNL Oracle Eloqua Help Center]中的[导入联系人或帐户](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)。
