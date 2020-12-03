---
keywords: email;Email;e-mail;email destinations;salesforce;salesforce destination
title: SalesforceMarketing Cloud
seo-title: SalesforceMarketing Cloud
description: SalesforceMarketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
seo-description: SalesforceMarketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## 概述

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一款以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。

要将存储发 [!DNL Salesforce Marketing Cloud]送到，您必 [须首先以实时CDP连接目](#connect-destination) 标，然后设置从位置 [到的数据导入](#import-data-into-salesforce)[!DNL Salesforce Marketing Cloud]。

## 导出类型 {#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](../../ui/activate-destinations.md#select-attributes)。

## 连接目标 {#connect-destination}

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Salesforce Marketing Cloud]，选 **[!UICONTROL 择，然后选择]**“连接目标”。

![连接到Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接之一。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 对于 [!DNL Salesforce Marketing Cloud]，您可以在带密 **[!UICONTROL 码的SFTP和]****[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型填写以下信息，然后选择“连 **[!UICONTROL 接到目标”]**。

对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。

对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

![填写Salesforce信息](../../assets/catalog/email-marketing/salesforce/account-info.png)

在设 **[!UICONTROL 置步]** 骤中，填写目标的相关信息，如下所示：
- **[!UICONTROL 名称]**:为目标选择相关名称。
- **[!UICONTROL 描述]**:输入目标的说明。
- **[!UICONTROL 文件夹路径]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL 文件格式]**: **[!UICONTROL CSV]** 或 **[!UICONTROL TAB_DELIMITED]**。 选择要导出到存储位置的文件格式。

![Salesforce基本信息](../../assets/catalog/email-marketing/salesforce/basic-information.png)

填写 **[!UICONTROL 上述字段]** 后，单击创建目标。 您的目标现已连接，您可 [以将区段](../../ui/activate-destinations.md) 激活到目标。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](../../ui/activate-destinations.md) ，请参阅将激活和区段激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](../../ui/activate-destinations.md) 活到目 [!DNL Salesforce Marketing Cloud] 标时 [，建议您从合并模式中选择唯一标](../../../profile/home.md#profile-fragments-and-union-schemas)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](./overview.md#destination-attributes) 的模式字段。

## 导出的数据 {#exported-data}

对 [!DNL Salesforce Marketing Cloud] 于目标，实时CDP会在您提供的存储位置 `.txt` 创建制 `.csv` 表符分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](../../ui/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Salesforce_Marketing_Cloud_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 将数据导入设置为 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

在将实时CDP连接到您的 [!DNL Amazon S3] 或SFTP存储后，您必须设置从存储位置导入到的数据 [!DNL Salesforce Marketing Cloud]。 要了解如何完成此操作，请参 [阅中的将订阅者从文件导入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) (位于 [!DNL Salesforce Help Center])。