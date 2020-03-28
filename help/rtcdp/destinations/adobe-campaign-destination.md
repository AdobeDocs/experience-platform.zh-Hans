---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和交付活动。
seo-description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和交付活动。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和交付活动。 有关 [详细信息](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) ，请参阅关于Adobe Campaign经典。

要向Adobe Campaign发送细分数据，您必须先在 [Adobe实时客户数据平台中连接目标](#connect-destination) ，然后设置从您的存储位置向Adobe Campaign导入的数据 [](#import-data-into-campaign) 。

## 连接目标 {#connect-destination}

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Adobe Campaign，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到Adobe活动](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在Connect目标工作流中，选择 **[!UICONTROL Connection type]** 存储位置。 对于Adobe Campaign，您可以在和之 **[!UICONTROL Amazon S3]**&#x200B;间 **[!UICONTROL SFTP with Password]** 进行选 **[!UICONTROL SFTP with SSH Key]**&#x200B;择。 根据连接类型，填写以下信息，然后选择 **[!UICONTROL Connect]**。

   ![设置活动向导](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   对于 **[!UICONTROL Amazon S3]** 连接，您必须提供访问密钥ID和机密访问密钥。
对于 **[!UICONTROL SFTP with Password]** 连接，必须提供域、端口、用户名和密码。
对于 **[!UICONTROL SFTP with SSH Key]** 连接，必须提供域、端口、用户名和SSH密钥。

   ![填写活动信息](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在 **[!UICONTROL Basic Information]**&#x200B;中，填写目标的相关信息，如下所示：
   * **[!UICONTROL Name]**:为目标选择相关名称。
   * **[!UICONTROL Description]**:输入目标的说明。
   * **[!UICONTROL Bucket Name]**:对 *于S3连接*。 输入S3存储段的位置，实时CDP会将导出数据作为CSV或制表符分隔的文件存放。
   * **[!UICONTROL Folder Path]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL File Format]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![活动基本信息](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 填写 **[!UICONTROL Create]** 上述字段后单击。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到Adobe Campaign目标](/help/rtcdp/destinations/activate-destinations.md) ，建议您从合并模式中选择唯一标 [识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的模式](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。


## 将数据导入设置为Adobe Campaign {#import-data-into-campaign}

将实时CDP连接到Amazon S3或SFTP存储后，您必须设置从存储位置到Adobe Campaign的数据导入。 要了解如何完成此操作，请参阅 [Adobe Campaign帮助文档](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 中的导入数据。