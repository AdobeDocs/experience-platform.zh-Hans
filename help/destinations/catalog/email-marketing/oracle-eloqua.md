---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；oracle雄辩；oracle
title: Oracle Evola连接
description: Oracle Evola是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是由B2B营销人员和组织提供的用于营销自动化的软件即服务( [!DNL Oracle] SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

要向[!DNL Oracle Eloqua]发送区段数据，必须先在Adobe Experience Platform中[连接目标](#connect-destination)，然后[将存储位置中的数据导入](#import-data-into-eloqua)设置为[!DNL Oracle Eloqua]。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Oracle Eloqua]，然后选择&#x200B;**[!UICONTROL 连接目标]**。

[连接到Evola](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，如果您之前已设置到云存储目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择现有连接之一。 或者，您可以选择&#x200B;**[!UICONTROL 新建帐户]**&#x200B;来设置新连接。 填写帐户身份验证凭据，然后选择&#x200B;**[!UICONTROL 连接到目标]**。 对于[!DNL Oracle Eloqua]，您可以在&#x200B;**[!UICONTROL 带密码]**&#x200B;的SFTP和&#x200B;**[!UICONTROL 带SSH密钥]**&#x200B;的SFTP之间进行选择。 根据连接类型，填写以下信息，然后选择&#x200B;**[!UICONTROL 连接到目标]**。

对于具有Password ]**连接的**[!UICONTROL  SFTP，必须提供域、端口、用户名和密码。
对于具有SSH密钥]**连接的**[!UICONTROL  SFTP，必须提供域、端口、用户名和密码。

![设置Elova向导](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

在&#x200B;**[!UICONTROL 设置]**&#x200B;步骤中，填写目标的相关信息，如下所示：
- **[!UICONTROL 名称]**:为目标选择相关名称。
- **[!UICONTROL 描述]**:输入目标的说明。
- **[!UICONTROL 存储段名称]**:您的Amazon S3存储桶，平台将存放数据导出。输入长度必须介于3到63个字符之间。 必须以字母或数字开头和结尾。 只能包含小写字母、数字或连字符(-)。 不得将格式设置为IP地址（例如192.100.1.1）。
- **[!UICONTROL 文件夹路径]**:在您的存储位置提供路径，平台将在该路径中将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。
- **[!UICONTROL 营销操作]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![雄辩的基本信息](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

填写上面的字段后，单击&#x200B;**[!UICONTROL 创建目标]**。 您的目标现在已创建，您可以[将区段](../../ui/activate-destinations.md)激活到目标。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 目标属性{#destination-attributes}

当[将区段](../../ui/activate-destinations.md)激活到[!DNL Oracle Eloqua]目标时，建议您从[合并模式](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参阅[在电子邮件营销目标中选择要用作导出文件中目标属性的模式字段](./overview.md#destination-attributes)。

## 导出的数据{#exported-data}

对于[!DNL Oracle Eloqua]目标，平台会在您提供的存储位置创建制表符分隔的`.txt`或`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 将数据导入到[!DNL Oracle Eloqua] {#import-data-into-eloqua}

将平台连接到Amazon S3或SFTP存储后，必须将存储位置的数据导入设置为[!DNL Oracle Eloqua]。 要了解如何实现此操作，请参阅[!DNL Oracle Eloqua Help Center]中的[导入联系人或帐户](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)。