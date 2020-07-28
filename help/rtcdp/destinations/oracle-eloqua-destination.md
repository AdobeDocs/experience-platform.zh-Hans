---
title: Oracle Evolca目标
seo-title: Oracle Evolca目标
description: Oracle Elova是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
seo-description: Oracle Elova是Oracle提供的一个软件即服务(SaaS)平台，用于实现营销自动化，旨在帮助B2B营销人员和组织管理营销活动和销售线索生成。
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## 概述

[Eloca](https://www.oracle.com/marketingcloud/products/marketing-automation/) 是一个软件即服务(SaaS)平台，旨在实现B2B营销人员和组织对营销活动和销售线索生成的 [!DNL Oracle] 管理，并提供营销自动化。

要将区段数据发 [!DNL Oracle Eloqua]送到，您必 [须先在Adobe实时平台中](#connect-destination) 连接目标 [，然后设置从存储位置](#import-data-into-eloqua) 导入到的中 [!DNL Oracle Eloqua]。

## 连接到目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接”>“目标]**”中， [!DNL Oracle Eloqua]选择，然后选 **[!UICONTROL 择“连接目标”]**。

   ![连接到Elovica](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. 在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接之一。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 对于 [!DNL Oracle Eloqua]，您可以在带密 **[!UICONTROL 码的SFTP和]****[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型填写以下信息，然后选择“连 **[!UICONTROL 接到目标”]**。

   对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

   ![设置Elova向导](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. 在设 **[!UICONTROL 置步]** 骤中，填写目标的相关信息，如下所示：
   * **[!UICONTROL 名称]**: 为目标选择相关名称。
   * **[!UICONTROL 描述]**: 输入目标的说明。
   * **[!UICONTROL 文件夹路径]**: 在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。

   ![雄辩基本信息](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. 填写 **[!UICONTROL 上述字段]** 后，单击创建目标。 您的目标现已创建完毕，您 [可以将区段](/help/rtcdp/destinations/activate-destinations.md) 激活到目标。

## 目标属性

在将 [区段激](/help/rtcdp/destinations/activate-destinations.md) 活到目 [!DNL Oracle Eloqua] 标时 [，建议您从合并模式中选择唯一标](../../profile/home.md#profile-fragments-and-union-schemas)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 的模式字段。

## 将数据导入设置为 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

在将实时CDP连接到您的AmazonS3或SFTP存储后，您必须设置从存储位置导入到的数据 [!DNL Oracle Eloqua]。 要了解如何完成此操作，请参阅 [中的导入联系人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 或帐户 [!DNL Oracle Eloqua Help Center]。