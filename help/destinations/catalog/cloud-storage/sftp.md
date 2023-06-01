---
keywords: SFTP；sftp
title: SFTP连接
description: 创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 47e0dfb59edca58e205cb478e9ee624659753ab9
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 7%

---

# SFTP连接

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>通过测试版的导出数据集功能和改进的文件导出功能，您现在可能会看到两个 [!DNL SFTP] 目标目录中的信息卡。
>* 如果您已经将文件导出到 **[!UICONTROL SFTP]** 目标：请为新的数据集创建新的数据流 **[!UICONTROL SFTP测试版]** 目标。
>* 如果您尚未创建任何数据流到 **[!UICONTROL SFTP]** 目标，请使用新的 **[!UICONTROL SFTP测试版]** 用于导出文件的信息卡 **[!UICONTROL SFTP]**.


![并排视图中两个SFTP目标卡的图像。](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

新版中的改进 [!DNL SFTP] 目标卡包括：

* [数据集导出支持](/help/destinations/ui/export-datasets.md).
* 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 能够通过以下方式设置导出文件中的自定义文件标头： [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

创建到SFTP服务器的实时出站连接，定期从Adobe Experience Platform导出分隔的数据文件。

>[!IMPORTANT]
>
> 虽然Experience Platform支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为 [!DNL Amazon S3] 和 [!DNL SFTP].

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![基于配置文件的SFTP导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 身份验证信息 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="私有 SSH 密钥"
>abstract="私有 SSH 密钥的格式必须为 Base64 编码的字符串，并且不得受密码保护。"

如果您选择 **[!UICONTROL 基本身份验证]** 键入以连接到SFTP位置：

![SFTP目标基本身份验证](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 主机]**：SFTP存储位置的地址；
* **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL 密码]**：用于登录到SFTP存储位置的密码。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 在下图中查看正确格式化的加密密钥示例。

   ![图像显示UI中格式正确的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


如果您选择 **[!UICONTROL 使用SSH密钥的SFTP]** 要连接到SFTP位置的身份验证类型：

![SFTP目标SSH密钥身份验证](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 域]**：填写SFTP帐户的IP地址或域名
* **[!UICONTROL 端口]**：您的SFTP存储位置使用的端口；
* **[!UICONTROL 用户名]**：用于登录到SFTP存储位置的用户名；
* **[!UICONTROL SSH密钥]**：用于登录到SFTP存储位置的私有SSH密钥。 私有 密钥的格式必须为 Base64 编码的字符串，并且不得受密码保护。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 在下图中查看正确格式化的加密密钥示例。

   ![图像显示UI中格式正确的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目标详细信息 {#destination-details}

在建立与SFTP位置的身份验证连接后，提供目标的以下信息：

![SFTP目标的可用目标详细信息](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名称]**：输入有助于您在Experience Platform用户界面中标识此目标的名称；
* **[!UICONTROL 描述]**：输入此目标的描述；
* **[!UICONTROL 文件夹路径]**：输入要导出文件的SFTP位置中的文件夹路径。
* **[!UICONTROL 文件类型]**：选择导出文件应使用的格式Experience Platform。 此选项仅适用于 **[!UICONTROL SFTP测试版]** 目标。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。 此选项仅适用于 **[!UICONTROL SFTP测试版]** 目标。
* 
   * **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 此选项仅适用于 **[!UICONTROL SFTP测试版]** 目标。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请参阅 [导出数据集教程](/help/destinations/ui/export-datasets.md).

## 导出的数据 {#exported-data}

对象 [!DNL SFTP] 目标，平台创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在区段激活教程中。

## IP地址允许列表

请参阅 [SFTP目标的IP地址允许列表](ip-address-allow-list.md) (如果需要将AdobeIP添加到允许列表)。
