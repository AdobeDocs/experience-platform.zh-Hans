---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；salesforce;salesforce目标
title: SalesforceMarketing Cloud连接
seo-description: SalesforceMarketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一款以前称为ExactTarget的数字营销套件，它允许您构建和自定义访客和客户的旅程，以个性化其体验。

要向[!DNL Salesforce Marketing Cloud]发送区段数据，必须首先在平台中[连接目标](#connect-destination)，然后[设置从存储位置导入](#import-data-into-salesforce)的[!DNL Salesforce Marketing Cloud]。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## 连接目标{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择[!DNL Salesforce Marketing Cloud]，然后选择&#x200B;**[!UICONTROL Connect destination]**。

![连接到Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，如果您之前已设置到云存储目标的连接，请选择&#x200B;**[!UICONTROL Existing Account]**&#x200B;并选择现有连接之一。 或者，可以选择&#x200B;**[!UICONTROL New Account]**&#x200B;设置新连接。 填写帐户身份验证凭据并选择&#x200B;**[!UICONTROL Connect to destination]**。 对于[!DNL Salesforce Marketing Cloud]，您可以在&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;和&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;之间进行选择。 根据连接类型，填写以下信息，然后选择&#x200B;**[!UICONTROL Connect to destination]**。

对于&#x200B;**[!UICONTROL SFTP with Password]**&#x200B;连接，必须提供域、端口、用户名和密码。

对于&#x200B;**[!UICONTROL SFTP with SSH Key]**&#x200B;连接，必须提供域、端口、用户名和密码。

![填写Salesforce信息](../../assets/catalog/email-marketing/salesforce/account-info.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步骤中，填写目标的相关信息，如下所示：
- **[!UICONTROL Name]**:为目标选择相关名称。
- **[!UICONTROL Description]**:输入目标的说明。
- **[!UICONTROL Bucket name]**:您的Amazon S3存储桶，平台将存放数据导出。输入长度必须介于3到63个字符之间。 必须以字母或数字开头和结尾。 只能包含小写字母、数字或连字符(-)。 不得将格式设置为IP地址（例如192.100.1.1）。
- **[!UICONTROL Folder Path]**:在您的存储位置提供路径，平台将在该路径中将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL File Format]**: **CSV** 或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。
- **[!UICONTROL Marketing actions]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![Salesforce基本信息](../../assets/catalog/email-marketing/salesforce/basic-information.png)

填写上面的字段后，单击&#x200B;**[!UICONTROL Create destination]**。 目标现已连接，您可以[将区段](../../ui/activate-destinations.md)激活到目标。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 目标属性{#destination-attributes}

当[将区段](../../ui/activate-destinations.md)激活到[!DNL Salesforce Marketing Cloud]目标时，建议您从[合并模式](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参阅[在电子邮件营销目标中选择要用作导出文件中目标属性的模式字段](./overview.md#destination-attributes)。

## 导出的数据{#exported-data}

对于[!DNL Salesforce Marketing Cloud]目标，平台会在您提供的存储位置创建制表符分隔的`.txt`或`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 将数据导入到[!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

将平台连接到您的[!DNL Amazon S3]或SFTP存储后，必须将存储位置的数据导入设置为[!DNL Salesforce Marketing Cloud]。 要了解如何实现此操作，请参阅[!DNL Salesforce Help Center]中的[将订阅者从文件](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)导入Marketing Cloud。