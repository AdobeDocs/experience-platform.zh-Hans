---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；oracle雄辩；oracle
title: OracleEloqua连接
description: OracleEloqua是由Oracle提供的软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索的生成。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 是提供的软件即服务(SaaS)平台，用于营销自动化 [!DNL Oracle] 旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

将区段数据发送到 [!DNL Oracle Eloqua]，则必须先 [连接目标](#connect-destination) 在Adobe Experience Platform [设置数据导入](#import-data-into-eloqua) 从您的存储位置到 [!DNL Oracle Eloqua].

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从 [受众激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes).

## IP地址允许列表 {#allow-list}

通过SFTP存储设置电子邮件营销目标时，Adobe建议您向允许列表添加某些IP范围。

请参阅 [云存储目标的IP地址允许列表](../cloud-storage/ip-address-allow-list.md) 如果您需要将AdobeIP添加到允许列表。

## 连接到目标 {#connect}

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
* **[!UICONTROL 文件格式]**: **CSV** 或 **制表符分隔**. 选择要导出到存储位置的文件格式。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## 将区段激活到此目标 {#activate}

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#destination-attributes}

在将区段激活到此目标时，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标时的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对于 [!DNL Oracle Eloqua] 目标，平台会创建 `.csv` 文件。 有关文件的更多信息，请参阅 [验证区段激活](../../ui/activate-batch-profile-destinations.md#verify) 区段激活教程中的。

## 设置数据导入到 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

连接后 [!DNL Platform] 至 [!DNL SFTP] 存储中，您必须将数据从存储位置导入到 [!DNL Oracle Eloqua]. 要了解如何完成此操作，请参阅 [导入联系人或帐户](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 在 [!DNL Oracle Eloqua Help Center].
