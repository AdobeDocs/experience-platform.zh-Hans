---
keywords: SFTP;SFTP
title: SFTP连接
description: 创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 691e3181e05a24b6bb0ebbe8e0f797a2b4c572d2
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# SFTP连接

## 概述 {#overview}

创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。

>[!IMPORTANT]
>
> 虽然Adobe支持将数据导出到SFTP服务器，但建议使用云存储位置导出数据 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![基于SFTP配置文件的导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA公钥"
>abstract="或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须编写为Base64编码字符串。"

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **主机**:SFTP存储位置的地址
* **用户名**:登录SFTP存储位置的用户名
* **密码**:登录SFTP存储位置的密码
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64] 编码字符串。

## 导出的数据 {#exported-data}

对于 [!DNL SFTP] 目标，平台会创建 `.csv` 文件。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。

## IP地址允许列表

请参阅 [云存储目标的IP地址允许列表](ip-address-allow-list.md) 如果您需要将AdobeIP添加到允许列表。
