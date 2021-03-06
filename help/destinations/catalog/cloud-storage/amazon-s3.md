---
keywords: Amazon S3;S3目标；s3;Amazon s3
title: Amazon S3连接
description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 1%

---

# [!DNL Amazon S3] 连接 {#s3-connection}

## 概述 {#overview}

创建到的实时出站连接 [!DNL Amazon Web Services] (AWS)S3存储，可将CSV数据文件从Adobe Experience Platform定期导出到您自己的S3存储段中。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Amazon S3基于配置文件的导出类型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA公钥"
>abstract="或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64-encoded] 字符串。 在下面的文档链接中查看格式正确的键值示例。"

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**:在 [!DNL Amazon S3]，生成 `access key - secret access key` 对，以授予对 [!DNL Amazon S3] 帐户。 在 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密密钥]**:或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64-encoded] 字符串。
   * 示例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 请参阅下面格式正确的PGP键示例，其中间部分缩短为简短。

      ![PGP密钥](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="存储段名称"
>abstract="长度必须介于3到63个字符之间。 必须以字母或数字开头和结尾。 必须只包含小写字母、数字或连字符(-)。 不得格式化为IP地址（例如，192.100.1.1）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="文件夹路径"
>abstract="必须只包含字符A-Z、a-z、0-9，并且可以包含以下特殊字符： `/!-_.'()"^[]+$%.*"`. 要按区段文件创建文件夹，请插入宏 `/%SEGMENT_NAME%` 或 `/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 中。 宏只能在文件夹路径的末尾插入。 查看文档中的宏示例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="使用宏在存储位置中创建文件夹"

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 存储段名称]**:输入 [!DNL Amazon S3] 存储段供此目标使用。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的区段文件在Amazon S3存储中创建自定义文件夹。 读取 [使用宏在存储位置中创建文件夹](overview.md#use-macros) 中。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

### 必需 [!DNL Amazon S3] 权限 {#required-s3-permission}

要成功将数据连接并导出到 [!DNL Amazon S3] 存储位置，为创建Identity and Access Management(IAM)用户 [!DNL Platform] in [!DNL Amazon S3] 并为以下操作分配权限：

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

对于 [!DNL Amazon S3] 目标， [!DNL Platform] 创建 `.csv` 文件。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。
