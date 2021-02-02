---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；adobe活动;活动
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
seo-description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
translation-type: tm+mt
source-git-commit: cf2d76799c03a2ea0414aedd83b35f3ce2ca3cb5
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。 有关详细信息，请参阅[关于Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)。

要向Adobe Campaign发送段数据，您必须先[连接Adobe Experience Platform的目标](#connect-destination)，然后[设置从存储位置到Adobe Campaign的数据导入](#import-data-into-campaign)。

## 导出类型{#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](../../ui/activate-destinations.md#select-attributes)。

## 连接目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择Adobe Campaign，然后选择&#x200B;**[!UICONTROL 连接目标]**。

![连接到adobe活动](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

在Connect目标工作流中，为存储位置选择&#x200B;**[!UICONTROL 连接类型]**。 对于Adobe Campaign，您可以选择&#x200B;**[!UICONTROL AmazonS3]**、**[!UICONTROL 口令为SFTP]**、**[!UICONTROL SFTP为SSH密钥为]**&#x200B;和&#x200B;**[!UICONTROL Azure Blob]**。 根据连接类型，填写以下信息，然后选择&#x200B;**[!UICONTROL Connect]**。

![设置活动向导](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- 对于&#x200B;**[!UICONTROL AmazonS3]**&#x200B;连接，必须提供访问密钥ID和秘密访问密钥。
- 对于具有密码&#x200B;]**连接的**[!UICONTROL  SFTP，必须提供域、端口、用户名和密码。
- 对于具有SSH密钥&#x200B;]**连接的**[!UICONTROL  SFTP，必须提供域、端口、用户名和SSH密钥。
- 对于&#x200B;**[!UICONTROL Azure Blob]**&#x200B;连接，必须提供连接字符串。

或者，您可以附加RSA格式的公钥，以在&#x200B;**[!UICONTROL 密钥]**&#x200B;部分下为导出的文件添加PGP/GPG加密。 请注意，此公钥&#x200B;**必须**&#x200B;写成Base64编码字符串。

![填写活动信息](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

在&#x200B;**[!UICONTROL 基本信息]**&#x200B;中，填写目标的相关信息，如下所示：
- **[!UICONTROL 名称]**:为目标选择相关名称。
- **[!UICONTROL 描述]**:输入目标的说明。
- **[!UICONTROL 存储段名称]**: *对于S3连接*。输入S3存储段的位置，平台会将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL 文件夹路径]**:在您的存储位置提供路径，平台会将导出数据存储为CSV或制表符分隔的文件。
- **[!UICONTROL 容器]**: *用于Blob连接*。包含文件夹路径的Blob的容器。
- **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。

![活动基本信息](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

填写上面的字段后，单击&#x200B;**[!UICONTROL 创建]**。 目标现已连接，您可以[将区段](../../ui/activate-destinations.md)激活到目标。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 目标属性{#destination-attributes}

当[将区段](../../ui/activate-destinations.md)激活到Adobe Campaign目标时，建议您从[合并模式](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参阅电子邮件营销目标文档中的[选择要用作导出文件中的目标属性的模式字段](./overview.md#destination-attributes)。

## 导出的数据{#exported-data}

对于[!DNL Adobe Campaign]目标，平台会在您提供的存储位置创建制表符分隔的`.txt`或`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 将数据导入Adobe Campaign{#import-data-into-campaign}

>[!IMPORTANT]
>
>- 执行此集成时，请记住SFTP存储限制、存储限制和有效用户档案限制，这些限制均符合您的Adobe Campaign合同。
>- 您需要使用[!DNL Campaign]计划在Adobe Campaign中工作流、导入和映射导出的区段。 请参阅Adobe Campaign文档中的[设置重复导入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows)。



将平台连接到[!DNL Amazon S3]或SFTP存储后，必须设置从存储位置导入到Adobe Campaign的数据。 要了解如何实现此操作，请参阅Adobe Campaign文档中的[导入数据](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html)。