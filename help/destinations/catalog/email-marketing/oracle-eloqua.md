---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；oracle雄辩；oracle
title: Oracle Elvoca连接
description: Oracle Evola是由Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
translation-type: tm+mt
source-git-commit: 29b4eaca06e2f1032584a0b4720490934a6e1fa7
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 是由B2B营销人员和组织提供的用于营销自动化的软件即服务( [!DNL Oracle] SaaS)平台，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

要向[!DNL Oracle Eloqua]发送区段数据，必须先在Adobe Experience Platform中[连接目标](#connect-destination)，然后[将存储位置中的数据导入](#import-data-into-eloqua)设置为[!DNL Oracle Eloqua]。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## IP地址允许列表{#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议您向允许列表添加某些IP范围。

如果您需要将AdobeIP添加到允许列表，请参阅云存储目标](../cloud-storage/ip-address-allow-list.md)的[ IP地址允许列表。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择[!DNL Oracle Eloqua]，然后选择&#x200B;**[!UICONTROL Configure]**。

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关[!UICONTROL Activate]和[!UICONTROL Configure]之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。

![连接到Evola](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

在&#x200B;**[!UICONTROL Account]**&#x200B;步骤中，如果您之前已设置到云存储目标的连接，请选择&#x200B;**[!UICONTROL Existing Account]**&#x200B;并选择现有连接之一。 或者，可以选择&#x200B;**[!UICONTROL New Account]**&#x200B;设置新连接。 填写帐户身份验证凭据并选择&#x200B;**[!UICONTROL Connect to destination]**。 对于[!DNL Oracle Eloqua]，您可以在&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;和&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;之间进行选择。

![Connect Evola帐户](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

根据连接类型，填写以下信息，然后选择&#x200B;**[!UICONTROL Connect to destination]**。

- 对于&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;连接，必须提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL Password]。
- 对于&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;连接，必须提供[!UICONTROL Domain]、[!UICONTROL Port]、[!UICONTROL Username]和[!UICONTROL SSH Key]。

或者，您也可以附加RSA格式的公钥，以便将PGP/GPG加密添加到&#x200B;**[!UICONTROL Key]**&#x200B;部分下的导出文件。 您的公钥必须写入为[!DNL Base64]编码字符串。

![Evola连接到目标](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，填写目标的相关信息，如下所示：
- **[!UICONTROL Name]**:为目标选择相关名称。
- **[!UICONTROL Description]**:输入目标的说明。
- **[!UICONTROL Folder Path]**:在您的存储位置提供路径，平台将在该路径中将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL File Format]**: **CSV** 或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。
- **[!UICONTROL Marketing actions]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![雄辩的基本信息](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

填写上面的字段后，单击&#x200B;**[!UICONTROL Create destination]**。 您的目标现在已创建，您可以[将区段](../../ui/activate-destinations.md)激活到目标。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 目标属性{#destination-attributes}

当[将区段](../../ui/activate-destinations.md)激活到[!DNL Oracle Eloqua]目标时，Adobe建议您从[合并模式](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参阅[选择要用作导出文件中目标属性的模式字段](./overview.md#destination-attributes)。

## 导出的数据{#exported-data}

对于[!DNL Oracle Eloqua]目标，平台会在您提供的存储位置创建制表符分隔的`.txt`或`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 将数据导入到[!DNL Oracle Eloqua] {#import-data-into-eloqua}

将[!DNL Platform]连接到SFTP存储后，必须将存储位置中的数据导入设置为[!DNL Oracle Eloqua]。 要了解如何实现此操作，请参阅[!DNL Oracle Eloqua Help Center]中的[导入联系人或帐户](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)。
