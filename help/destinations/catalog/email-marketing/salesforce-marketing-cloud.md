---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；Salesforce;Salesforce目标
title: SalesforceMarketing Cloud连接
seo-description: SalesforceMarketing Cloud是一个以前称为ExactTarget的数字营销套件，允许您为访客和客户构建和自定义历程，以个性化其体验。
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一个以前称为ExactTarget的数字营销套件，允许您构建和自定义访客和客户的历程，以个性化其体验。

要将区段数据发送到[!DNL Salesforce Marketing Cloud]，必须先在Platform中[连接目标](#connect-destination)，然后[设置从存储位置导入](#import-data-into-salesforce)的数据。[!DNL Salesforce Marketing Cloud]

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从受众激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-batch-profile-destinations.md#select-attributes)。

## IP地址允许列表 {#allow-list}

通过SFTP存储设置电子邮件营销目标时，Adobe建议您向允许列表添加某些IP范围。

如果需要向允许列表添加AdobeIP，请参阅云存储目标的[IP地址允许列表](../cloud-storage/ip-address-allow-list.md) 。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

此目标支持以下连接类型：

* **[!UICONTROL 带密码的SFTP]**
* **[!UICONTROL 具有SSH密钥的SFTP]**

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL 带密码的SFTP]**&#x200B;连接，必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL 密码]
* 对于&#x200B;**[!UICONTROL 具有SSH密钥的SFTP]**&#x200B;连接，必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL SSH密钥]

* 或者，您也可以附加RSA格式的公钥，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下将PGP/GPG加密添加到导出的文件中。 您的公钥必须写为[!DNL Base64]编码字符串。
* **[!UICONTROL 名称]**:为您的目标选择相关名称。
* **[!UICONTROL 描述]**:输入目标的描述。
* **[!UICONTROL 文件夹路径]**:在存储位置中提供路径，Platform会将导出数据存储为CSV或制表符分隔的文件。
* **[!UICONTROL 文件格式]**: **** CSV或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 目标属性 {#destination-attributes}

在将区段激活到此目标时，Adobe建议您从[并集架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关更多信息，请参阅[将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Salesforce Marketing Cloud]目标，Platform会在您提供的存储位置中创建一个以制表符分隔的`.csv`文件。 有关这些文件的更多信息，请参阅区段激活教程中的[验证区段激活](../../ui/activate-batch-profile-destinations.md#verify) 。

## 设置数据导入到[!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

将[!DNL Platform]连接到[!DNL SFTP]存储后，必须将数据从存储位置导入[!DNL Salesforce Marketing Cloud]。 要了解如何完成此操作，请参阅[!DNL Salesforce Help Center]中的[将订阅者从文件](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)导入Marketing Cloud。
