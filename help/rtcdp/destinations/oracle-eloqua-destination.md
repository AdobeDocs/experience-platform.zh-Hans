---
title: Oracle Evolca目标
seo-title: Oracle Evolca目标
description: Oracle Evolca是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
seo-description: Oracle Evolca是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Evolca

## 概述

[Evolca](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

要向Oracle Evolca发送区段数据，您必须先在 [Adobe Real-time Customer Data Platform中连接目标](#connect-destination) ，然后设置从存储位置到Oracle Elovica的数据导入 [](#import-data-into-eloqua) 。

## 连接到目标 {#connect-destination}

1. 在“连 **[!UICONTROL 接”>“目标]**”中，选择Oracle Evolca，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到Evolca](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. 在连接目标向导中，选择存储 **[!UICONTROL 位置的连接类型]** 。 对于Oracle Evolca，您可以在 **SFTP with Password** （口令）和 **SSH Key(SFTP)之间进行选择**。 根据连接类型，填写以下信息，然后选择“连 **[!UICONTROL 接”]**。

   ![设置Elovay向导](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP与SSH密钥连接** ，您必须提供域、端口、用户名和SSH密钥。

   ![填写Exola信息](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. 在“ **基本信息**”中，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **文件夹路径**:在您的存储位置提供路径，实时CDP会将您的导出数据作为CSV或制表符分隔的文件存放。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![雄辩的基本信息](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. 在“基 **本信息** ”中填写字段后，单 **击创建**。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Evolca目标时，我们建议您从联合架构中选择唯一 [标识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的架构](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 字段。

## 设置Oracle Evolca中的数据导入 {#import-data-into-eloqua}

在将实时CDP连接到Amazon S3或SFTP存储之后，您必须设置从存储位置到Oracle Evolca的数据导入。 要了解如何实现此目标，请参 [阅Oracle Elovica帮助中心中的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) “导入联系人或帐户”。