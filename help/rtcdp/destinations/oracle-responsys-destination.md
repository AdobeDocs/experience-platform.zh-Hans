---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Oracle Responsys目标
seo-title: Oracle Responsys目标
description: Responsys是面向跨渠道营销活动的企业电子邮件营销工具，由Oracle提供，用于在电子邮件、移动设备、展示广告和社交平台之间实现个性化互动。
seo-description: Responsys是面向跨渠道营销活动的企业电子邮件营销工具，由Oracle提供，用于在电子邮件、移动设备、展示广告和社交平台之间实现个性化互动。
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是面向跨渠道营销活动的企业电子邮件营销工具，可通过 [!DNL Oracle] 在电子邮件、移动设备、展示广告和社交渠道实现个性化互动。

要将区段数据发 [!DNL Oracle Responsys]送到，您必 [须先连接到Adobe实时平台中的目](#connect-destination) 标，然后设置存储位置中的 [导入](#import-data-into-responsys)[!DNL Oracle Responsys]。

## 导出类型 {#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](/help/rtcdp/destinations/activate-destinations.md#select-attributes)。

## 连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Oracle Responsys]，选 **[!UICONTROL 择，然后选择]**“连接目标”。

   ![连接到Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. 在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接之一。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 对于 [!DNL Oracle Responsys]，您可以在带密 **[!UICONTROL 码的SFTP和]****[!UICONTROL 带SSH密钥的SFTP之间进行选择]**。 根据连接类型填写以下信息，然后选择“连 **[!UICONTROL 接到目标”]**。

   对 **[!UICONTROL 于带口令的SFTP]** ，您必须提供域、端口、用户名和密码。
对于 **[!UICONTROL 具有SSH密钥连接]** 的SFTP，您必须提供域、端口、用户名和密码。

   ![填写Responsys信息](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. 在设 **[!UICONTROL 置步]** 骤中，填写目标的相关信息，如下所示：
   * **[!UICONTROL 名称]**:为目标选择相关名称。
   * **[!UICONTROL 描述]**:输入目标的说明。
   * **[!UICONTROL 文件夹路径]**:在存储位置提供路径，实时CDP会将导出数据存储为CSV或制表符分隔的文件。
   * **[!UICONTROL 文件格式]**: **CSV** 或 **TAB_DELIMITED**。 选择要导出到存储位置的文件格式。

   ![Responsys基本信息](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. 填写 **[!UICONTROL 上述字段]** 后，单击创建目标。 您的目标现已连接，您可 [以将区段](/help/rtcdp/destinations/activate-destinations.md) 激活到目标。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。

## 目标属性 {#destination-attributes}

在将 [区段激](/help/rtcdp/destinations/activate-destinations.md) 活到目 [!DNL Oracle Responsys] 标时 [，建议您从合并模式中选择唯一标](../../profile/home.md#profile-fragments-and-union-schemas)识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。 有关详细信息，请参 [阅选择在电子邮件营销目标中的导出文件中用作目标属性](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 的模式字段。

## 导出的数据 {#exported-data}

对 [!DNL Oracle Responsys] 于目标，Adobe实时CDP会在您提供的存储位置创建制 `.txt` 表符 `.csv` 分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Responsys_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 将数据导入设置为 [!DNL Oracle Responsys] {#import-data-into-responsys}

在将实时CDP连接到您的 [!DNL Amazon S3] 或SFTP存储后，您必须设置从存储位置导入到的数据 [!DNL Oracle Responsys]。 要了解如何完成此操作，请参阅 [中的导入联系人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 或帐户 [!DNL Oracle Responsys Help Center]。