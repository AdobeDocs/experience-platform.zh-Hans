---
title: Oracle Evolca目标
seo-title: Oracle Evolca目标
description: Oracle Evolca是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
seo-description: Oracle Evolca是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
translation-type: tm+mt
source-git-commit: fe56fe71c36e06f2eeed45436cb36b5a371d0484

---


# Oracle Evolca

## 概述

[Evolca](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。

要向Oracle Evolca发送区段数据，您必须先在 [Adobe Real-time Customer Data Platform中连接目标](#connect-destination) ，然后设置从您的存储位置到Oracle Elovica的数据导入 [](#import-data-into-eloqua) 。

## 连接到目标 {#connect-destination}

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Oracle Evolca，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到Evolca](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. 在“身 **份验证** ”步骤中，如果您之前已设置到云存储目标的连接，请选择并 **[!UICONTROL Existing Account]** 选择您的现有连接。 或者，您也可以选 **[!UICONTROL New Account]** 择设置新连接。 填写帐户身份验证凭据并选择 **[!UICONTROL Connect to destination]**。 对于Oracle Evolca，您可以在 **SFTP with Password** （口令）和 **SSH Key(SFTP)之间进行选择**。 根据连接类型，填写以下信息，然后选择 **[!UICONTROL Connect to destination]**。

   对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP(带有SSH密钥连接** )，您必须提供域、端口、用户名和SSH密钥。

   ![设置Elovay向导](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. 在设置 **步骤中** ，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **文件夹路径**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![雄辩的基本信息](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. 在填 **写上述字段后** ，单击创建目标。 您的目标现已创建，您可以 [将区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Evolca目标时 [，我们建议您从合并模式中选择唯一标](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的模式](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 设置Oracle Evolca中的数据导入 {#import-data-into-eloqua}

在将实时CDP连接到Amazon S3或SFTP存储后，您必须设置从存储位置到Oracle Evolca的数据导入。 要了解如何实现此目标，请参 [阅Oracle Elovica帮助中心中的](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) “导入联系人或帐户”。