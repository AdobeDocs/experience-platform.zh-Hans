---
title: Oracle Responsys目标
seo-title: Oracle Responsys目标
description: Responsys是面向跨渠道营销活动的企业电子邮件营销工具，Oracle为跨电子邮件、移动设备、展示广告和社交平台提供个性化互动服务。
seo-description: Responsys是面向跨渠道营销活动的企业电子邮件营销工具，Oracle为跨电子邮件、移动设备、展示广告和社交平台提供个性化互动服务。
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Responsys

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是面向跨渠道营销活动的企业电子邮件营销工具，Oracle提供此工具，可跨电子邮件、移动设备、展示广告和社交平台实现个性化互动。

要向Oracle Responsys发送区段数据，您必须先连接 [到Adobe Real](#connect-destination) Time Customer Data Platform中的目标，然后设置从存储位置到Oracle Responsys的数据导入 [](#import-data-into-responsys) 。

## 连接目标 {#connect-destination}

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Oracle Responsys，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. 在“身 **份验证** ”步骤中，如果您之前已设置到云存储目标的连接，请选择并选 **[!UICONTROL Existing Account]** 择一个现有连接。 或者，您也可以选 **[!UICONTROL New Account]** 择设置新连接。 填写帐户身份验证凭据并选择 **[!UICONTROL Connect to destination]**。 对于Oracle Responsys，您可以在 **SFTP with Password** （口令）和 **SFTP with SSH Key（SSH密钥）之间进行选择**。 根据连接类型，填写以下信息，然后选择 **[!UICONTROL Connect to destination]**。

   对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP与SSH密钥连接** ，您必须提供域、端口、用户名和SSH密钥。

   ![填写Responsys信息](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. 在设置 **步骤中** ，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **文件夹路径**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![Responsys基本信息](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. 在填 **写上述字段后** ，单击创建目标。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Oracle Responsys目标时，建议您从合并模式中选择唯一标 [识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的模式](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 设置Oracle Responsys的数据导入 {#import-data-into-responsys}

在将实时CDP连接到Amazon S3或SFTP存储后，您必须设置从存储位置到Oracle Responsys的数据导入。 要了解如何完成此操作，请参 [阅在Oracle Responsys帮助中心导入联系人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 或帐户。