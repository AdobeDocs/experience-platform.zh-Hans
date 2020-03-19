---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
seo-description: Salesforce Marketing Cloud是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## 概述

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一个以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。

要将区段数据发送到Salesforce Marketing Cloud，您必须首先在 [Adobe实时CDP中连接目标](#connect-destination) ，然后设置从存储 [位置将数据导入](#import-data-into-salesforce) Salesforce Marketing Cloud。

## 连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择Salesforce Marketing Cloud，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. 在连接目标向导中，选择存储 **[!UICONTROL 位置的连接类型]** 。 对于Salesforce Marketing Cloud，您可以在 **SFTP（带口令）和** SSH **FTP（带SSH密钥）之间进行选择**。 根据连接类型，填写以下信息，然后选择“连 **[!UICONTROL 接”]**。

   ![设置Salesforce向导](/help/rtcdp/destinations/assets/salesforce-step1.png)

   对于 **SFTP(带密码连接** )，您必须提供域、端口、用户名和密码。
对于 **SFTP与SSH密钥连接** ，您必须提供域、端口、用户名和SSH密钥。

   ![填写Salesforce信息](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. 在“ **基本信息**”中，填写目标的相关信息，如下所示：
   * **名称**:为目标选择相关名称。
   * **说明**:输入目标的说明。
   * **文件夹路径**:在您的存储位置提供路径，实时CDP会将您的导出数据作为CSV或制表符分隔的文件存放。
   * **文件格式**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。
   ![Salesforce基本信息](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. 在“基 **本信息** ”中填写字段后，单 **击创建**。 您的目标现已连接，您可以将 [区段激活](/help/rtcdp/destinations/activate-destinations.md) 到目标。

## 目标属性 {#destination-attributes}

将区 [段激活到](/help/rtcdp/destinations/activate-destinations.md) Salesforce Marketing Cloud目标时，建议您从联合架构中选择唯一 [标识符](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中导出的文件中用作目标属性的架构](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 字段。

## 设置数据导入到Salesforce Marketing Cloud {#import-data-into-salesforce}

在将实时CDP连接到Amazon S3或SFTP存储之后，您必须设置从存储位置到Salesforce Marketing Cloud的数据导入。 要了解如何实现此目标，请参 [阅将订阅者从Salesforce帮助中心的文件导入](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) Marketing Cloud。