---
title: SalesforceMarketing Cloud连接
description: SalesforceMarketing Cloud是一个数字营销套件，以前称为ExactTarget，通过它，可为访客和客户构建和自定义历程以个性化其体验。
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一个数字营销套件，以前称为ExactTarget，可让您为访客和客户构建和自定义历程，以个性化其体验。

要将受众数据发送到，请执行以下操作 [!DNL Salesforce Marketing Cloud]，您必须首先 [连接到目标](#connect-destination) 在Platform中，然后 [设置数据导入](#import-data-into-salesforce) 从存储位置移至 [!DNL Salesforce Marketing Cloud].

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议将某些IP范围添加到SFTP允许列表。

请参阅 [列入允许列表 SFTP目标的IP地址](../cloud-storage/ip-address-allow-list.md) 如果您需要将AdobeIP添加到允许列表。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

此目标支持以下连接类型：

* **[!UICONTROL 包含密码的SFTP]**
* **[!UICONTROL 包含SSH密钥的SFTP]**

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* 对象 **[!UICONTROL 包含密码的SFTP]** 连接，您必须提供：
   * **[!UICONTROL 域]**：SFTP帐户的IP地址或域名；
   * **[!UICONTROL 端口]**：您的SFTP存储位置使用的端口；
   * **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
   * **[!UICONTROL 密码]**：用于登录到SFTP存储位置的密码。
* 对象 **[!UICONTROL 包含SSH密钥的SFTP]** 连接，您必须提供：
   * **[!UICONTROL 域]**：SFTP帐户的IP地址或域名；
   * **[!UICONTROL 端口]**：您的SFTP存储位置使用的端口；
   * **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
   * **[!UICONTROL SSH密钥]**：用于登录到SFTP存储位置的私有SSH密钥。 私钥必须采用Base64编码的字符串格式，且不得受密码保护。

* 或者，您可以附加RSA格式的公钥，将带有PGP/GPG的加密添加到导出文件中的 **[!UICONTROL 键]** 部分。 您的公钥必须编写为 [!DNL Base64] 编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* **[!UICONTROL 文件夹路径]**：提供Platform将导出数据作为CSV文件存储到的存储位置中的路径。
* **[!UICONTROL 文件格式]**：选择 **CSV** 以将CSV文件导出到存储位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从 [合并架构](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对象 [!DNL Salesforce Marketing Cloud] 目标，平台创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [验证受众激活](../../ui/activate-batch-profile-destinations.md#verify) 在audience activation教程中。

## 设置数据导入到 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

连接后 [!DNL Platform] 敬您的 [!DNL SFTP] 存储时，您必须设置从存储位置导入到的数据导入 [!DNL Salesforce Marketing Cloud]. 要了解如何完成此操作，请参阅 [将订阅者从文件导入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 在 [!DNL Salesforce Help Center].
