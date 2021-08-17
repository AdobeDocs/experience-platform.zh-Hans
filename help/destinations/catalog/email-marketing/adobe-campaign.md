---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；Adobe Campaign;Campaign
title: Adobe Campaign连接
description: Adobe Campaign是一套解决方案，可帮助您在所有在线渠道和离线渠道之间个性化并交付促销活动。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Adobe Campaign连接

## 概述 {#overview}

Adobe Campaign是一套解决方案，可帮助您在所有在线渠道和离线渠道之间个性化并交付促销活动。 有关更多信息，请参阅[Campaign Classic入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)。

要将区段数据发送到Adobe Campaign，您必须先在Adobe Experience Platform中连接目标](#connect-destination)，然后[设置从存储位置将数据导入](#import-data-into-campaign)到Adobe Campaign。[

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在受众激活工作 **[!UICONTROL 流]** 的“选择属 [性”步骤中选择](../../ui/activate-batch-profile-destinations.md#select-attributes)。

## IP地址允许列表 {#allow-list}

通过SFTP存储设置电子邮件营销目标时，Adobe建议您向允许列表添加某些IP范围。

如果需要向允许列表添加AdobeIP，请参阅云存储目标的[IP地址允许列表](../cloud-storage/ip-address-allow-list.md) 。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

Adobe Campaign支持以下连接类型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 带密码的SFTP]**
* **[!UICONTROL 具有SSH密钥的SFTP]**
* **[!UICONTROL Azure Blob]**

向Adobe Campaign发送数据的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL Amazon S3]**&#x200B;连接，必须提供[!UICONTROL 访问密钥ID]和[!UICONTROL 密钥访问密钥]。
* 对于具有密码&#x200B;]**连接的**[!UICONTROL  SFTP，必须提供[!UICONTROL 域]、[!UICONTROL 端口]、[!UICONTROL 用户名]和[!UICONTROL 密码]。
* 对于具有SSH密钥&#x200B;]**连接的**[!UICONTROL  SFTP，必须提供[!UICONTROL 域]、[!UICONTROL 端口]、[!UICONTROL 用户名]和[!UICONTROL SSH密钥]。
* 对于&#x200B;**[!UICONTROL Azure Blob]**&#x200B;连接，必须提供连接字符串。
* 或者，您也可以附加RSA格式的公钥，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下将PGP/GPG加密添加到导出的文件中。 您的公钥必须写为[!DNL Base64]编码字符串。
* **[!UICONTROL 名称]**:为您的目标选择相关名称。
* **[!UICONTROL 描述]**:输入目标的描述。
* **[!UICONTROL 存储段名称]**: *对于S3连接*。输入S3存储段的位置，其中[!DNL Platform]将将导出数据存储为CSV或制表符分隔的文件。
* **[!UICONTROL 文件夹路径]**:在存储位置中提供路径，将 [!DNL Platform] 将导出数据存储为CSV或制表符分隔的文件。
* **[!UICONTROL 容器]**: *对于Blob连接*。包含文件夹路径中的Blob的容器。
* **[!UICONTROL 文件格式]**: **** CSV或 **TAB_DELIMITED**。选择要导出到存储位置的文件格式。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 目标属性 {#destination-attributes}

在将区段激活到此目标时，Adobe建议您从[并集架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关更多信息，请参阅[将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Adobe Campaign]目标， [!DNL Platform]会在您提供的存储位置创建以制表符分隔的`.csv`文件。 有关这些文件的更多信息，请参阅区段激活教程中的[验证区段激活](../../ui/activate-batch-profile-destinations.md#verify) 。

## 设置数据导入Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 在执行此集成时，请记住[!DNL SFTP]存储限制、数据库存储限制和活动配置文件限制(根据您的Adobe Campaign合同)。
>* 您需要使用[!DNL Campaign]工作流在Adobe Campaign中计划、导入和映射导出的区段。 请参阅Adobe Campaign Classic文档中的[设置定期导入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html)和Adobe Campaign Standard文档中的[关于数据管理活动](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html)。
>* 向Adobe Campaign发送数据的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。


将[!DNL Platform]连接到[!DNL Amazon S3]或[!DNL Azure Blob]存储后，必须将数据从存储位置导入Adobe Campaign。 要了解如何完成此操作，请参阅以下Adobe Campaign文档页面：
* [数据导入和导出以](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans) 及数 [据加载（文件）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) (位于Adobe Campaign Classic文档中)。
* [在Adobe Campaign Standard文档中开始使用流程](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和数 [据](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 管理和加载文件。
