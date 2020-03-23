---
title: Oracle Responsys目标
seo-title: Oracle Responsys目标
description: Responsys是一款企业电子邮件营销工具，用于Oracle提供的跨渠道营销活动，用于在电子邮件、移动设备、展示广告和社交渠道之间实现个性化互动。
seo-description: Responsys是一款企业电子邮件营销工具，用于Oracle提供的跨渠道营销活动，用于在电子邮件、移动设备、展示广告和社交渠道之间实现个性化互动。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是Oracle为跨渠道营销活动提供的企业电子邮件营销工具，用于在电子邮件、移动设备、展示广告和社交渠道中实现个性化互动。

要向Oracle Responsys发送区段数据，您必须先在Adobe Real- [time Customer Data Platform中连接目标](#connect-destination) ，然后设置从存储位置到Oracle Responsys的 [数据导入](#import-data-into-responsys) 。

## 连接目标 {#connect-destination}

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Oracle Responsys，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. 在Connect目标向导中，选择存储 **[!UICONTROL Connection type]** 位置对应的。 对于Oracle Responsys，您可以在 **SFTP with Password** （口令）和 **SFTP with SSH Key（SSH密钥）之间进行选择**。 根据连接类型，填写以下信息，然后选择 **[!UICONTROL Connect]**。

   ![设置Responsys向导](/help/rtcdp/destinations/assets/responsys-wizard.png)

   对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP(带有SSH密钥连接** )，您必须提供域、端口、用户名和SSH密钥。

   ![填写Responsys信息](/help/rtcdp/destinations/assets/responsys-step2.png)

1. 在“ **基本信息**”中，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **文件夹路径**:在您的存储位置提供路径，实时CDP会将您的导出数据作为CSV或制表符分隔的文件存放。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![Responsys基本信息](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. 在“基 **本信息** ”中填写字段后，单 **击创建**。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Responsys目标时，建议您从联合架构中选择唯一 [标识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的架构](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 字段。

## 设置Oracle Responsys的数据导入 {#import-data-into-responsys}

在将实时CDP连接到Amazon S3或SFTP存储之后，您必须设置从存储位置到Oracle Responsys的数据导入。 要了解如何完成此操作，请参 [阅在Oracle Responsys帮助中心导入联系人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 或帐户。