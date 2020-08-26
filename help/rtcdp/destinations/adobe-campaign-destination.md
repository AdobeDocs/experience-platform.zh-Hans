---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
seo-description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
translation-type: tm+mt
source-git-commit: 4c45da353b1deeb66b0dedb37450158f4bdc2a7c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。 请参 [阅关于Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) ，以了解更多信息。

要向Adobe Campaign发送细分数据，您必须先 [在Adobe实时平台](#connect-destination) ，然后设置从您的 [存储位置导入到Adobe Campaign的数据](#import-data-into-campaign) 。

## 连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接]** ”>“目 **[!UICONTROL 标”中]**，选择“Adobe Campaign”，然 **[!UICONTROL 后选择Connect目标]**。

   ![连接到adobe活动](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在Connect目标工作流中，选择 **[!UICONTROL 存储位置]** 的连接类型。 对于Adobe Campaign，您可以在 **[!UICONTROL AmazonS3]**、 **[!UICONTROL 带口令的SFTP]** 和 **[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型，填写以下信息，然后选择“ **[!UICONTROL Connect]**”。

   ![设置活动向导](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   对 **[!UICONTROL 于AmazonS]** 3连接，您必须提供访问密钥ID和秘密访问密钥。
对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

   ![填写活动信息](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在“ **[!UICONTROL 基本信息]**”中，填写目标的相关信息，如下所示：
   * **[!UICONTROL 名称]**:为目标选择相关名称。
   * **[!UICONTROL 描述]**:输入目标的说明。
   * **[!UICONTROL 存储段名称]**: *对于S3连接*。 输入S3存储段的位置，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件夹路径]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。

   ![活动基本信息](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 填写 **[!UICONTROL 上述字]** 段后，单击“创建”。 您的目标现已连接，您可 [以将区段](/help/rtcdp/destinations/activate-destinations.md) 激活到目标。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](/help/rtcdp/destinations/activate-destinations.md) 活到Adobe Campaign目标时 [，建议您从合并模式中选择唯一](../../profile/home.md#profile-fragments-and-union-schemas)标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅在电子邮件营销目标文档中选择要用作导出文件中目标属性](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 的模式字段。

## 导出的数据 {#exported-data}

对 [!DNL Adobe Campaign] 于目标，Adobe实时CDP会在您提供的存储位置创建制 `.txt` 表符 `.csv` 分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 将数据导入设置为Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 执行此集成时，请记住SFTP存储限制、存储限制和有效用户档案限制，这些限制均符合您的Adobe Campaign合同。
>* 您需要使用计划工作流、导入和映射Adobe Campaign中导出的区 [!DNL Campaign] 段。 请参阅 [Adobe Campaign文档中的设置](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#setting-up-a-recurring-import) 经常性导入。



在将实时CDP连接到您的 [!DNL Amazon S3] 存储或SFTP后，您必须设置从存储位置导入到Adobe Campaign的数据。 要了解如何完成此操作，请参阅 [Adobe Campaign文档](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 中的导入数据。