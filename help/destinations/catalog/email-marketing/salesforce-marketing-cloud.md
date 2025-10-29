---
title: Salesforce Marketing Cloud连接
description: Salesforce Marketing Cloud是一个数字营销套件，以前称为ExactTarget；它允许您为访客和客户构建和自定义历程，以个性化其体验。
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud]连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/)是一个数字营销套件，以前称为ExactTarget，它允许您为访客和客户构建和自定义历程，以个性化其体验。

若要将受众数据发送到[!DNL Salesforce Marketing Cloud]，您必须先[连接到Experience Platform中的目标](#connect-destination)，然后[设置数据导入](#import-data-into-salesforce)（从您的存储位置导入[!DNL Salesforce Marketing Cloud]）。

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
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议将某些IP范围添加到SFTP允许列表。

如果您需要将Adobe 列入允许列表 IP添加到SFTP允许列表，请参阅[SFTP目标的IP地址](../cloud-storage/ip-address-allow-list.md)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

此目标支持以下连接类型：

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;连接，您必须提供：
   * **[!UICONTROL Domain]**： SFTP帐户的IP地址或域名；
   * **[!UICONTROL Port]**： SFTP存储位置使用的端口；
   * **[!UICONTROL Username]**：用于登录到SFTP存储位置的用户名；
   * **[!UICONTROL Password]**：用于登录到SFTP存储位置的密码。
* 对于&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;连接，您必须提供：
   * **[!UICONTROL Domain]**： SFTP帐户的IP地址或域名；
   * **[!UICONTROL Port]**： SFTP存储位置使用的端口；
   * **[!UICONTROL Username]**：用于登录到SFTP存储位置的用户名；
   * **[!UICONTROL SSH Key]**：用于登录到SFTP存储位置的私有SSH密钥。 私钥必须采用Base64编码的字符串格式，且不得受密码保护。

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

将受众激活到此目标时，Adobe建议您从[合并架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关详细信息，请参阅将受众激活到电子邮件营销目标时的最佳实践[&#128279;](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Salesforce Marketing Cloud]目标，Experience Platform会在您提供的存储位置创建一个`.csv`文件。 有关这些文件的详细信息，请参阅受众激活教程中的[验证受众激活](../../ui/activate-batch-profile-destinations.md#verify)。

## 设置数据导入到[!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

将[!DNL Experience Platform]连接到[!DNL SFTP]存储后，您必须设置从存储位置到[!DNL Salesforce Marketing Cloud]的数据导入。 要了解如何完成此操作，请参阅[将订阅者从](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5)中的文件[!DNL Salesforce Help Center]导入Marketing Cloud。
