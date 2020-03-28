---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
seo-description: Salesforce Marketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Salesforce Marketing Cloud

## 概述

[Salesforce Marketing Cloud是一款以前称为ExactTarget的数字营销套件](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ，它允许您为访客和客户构建和自定义旅程，以个性化其体验。

要将区段数据发送到Salesforce Marketing Cloud，您必须首先在 [Adobe实时CDP中连接目标](#connect-destination) ，然后设置从您的存储位置导入到Salesforce Marketing Cloud的数据 [](#import-data-into-salesforce) 。

## 连接目标 {#connect-destination}

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Salesforce Marketing Cloud，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. 在该步 **[!UICONTROL Authentication]** 骤中，如果您之前已设置到云存储目标的连接，请选择并选 **[!UICONTROL Existing Account]** 择一个现有连接。 或者，您也可以选 **[!UICONTROL New Account]** 择设置新连接。 填写帐户身份验证凭据并选择 **[!UICONTROL Connect to destination]**。 对于Salesforce Marketing Cloud，您可以在和之间进 **[!UICONTROL SFTP with Password]** 行选 **[!UICONTROL SFTP with SSH Key]**&#x200B;择。 根据连接类型，填写以下信息，然后选择 **[!UICONTROL Connect to destination]**。

   对于 **[!UICONTROL SFTP with Password]** 连接，必须提供域、端口、用户名和密码。
对于 **[!UICONTROL SFTP with SSH Key]** 连接，必须提供域、端口、用户名和SSH密钥。

   ![填写Salesforce信息](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. 在该步 **[!UICONTROL Setup]** 骤中，填写目标的相关信息，如下所示：
   * **[!UICONTROL Name]**:为目标选择相关名称。
   * **[!UICONTROL Description]**:输入目标的说明。
   * **[!UICONTROL Folder Path]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL File Format]**:或 **[!UICONTROL CSV]** 者 **[!UICONTROL TAB_DELIMITED]**。 选择要导出到存储位置的文件格式。
   ![Salesforce基本信息](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. 填写 **[!UICONTROL Create destination]** 上述字段后单击。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Salesforce Marketing Cloud目标时，建议您从合并模式中选择唯一标 [识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的模式](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 设置数据导入到Salesforce Marketing Cloud {#import-data-into-salesforce}

在将实时CDP连接到Amazon S3或SFTP存储后，您必须设置从存储位置导入到Salesforce Marketing Cloud的数据。 要了解如何实现此目标，请参 [阅将订阅者从Salesforce帮助中心的文件导入](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) Marketing Cloud。