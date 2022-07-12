---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；Salesforce;Salesforce目标
title: SalesforceMarketing Cloud连接
description: SalesforceMarketing Cloud是一个以前称为ExactTarget的数字营销套件，允许您为访客和客户构建和自定义历程，以个性化其体验。
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一个以前称为ExactTarget的数字营销套件，允许您构建和自定义访客和客户的历程，以个性化其体验。

将区段数据发送到 [!DNL Salesforce Marketing Cloud]，则必须先 [连接目标](#connect-destination) 在平台中，然后 [设置数据导入](#import-data-into-salesforce) 从您的存储位置到 [!DNL Salesforce Marketing Cloud].

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP地址允许列表 {#allow-list}

通过SFTP存储设置电子邮件营销目标时，Adobe建议您向允许列表添加某些IP范围。

请参阅 [云存储目标的IP地址允许列表](../cloud-storage/ip-address-allow-list.md) 如果您需要将AdobeIP添加到允许列表。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

此目标支持以下连接类型：

* **[!UICONTROL 带密码的SFTP]**
* **[!UICONTROL 具有SSH密钥的SFTP]**

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* 对于 **[!UICONTROL 带密码的SFTP]** 连接，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL 密码]
* 对于 **[!UICONTROL 具有SSH密钥的SFTP]** 连接，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL SSH密钥]

* 或者，您也可以将RSA格式的公钥附加到 **[!UICONTROL 键]** 中。 您的公钥必须写为 [!DNL Base64] 编码字符串。
* **[!UICONTROL 名称]**:为您的目标选择相关名称。
* **[!UICONTROL 描述]**:输入目标的描述。
* **[!UICONTROL 文件夹路径]**:在存储位置中提供路径，Platform会将导出数据存储为CSV文件。
* **[!UICONTROL 文件格式]**:选择 **CSV** 将CSV文件导出到存储位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#destination-attributes}

在将区段激活到此目标时，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标时的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对于 [!DNL Salesforce Marketing Cloud] 目标，平台会创建 `.csv` 文件。 有关文件的更多信息，请参阅 [验证区段激活](../../ui/activate-batch-profile-destinations.md#verify) 区段激活教程中的。

## 设置数据导入到 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

连接后 [!DNL Platform] 至 [!DNL SFTP] 存储中，您必须将数据从存储位置导入到 [!DNL Salesforce Marketing Cloud]. 要了解如何完成此操作，请参阅 [将订阅者从文件导入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 在 [!DNL Salesforce Help Center].
