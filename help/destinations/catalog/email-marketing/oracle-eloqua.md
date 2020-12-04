---
keywords: email;Email;e-mail;email destinations;oracle eloqua;oracle
title: Oracle雄辩
seo-title: Oracle雄辩
description: Oracle雄辩是Oracle公司提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
seo-description: Oracle雄辩是Oracle公司提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## 概述

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是由B2B营销人员和组织提供的营销自动化软件即服务(SaaS) [!DNL Oracle] 平台，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

要将区段数据发 [!DNL Oracle Eloqua]送到，您必 [须先在实时客户数据平台](#connect-destination) 中连接目标，然后 [设置从存储位置导入](#import-data-into-eloqua) 到的数据 [!DNL Oracle Eloqua]。

## 导出类型 {#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](../../ui/activate-destinations.md#select-attributes)。

## 连接到目标 {#connect-destination}

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Oracle Eloqua]，选 **[!UICONTROL 择，然后选择]**“连接目标”。

[连接到Elovica](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接之一。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 对于 [!DNL Oracle Eloqua]，您可以在带密 **[!UICONTROL 码的SFTP和]****[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型填写以下信息，然后选择“连 **[!UICONTROL 接到目标”]**。

对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

![设置Elova向导](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

在设 **[!UICONTROL 置步]** 骤中，填写目标的相关信息，如下所示：
- **[!UICONTROL 名称]**:为目标选择相关名称。
- **[!UICONTROL 描述]**:输入目标的说明。
- **[!UICONTROL 文件夹路径]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。

![雄辩基本信息](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

填写 **[!UICONTROL 上述字段]** 后，单击创建目标。 您的目标现已创建完毕，您 [可以将区段](../../ui/activate-destinations.md) 激活到目标。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](../../ui/activate-destinations.md) ，请参阅将激活和区段激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](../../ui/activate-destinations.md) 活到目 [!DNL Oracle Eloqua] 标时 [，建议您从合并模式中选择唯一标](../../../profile/home.md#profile-fragments-and-union-schemas)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](./overview.md#destination-attributes) 的模式字段。

## 导出的数据 {#exported-data}

对 [!DNL Oracle Eloqua] 于目标，实时CDP会在您提供的存储位置 `.txt` 创建制 `.csv` 表符分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](../../ui/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。

## 将数据导入设置为 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

在将实时CDP连接到您的AmazonS3或SFTP存储后，您必须设置从存储位置导入到的数据 [!DNL Oracle Eloqua]。 要了解如何完成此操作，请参阅 [中的导入联系人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 或帐户 [!DNL Oracle Eloqua Help Center]。