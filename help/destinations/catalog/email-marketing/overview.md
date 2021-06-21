---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标
title: 电子邮件营销目标概述
type: Tutorial
description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，例如发送促销电子邮件活动。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 电子邮件营销目标概述{#email-marketing-destinations}

电子邮件服务提供商(ESP)使您能够管理电子邮件营销活动，如发送促销电子邮件活动。 Adobe Experience Platform通过允许您将区段激活到电子邮件营销目标来与ESP集成。

要将区段发送到营销活动的电子邮件营销目标，Platform必须先连接到该目标。

连接到电子邮件营销目标是一个三步流程（[配置目标](#connect-destination)、[激活区段](#select-segments)、[将数据从存储位置导入目标](#import-data-into-destination)）。 下文将在本页中进一步介绍每个步骤。

在连接目标流（如以下部分所述）中，连接到[!DNL Amazon S3]或[!DNL SFTP]。 Platform将区段导出为`.csv`文件，并将它们传送到您的首选位置。 从[!DNL Platform]中启用的存储位置计划在电子邮件营销平台中的数据导入。 每个合作伙伴的数据导入流程各不相同。 有关更多信息，请阅读各个目标文章。

## 配置目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择要连接的电子邮件营销目标，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接到目标](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

在&#x200B;**[!UICONTROL 帐户]**&#x200B;步骤中，如果您之前已设置与电子邮件营销目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]** ，然后选择您的现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL 新帐户]**&#x200B;以设置到电子邮件营销目标的新连接。 在&#x200B;**[!UICONTROL 连接类型]**&#x200B;选择器中，您可以在[!UICONTROL Amazon S3]、[!UICONTROL Azure Blob]、[!UICONTROL 带密码的SFTP]或[!UICONTROL 带SSH密钥的SFTP]之间进行选择。 根据您的连接类型填写以下信息，然后选择&#x200B;**[!UICONTROL 连接]**。

- 对于&#x200B;**S3连接**，必须提供Amazon访问密钥ID和密钥访问密钥。
- 对于&#x200B;**带密码的SFTP**&#x200B;连接，必须为SFTP服务器提供域、端口、用户名和密码。
- 对于&#x200B;**具有SSH密钥的SFTP**&#x200B;连接，必须为SFTP服务器提供域、端口、用户名和SSH密钥。

或者，您也可以附加RSA格式的公钥，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下为导出的文件添加加密。 您的公钥必须写为[!DNL Base64]编码字符串。

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，输入新目标的名称和说明，以及导出文件的文件格式。

如果您在上一步中选择了Amazon S3作为存储选项，请在将要提交文件的云存储目标中插入存储段名称和文件夹路径。 对于SFTP存储选项，插入将要传送文件的文件夹路径。

在此步骤中，您还可以选择应用于此目标的任何营销操作。 营销操作指示将数据导出到目标的意图。 您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请阅读[数据使用策略概述](../../../data-governance/policies/overview.md)。

![电子邮件设置步骤](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## 选择要包含在目标导出中的区段成员{#select-segments}

在&#x200B;**[!UICONTROL 选择区段]**&#x200B;页面上，选择要发送到目标的区段。 有关以下部分中字段的更多信息。

![选择区段](../../assets/common/email-select-segments.png)

## 配置文件名

有关区段计划和文件名编辑选项的信息，请参阅激活目标教程中的[配置](../../ui/activate-destinations.md#configure)步骤。

## 选择属性 — 选择要在导出的文件{#destination-attributes}中用作目标属性的架构字段

在此步骤中，您将选择要导出到电子邮件营销目标的字段，并标记哪些字段是必填字段。
有关此步骤的信息，请参阅激活目标教程中的[选择属性](../../ui/activate-destinations.md#select-attributes)步骤。

## 身份 {#identity}

Adobe建议您从[并集架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 这是您的用户身份已从中键出的字段。 最常见的情况是，此字段是电子邮件地址，但也可以是忠诚度计划ID或电话号码。 有关架构中最常见的唯一标识符及其XDM字段，请参阅下表。

| 唯一标识符 | 统一架构中的XDM字段 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| 忠诚度计划ID | `Customer-defined XDM field` |

## 其他目标属性

在架构字段选择器中，选择要导出到电子邮件目标的其他字段。 一些推荐选项包括：

| 架构 | XDM字段 |
|------ | ---------|
| 名字 | `person.name.firstName` |
| 姓氏 | `person.name.lastName` |
| 电话 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址状态 | `homeAddress.stateProvince` |
| 地址邮政编码 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 区段成员资格 | `segmentMembership.status` |

## 将数据从存储位置导入目标{#import-data-into-destination}

阅读单个电子邮件营销目标文章，了解如何将数据从存储位置导入目标：

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle雄辩](./oracle-eloqua.md#import-data-into-eloqua)
- [OracleResponsys](./oracle-responsys.md#import-data-into-responsys)
- [SalesforceMarketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## 将区段激活到电子邮件营销目标

有关如何将区段激活到电子邮件营销目标的说明，请参阅[将用户档案和区段激活到目标](../../ui/activate-destinations.md)。

## 其他资源

- [将数据激活到目标](../../ui/activate-destinations.md)
- [使用流量服务API创建电子邮件营销目标并激活数据](../../api/email-marketing.md)
