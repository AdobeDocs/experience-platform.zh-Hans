---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是一款以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
seo-description: Salesforce Marketing Cloud是一款以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## 概述

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是一款以前称为ExactTarget的数字营销套件，它允许您为访客和客户构建和自定义旅程，以个性化其体验。

要将区段数据发 [!DNL Salesforce Marketing Cloud]送到，您必 [须先在Adobe Real](#connect-destination) -time CDP中连接目标，然后 [将存储位置的数据导入](#import-data-into-salesforce) 设置到中 [!DNL Salesforce Marketing Cloud]。

## 连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接”>“目标]**”中， [!DNL Salesforce Marketing Cloud]选择，然后选 **[!UICONTROL 择“连接目标”]**。

   ![连接到Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. 在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接之一。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 对于 [!DNL Salesforce Marketing Cloud]，您可以在带密 **[!UICONTROL 码的SFTP和]****[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型填写以下信息，然后选择“连 **[!UICONTROL 接到目标”]**。

   对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

   ![填写Salesforce信息](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. 在设 **[!UICONTROL 置步]** 骤中，填写目标的相关信息，如下所示：
   * **[!UICONTROL 名称]**: 为目标选择相关名称。
   * **[!UICONTROL 描述]**: 输入目标的说明。
   * **[!UICONTROL 文件夹路径]**: 在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件格式]**: **[!UICONTROL CSV]** 或 **[!UICONTROL TAB_DELIMITED]**。 选择要导出到存储位置的文件格式。

   ![Salesforce基本信息](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. 填写 **[!UICONTROL 上述字段]** 后，单击创建目标。 您的目标现已连接，您可 [以将区段](/help/rtcdp/destinations/activate-destinations.md) 激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](/help/rtcdp/destinations/activate-destinations.md) 活到目 [!DNL Salesforce Marketing Cloud] 标时 [，建议您从合并模式中选择唯一标](../../profile/home.md#profile-fragments-and-union-schemas)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 的模式字段。

## 将数据导入设置为 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

在将实时CDP连接到Amazon S3或SFTP存储后，您必须设置从存储位置导入到的数据 [!DNL Salesforce Marketing Cloud]。 要了解如何完成此操作，请参 [阅中的将订阅者从文件导入](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) Marketing Cloud [!DNL Salesforce Help Center]。