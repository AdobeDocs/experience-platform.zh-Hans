---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
seo-description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道中个性化和投放活动。 有关 [更多信息](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) ，请参阅关于Adobe Campaign经典。

要向Adobe Campaign发送细分数据，您必 [须先在Adobe](#connect-destination) Real-time Customer Data Platform中连接目标，然 [后设置从存储位置导入到](#import-data-into-campaign) Adobe Campaign的数据。

## 连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Adobe Campaign”，然 **[!UICONTROL 后选择Connect目标]**。

   ![连接到adobe活动](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在Connect目标工作流中，选择 **[!UICONTROL 存储位置]** 的连接类型。 对于Adobe Campaign，您可以在Amazon **[!UICONTROL S3]**、 **[!UICONTROL SFTP（带口令）和]** SFTP( **[!UICONTROL 带SSH密钥)之间进行选择]**。 根据连接类型，填写以下信息，然后选择“ **[!UICONTROL Connect]**”。

   ![设置活动向导](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   对 **[!UICONTROL 于Amazon S3]** 连接，您必须提供访问密钥ID和秘密访问密钥。
对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

   ![填写活动信息](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在“ **[!UICONTROL 基本信息]**”中，填写目标的相关信息，如下所示：
   * **[!UICONTROL 名称]**: 为目标选择相关名称。
   * **[!UICONTROL 描述]**: 输入目标的说明。
   * **[!UICONTROL 存储段名称]**: *对于S3连接*。 输入S3存储段的位置，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件夹路径]**: 在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。

   ![活动基本信息](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 填写 **[!UICONTROL 上述字]** 段后，单击“创建”。 您的目标现已连接，您可 [以将区段](/help/rtcdp/destinations/activate-destinations.md) 激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](/help/rtcdp/destinations/activate-destinations.md) 活到Adobe Campaign目标时 [，建议您从合并模式中选择唯一](../../profile/home.md#profile-fragments-and-union-schemas)标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 的模式字段。


## 将数据导入设置为Adobe Campaign {#import-data-into-campaign}

在将实时CDP连接到您的 [!DNL Amazon S3] 存储或SFTP后，您必须设置从存储位置导入到Adobe Campaign的数据。 要了解如何完成此操作，请参阅 [Adobe Campaign帮助](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 文档中的导入数据。