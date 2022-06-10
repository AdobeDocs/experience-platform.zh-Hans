---
keywords: SFTP;SFTP
title: SFTP连接
description: 创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 715533352e84573f60f012504988595af6146e2f
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 1%

---

# SFTP连接

## 概述 {#overview}

创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。

>[!IMPORTANT]
>
> 虽然Experience Platform支持将数据导出到SFTP服务器，但建议使用云存储位置导出数据 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![基于SFTP配置文件的导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA公钥"
>abstract="或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须编写为Base64编码字符串。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="专用SSH密钥"
>abstract="私有SSH密钥必须格式化为Base64编码的字符串，且不得受密码保护。 "

When [连接](../../ui/connect-destination.md) 要达到此目标，您必须提供以下信息：

#### 身份验证信息 {#authentication-information}

如果您选择 **[!UICONTROL 基本身份验证]** 键入以连接到SFTP位置：

![SFTP目标基本身份验证](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 主机]**:SFTP存储位置的地址；
* **[!UICONTROL 用户名]**:登录SFTP存储位置的用户名；
* **[!UICONTROL 密码]**:登录SFTP存储位置的密码。
* **[!UICONTROL 加密密钥]**:或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64] 编码字符串。
   * 示例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 请参阅下面格式正确的PGP键示例，其中间部分缩短为简短。

      ![PGP密钥](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


如果您选择 **[!UICONTROL 具有SSH密钥的SFTP]** 连接到SFTP位置的身份验证类型：

![SFTP目标SSH密钥身份验证](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 域]**:填写您的SFTP帐户的IP地址或域名
* **[!UICONTROL 端口]**:SFTP存储位置使用的端口；
* **[!UICONTROL 用户名]**:登录SFTP存储位置的用户名；
* **[!UICONTROL SSH密钥]**:用于登录SFTP存储位置的专用SSH密钥。 私钥必须格式化为Base64编码的字符串，且不得受密码保护。
* **[!UICONTROL 加密密钥]**:或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64] 编码字符串。
   * 示例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 请参阅下面格式正确的PGP键示例，其中间部分缩短为简短。

      ![PGP密钥](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 目标详细信息 {#destination-details}

在建立到SFTP位置的身份验证连接后，请提供目标的以下信息：

![SFTP目标的可用目标详细信息](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名称]**:在Experience Platform用户界面中输入一个名称，以帮助您识别此目标；
* **[!UICONTROL 描述]**:输入此目标的描述；
* **[!UICONTROL 文件夹路径]**:在SFTP位置中输入将导出文件的文件夹路径。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

对于 [!DNL SFTP] 目标，平台会创建 `.csv` 文件。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。

## IP地址允许列表

请参阅 [云存储目标的IP地址允许列表](ip-address-allow-list.md) 如果您需要将AdobeIP添加到允许列表。
