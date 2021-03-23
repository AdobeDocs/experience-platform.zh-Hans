---
keywords: 电子邮件；电子邮件；电子邮件目标
title: 电子邮件营销目标概述
type: 教程
description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，例如发送促销电子邮件活动。
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# 电子邮件营销目标概述{#email-marketing-destinations}

电子邮件服务提供商(ESP)使您能够管理电子邮件营销活动，如发送促销电子邮件活动。 Adobe Experience Platform通过允许您将区段激活到电子邮件营销目标，与ESP集成。

要向活动的电子邮件营销目标发送区段，平台必须首先连接到目标。

连接到电子邮件营销目标是一个三步过程([配置目标](#connect-destination)、[激活区段](#select-segments)、[将存储位置的数据导入目标](#import-data-into-destination))。 本页将进一步介绍每个步骤。

在连接目标流中（如以下部分所述），连接到Amazon S3或SFTP。 Platform将您的区段导出为`.csv`或`.txt`文件，并将它们发送到您的首选位置。 计划从平台中启用的存储位置导入电子邮件营销平台中的数据。 导入数据的过程因每个合作伙伴而异。 有关详细信息，请阅读各个目标文章。

## 配置目标{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择要连接的电子邮件营销目标，然后选择&#x200B;**[!UICONTROL Configure]**。

![连接到目标](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

在&#x200B;**[!UICONTROL Account]**&#x200B;步骤中，如果您之前已设置到电子邮件营销目标的连接，请选择&#x200B;**[!UICONTROL Existing Account]**&#x200B;并选择现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL New Account]**&#x200B;来设置到电子邮件营销目标的新连接。 在&#x200B;**[!UICONTROL Connection type]**&#x200B;选择器中，您可以在[!UICONTROL Amazon S3]、[!UICONTROL Azure Blob]、[!UICONTROL SFTP with Password]或[!UICONTROL SFTP with SSH Key]之间进行选择。 根据连接类型，填写以下信息，然后选择&#x200B;**[!UICONTROL Connect]**。

- 对于&#x200B;**S3连接**，必须提供Amazon访问密钥ID和密钥访问密钥。
- 对于&#x200B;**具有Password**&#x200B;连接的SFTP，您必须为SFTP服务器提供域、端口、用户名和密码。
- 对于具有SSH密钥&#x200B;**连接的** SFTP，必须为SFTP服务器提供域、端口、用户名和密码。

或者，您也可以附加RSA格式的公钥，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下为导出的文件添加加密。 您的公钥必须写入为[!DNL Base64]编码字符串。

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，输入新目标的名称和说明以及导出文件的文件格式。

如果您在上一步中选择了Amazon S3作为存储选项，请在云存储目标中插入存储段名称和文件夹路径，以便将文件传送到该目标。 对于SFTP存储选项，插入要传送文件的文件夹路径。

在此步骤中，您还可以选择应用于此目标的任何营销活动。 营销活动指示要将数据导出到目标的目的。 您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请阅读[数据使用策略概述](../../../data-governance/policies/overview.md)。

![电子邮件设置步骤](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## 选择要包含在目标导出中的区段成员{#select-segments}

在&#x200B;**[!UICONTROL Select Segments]**&#x200B;页面上，选择要发送到目标的区段。 有关以下部分中字段的更多信息。

![选择区段](../../assets/common/email-select-segments.png)

## 配置文件名

有关区段计划和文件名编辑选项的信息，请参阅激活目标教程中的[配置](../../ui/activate-destinations.md#configure)步骤。

## 选择属性 — 选择要用作导出文件{#destination-attributes}中的目标属性的模式字段

在此步骤中，您将选择要导出到电子邮件营销目标的字段，并标记哪些字段为必填字段。
有关此步骤的信息，请参阅激活目标教程中的[选择属性](../../ui/activate-destinations.md#select-attributes)步骤。

## 身份{#identity}

Adobe建议您从[合并模式](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 这是您的用户身份被抠离的字段。 最常用的字段是电子邮件地址，但也可以是忠诚度项目ID或电话号码。 请参阅下表，了解该模式中最常见的唯一标识符及其XDM字段。

| 唯一标识符 | 统一模式中的XDM字段 |
----------------- | ---------------------------
| Email Address | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| 忠诚度项目ID | `Customer-defined XDM field` |

## 其他目标属性

在“模式”字段选择器中，选择要导出到电子邮件目标的其他字段。 推荐的选项有：

| 架构 | XDM字段 |
------ | ---------
| 名字 | `person.name.firstName` |
| 姓氏 | `person.name.lastName` |
| 电话 | `mobilePhone.number` |
| 地址城 | `homeAddress.city` |
| 地址状态 | `homeAddress.stateProvince` |
| 地址邮政编码 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 细分会员资格 | `segmentMembership.status` |

## 将数据从存储位置导入目标{#import-data-into-destination}

阅读各个电子邮件营销目标文章，了解如何将存储位置的数据导入目标：

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Evola](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [SalesforceMarketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## 将区段激活到电子邮件营销目标

有关如何将区段激活到电子邮件营销目标的说明，请参阅[将用户档案和区段激活到目标](../../ui/activate-destinations.md)。

## Journey Orchestration

- [将数据激活到目标](../../ui/activate-destinations.md)
- [使用流服务API创建电子邮件营销目标并激活数据](../../api/email-marketing.md)