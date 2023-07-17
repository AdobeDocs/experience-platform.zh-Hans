---
title: Amazon S3连接
description: 创建到Amazon Web Services (AWS) S3存储的实时出站连接，定期将CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 11%

---

# [!DNL Amazon S3] 连接 {#s3-connection}

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>通过测试版的导出数据集功能和改进的文件导出功能，您现在可能会看到两个 [!DNL Amazon S3] 目标目录中的信息卡。
>* 如果您已经将文件导出到 **[!UICONTROL Amazon S3]** 目标，请新建数据流到新的 **[!UICONTROL Amazon S3 Beta]** 目标。
>* 如果您尚未创建任何数据流到 **[!UICONTROL Amazon S3]** 目标，请使用新的 **[!UICONTROL Amazon S3 Beta]** 用于导出文件的信息卡 **[!UICONTROL Amazon S3]**.

![并排视图中两个Amazon S3目标卡的图像。](../../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

新版中的改进 [!DNL Amazon S3] 目标卡包括：

* [数据集导出支持](/help/destinations/ui/export-datasets.md).
* 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 能够通过以下方式设置导出文件中的自定义文件标头： [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 概述 {#overview}

创建到 [!DNL Amazon S3] 存储，定期将数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 连接到您的 [!DNL Amazon S3] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 连接到您的 [!DNL Amazon S3] 存储位置使用Platform用户界面，请阅读部分 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下面的。
* 连接到您的 [!DNL Amazon S3] 存储位置以编程方式读取 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍可以导出到此目标的所有受众。

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表中描述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 从CSV文件引入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![基于配置文件的Amazon S3导出类型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**： In [!DNL Amazon S3]，生成 `access key - secret access key` 配对以授予Platform对的访问权限 [!DNL Amazon S3] 帐户。 了解详情，请参阅 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 在下图中查看正确格式化的加密密钥示例。

  ![图像显示UI中格式正确的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="存储桶名称"
>abstract="长度必须介于 3 和 63 个字符之间。必须以字母或数字开头和结尾。必须仅包含小写字母、数字或连字符 (-)。不得格式化为 IP 地址（例如，192.100.1.1）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="文件夹路径"
>abstract="必须仅包含字符 A-Z、a-z、0-9，并且可以包含以下特殊字符：`/!-_.'()"^[]+$%.*"`。要为每个受众文件创建一个文件夹，请插入宏 `/%SEGMENT_NAME%` 或 `/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 到文本字段中。 宏只能插入到文件夹路径的末尾。查看文档中的宏示例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=zh-Hans#use-macros" text="使用宏在存储位置创建一个文件夹"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 存储段名称]**：输入 [!DNL Amazon S3] 要由此目标使用的存储段。
* **[!UICONTROL 文件夹路径]**：输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 文件类型]**：选择导出文件应使用的格式Experience Platform。 此选项仅适用于 **[!UICONTROL Amazon S3 Beta]** 目标。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。 此选项仅适用于 **[!UICONTROL Amazon S3 Beta]** 目标。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 此选项仅适用于 **[!UICONTROL Amazon S3 Beta]** 目标。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的受众文件在Amazon S3存储中创建自定义文件夹。 读取 [使用宏在存储位置中创建文件夹](overview.md#use-macros) 以获取说明。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

### 必需 [!DNL Amazon S3] 权限 {#required-s3-permission}

要成功连接数据并将其导出到 [!DNL Amazon S3] 存储位置，创建身份和访问管理(IAM)用户 [!DNL Platform] 在 [!DNL Amazon S3] 并为以下操作分配权限：

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

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出数据集](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 导出的数据 {#exported-data}

对象 [!DNL Amazon S3] 目标， [!DNL Platform] 在提供的存储位置创建一个数据文件。 有关这些文件的详细信息，请参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 在audience activation教程中。
