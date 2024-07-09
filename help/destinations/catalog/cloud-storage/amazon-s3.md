---
title: Amazon S3连接
description: 创建到Amazon Web Services (AWS) S3存储的实时出站连接，定期将CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] 连接 {#s3-connection}

## 目标更改日志 {#changelog}

+++ 查看更改日志


| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 1 月 | 功能和文档更新 | Amazon S3目标连接器现在支持新的假定角色身份验证类型。 欲知更多信息，请参阅 [身份验证部分](#assumed-role-authentication). |
| 2023 年 7 月 | 功能和文档更新 | 在2023年7月的Experience Platform版本中， [!DNL Amazon S3] 目标提供了新功能，如下所示： <br><ul><li>[支持数据集导出](/help/destinations/ui/export-datasets.md)</li><li>额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。</li><li>可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。</li><li>[能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## 连接到您的 [!DNL Amazon S3] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 要连接到 [!DNL Amazon S3] 存储位置使用Platform用户界面，请阅读以下章节 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下。
* 要连接到 [!DNL Amazon S3] 以编程方式存储位置，请阅读有关如何使用 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![UU中突出显示的基于配置文件的Amazon S3导出类型。](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 导出数据的文件格式 {#file-format}

导出时 *受众数据*，平台创建 `.csv`， `parquet`，或 `.json` 文件存储位置。 有关这些文件的详细信息，请参见 [支持的导出文件格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 部分。

导出时 *数据集*，平台创建 `.parquet` 或 `.json` 文件存储位置。 有关这些文件的详细信息，请参见 [验证数据集导出是否成功](../../ui/export-datasets.md#verify) 导出数据集教程中的部分。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**. Amazon S3目标支持两种身份验证方法：

* 访问密钥和密钥身份验证
* 担任的角色身份验证

#### 访问密钥和密钥身份验证

当您想要输入Amazon S3访问密钥和密钥，以允许Experience Platform将数据导出到Amazon S3资产时，请使用此身份验证方法。

![选择访问密钥和密钥身份验证时必填字段的图像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**：在 [!DNL Amazon S3]，生成 `access key - secret access key` 对，以授予对的Platform访问权限 [!DNL Amazon S3] 帐户。 在中了解详情 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![该图像显示了UI中格式正确的PGP密钥的示例。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 担任的角色 {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="担任的角色身份验证"
>abstract="如果您不想与 Adobe 共享帐户密钥和私钥，请使用此身份验证类型。Experience Platform 而是会使用基于角色的访问权限连接到您的 Amazon S3 位置。粘贴您在 AWS 中为 Adobe 用户所创建角色的 ARN。该模式类似于 `arn:aws:iam::800873819705:role/destinations-role-customer` "

![选择承担的角色身份验证时必填字段的图像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

如果您不想与 Adobe 共享帐户密钥和私钥，请使用此身份验证类型。相反，Experience Platform会使用基于角色的访问连接到Amazon S3位置。

为此，您需要在AWS控制台中创建假定用户，以便Adobe [权限必需权限](#required-s3-permission) 以写入您的Amazon S3存储段。 创建 **[!UICONTROL 受信任的实体]** 在AWS中使用Adobe帐户 **[!UICONTROL 670664943635]**. 欲了解更多信息，请参见 [有关创建角色的AWS文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**：粘贴您在AWS中为Adobe用户创建的角色的ARN。 模式类似于 `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="存储桶名称"
>abstract="长度必须介于 3 和 63 个字符之间。必须以字母或数字开头和结尾。必须仅包含小写字母、数字或连字符 (-)。不得格式化为 IP 地址（例如，192.100.1.1）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="文件夹路径"
>abstract="必须仅包含字符 A-Z、a-z、0-9，并且可以包含以下特殊字符：`/!-_.'()"^[]+$%.*"`。要为每个受众文件创建一个文件夹，请将宏 `/%SEGMENT_NAME%`、`/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 插入文本字段。宏只能插入到文件夹路径的末尾。查看文档中的宏示例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=zh-Hans#use-macros" text="使用宏在存储位置创建一个文件夹"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 存储段名称]**：输入 [!DNL Amazon S3] 要由此目标使用的存储桶。
* **[!UICONTROL 文件夹路径]**：输入目标文件夹的路径，该文件夹将托管导出的文件。
* **[!UICONTROL 文件类型]**：选择导出的文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 查看 [示例清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 清单文件包含以下字段：
   * `flowRunId`：和 [数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 生成了导出的文件。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中存储导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（以字节为单位）。

>[!TIP]
>
>在连接目标工作流中，您可以在Amazon S3存储中为每个导出的受众文件创建一个自定义文件夹。 读取 [使用宏在您的存储位置中创建文件夹](overview.md#use-macros) 以获取说明。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

### 必填 [!DNL Amazon S3] 权限 {#required-s3-permission}

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

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Amazon S3] 存储并确保导出的文件包含预期的配置文件人口。

## IP地址允许列表 {#ip-address-allow-list}

请参阅 [IP地址允许列表](ip-address-allow-list.md) 文章(如果需要将AdobeIP添加到允许列表)。