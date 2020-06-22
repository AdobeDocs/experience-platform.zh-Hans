---
title: 电子邮件营销目标
seo-title: 电子邮件营销目标
description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，如发送促销电子邮件活动。
seo-description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，如发送促销电子邮件活动。
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---


# 电子邮件营销目标 {#email-marketing-destinations}

电子邮件服务提供商(ESP)使您能够管理电子邮件营销活动，如发送促销电子邮件活动。 Adobe实时客户数据Platform允许您将细分激活到电子邮件营销目标，从而与ESP集成。

要向活动的电子邮件营销目标发送区段，Adobe实时CDP必须首先连接到目标。

连接到电子邮件营销目标的过程分为三步。 本页将进一步介绍每个步骤。

在连接目标流中（如以下部分所述），连接到Amazon S3或SFTP。 实时CDP将您的细分作为或文 `.csv` 件导 `.txt` 出，并将它们提供给您的首选位置。 计划您在电子邮件营销平台中从实时CDP中启用的存储位置导入数据。 导入数据的过程因每个合作伙伴而异。 有关详细信息，请参阅各个目标文章。

## 第1步——连接目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接”>]**“目标”中，选择要连接的电子邮件营销目标，然后选择“连 **[!UICONTROL 接目标”]**。

   ![连接到目标](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. 在“身 **[!UICONTROL 份验证]** ”步骤中，如果您之前已设置到电子邮件营销目标的连接，请选择“现 **[!UICONTROL 有帐户]** ”，然后选择您的现有连接。 或者，您也可以选 **[!UICONTROL 择“新帐户]** ”来设置到电子邮件营销目标的新连接。 在连接 **[!UICONTROL 类型]** 选择器中，您可以在Amazon S3 **、带口**&#x200B;令的SFTP、 **带** SSH密钥的 **** SFTP之间进行选择。 根据连接类型，填写以下信息，然后选择“ **[!UICONTROL Connect]**”。

   对 **于S3连接**，您必须提供Amazon访问密钥ID和秘密访问密钥。

   对 **于带口令的SFTP** ，您必须为SFTP服务器提供域、端口、用户名和密码。

   对于 **具有SSH密钥连接** 的SFTP，您必须为SFTP服务器提供域、端口、用户名和密码。

3. 在设 **[!UICONTROL 置步]** 骤中，输入新目 **[!UICONTROL 标的名称]** 、说 **[!UICONTROL 明，以及导出]****** 文件的文件格式说明。 <br>
如果您在上一步中选择了Amazon S3作为存储选项，请在云 **[!UICONTROL 存储目标中]** ，插 **[!UICONTROL 入存储段名]** 称和文件夹路径，将文件传送到该目标中。 对于SFTP存储选项，插入 **[!UICONTROL 文件传送]** “文件夹”路径。 <br>
此外，在此步骤中，您还可以选 **[!UICONTROL 择应用于此目标]** 的任何Marketing用例。 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关Adobe定义的个别营销用例的信息，请参阅数 [据使用策略概述](/help/data-governance/policies/overview.md#core-actions)。 <br>
   ![电子邮件设置步骤](/help/rtcdp/destinations/assets/email-setup-step.png)

## 第2步——选择要包括在目标导出中的区段成员 {#select-segments}

在“选 **[!UICONTROL 择区段]** ”页面上，选择要发送到目标的区段。 在以下各节中查找有关字段的更多信息。

![选择区段](/help/rtcdp/destinations/assets/email-select-segments.png)

## 第3步——选择要在导出的文件中用作目标属性的模式字段 {#destination-attributes}

在此步骤中，您将选择要导出到电子邮件营销目标的字段。

![目标属性](/help/rtcdp/destinations/assets/destination-attributes.png)

### 身份 {#identity}

我们建议您从合并模式中选择唯一标 [识符](../../profile/home.md#profile-fragments-and-union-schemas)。 这是用户身份被锁定的字段。 最常用的字段是电子邮件地址，但也可以是忠诚度项目ID或电话号码。 请参阅下表，了解合并模式中最常见的唯一标识符及其XDM字段。

| 唯一标识符 | 统一模式中的XDM字段 |
---------|----------
| 电子邮件地址 | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| 忠诚度项目ID | `Customer-defined XDM field` |

### 其他目标属性

在模式字段选择器中，选择要导出到电子邮件目标的其他字段。 推荐的选项有：

| 架构 | XDM字段 |
---------|----------
| 名字 | `person.name.firstName` |
| 姓氏 | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址状态 | `homeAddress.stateProvince` |
| 地址邮政编码 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |

## 第3步——将数据从存储位置导入目标

请参阅单个电子邮件营销目标文章，了解如何将数据从存储位置导入目标：

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Evolca](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## 将区段激活到电子邮件营销目标

有关如何将区段激活到电子邮件营销目标的说明，请参 [阅将数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。