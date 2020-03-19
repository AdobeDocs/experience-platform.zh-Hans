---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解决方案，可帮助您跨所有线上和线下渠道个性化和投放营销活动。
seo-description: Adobe Campaign是一套解决方案，可帮助您跨所有线上和线下渠道个性化和投放营销活动。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解决方案，可帮助您跨所有线上和线下渠道个性化和投放营销活动。 有关 [详细信息，请参阅](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) “关于Adobe Campaign Classic”。

要向Adobe Campaign发送细分数据，您必须先在 [Adobe实时客户数据平台中连接目标](#connect-destination) ，然后设置从存储 [](#import-data-into-campaign) 位置导入到Adobe Campaign的数据。

## 连接目标 {#connect-destination}

1. 在“连 **[!UICONTROL 接”>“目标]**”中，选择“Adobe Campaign”，然后选择“ **[!UICONTROL Connect目标”]**。

   ![连接到Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在连接目标向导中，选择存储 **[!UICONTROL 位置的连接类型]** 。 对于Adobe Campaign，您可以在 **Amazon S3**、 **SFTP with Password** 和 **SSH Key之间进行选择**。 根据连接类型，填写以下信息，然后选择“连 **[!UICONTROL 接”]**。

   ![设置营销活动向导](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   对于 **S3连接** ，您必须提供访问密钥ID和机密访问密钥。
对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP与SSH密钥连接** ，您必须提供域、端口、用户名和SSH密钥。

   ![填写营销活动信息](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在“ **基本信息**”中，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **存储段名称**:对 *于S3连接*。 输入S3存储段的位置，实时CDP会将导出数据作为CSV或制表符分隔的文件存放。
   * **文件夹路径**:在您的存储位置提供路径，实时CDP会将您的导出数据作为CSV或制表符分隔的文件存放。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![营销活动基本信息](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 在“基 **本信息** ”中填写字段后，单 **击创建**。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Adobe Campaign目标时，建议您从联合架构中选择唯一 [标识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的架构](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 字段。


## 设置Adobe Campaign中的数据导入 {#import-data-into-campaign}

在将实时CDP连接到Amazon S3或SFTP存储之后，您必须设置从存储位置到Adobe Campaign的数据导入。 要了解如何完成此操作，请参阅 [Adobe Campaign帮助文档](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 中的导入数据。