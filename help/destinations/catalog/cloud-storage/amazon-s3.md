---
title: Amazon S3连接
description: 创建到Amazon Web Services (AWS) S3存储的实时出站连接，定期将CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 14%

---

# [!DNL Amazon S3]连接 {#s3-connection}

## 目标更改日志 {#changelog}

+++ 查看更改日志


| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 1 月 | 功能和文档更新 | Amazon S3目标连接器现在支持新的假定角色身份验证类型。 有关详情，请参阅[身份验证部分](#assumed-role-authentication)。 |
| 2023 年 7 月 | 功能和文档更新 | 在2023年7月发行的Experience Platform中，[!DNL Amazon S3]目标提供了新的功能，如下所示： <br><ul><li>[数据集导出支持](/help/destinations/ui/export-datasets.md)</li><li>额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。</li><li>可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。</li><li>[能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。</li></ul> |

{style="table-layout:auto"}

+++

## 通过API或UI连接到您的[!DNL Amazon S3]存储 {#connect-api-or-ui}

* 要使用Experience Platform用户界面连接到[!DNL Amazon S3]存储位置，请阅读下面的[连接到目标](#connect)和[将受众激活到此目标](#activate)部分。
* 若要以编程方式连接到[!DNL Amazon S3]存储位置，请阅读有关如何使用流服务API教程[将受众](../../api/activate-segments-file-based-destinations.md)激活到基于文件的目标的指南。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

![UU中突出显示的基于配置文件的Amazon S3导出类型。](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 如何使用Experience Platform用户界面[导出数据集](/help/destinations/ui/export-datasets.md)。
* 如何使用流服务API[以编程方式](/help/destinations/api/export-datasets.md)导出数据集。

## 导出数据的文件格式 {#file-format}

导出&#x200B;*受众数据*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.csv`、`parquet`或`.json`文件。 有关这些文件的更多信息，请参阅Audience Activation教程中的[导出的支持文件格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)部分。

导出&#x200B;*数据集*&#x200B;时，Experience Platform会在您提供的存储位置创建一个`.parquet`或`.json`文件。 有关这些文件的更多信息，请参阅导出数据集教程中的[验证成功的数据集导出](../../ui/export-datasets.md#verify)部分。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 公钥"
>abstract="（可选）您可以附加 RSA 格式的公钥以对导出的文件进行加密。在下面的文档链接中查看格式正确的密钥的示例。"

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。 Amazon S3目标支持两种身份验证方法：

* 访问密钥和密钥身份验证
* 担任的角色身份验证

#### 使用S3访问密钥和密钥进行身份验证

当您想要输入Amazon S3访问密钥和密钥，以允许Experience Platform将数据导出到Amazon S3资产时，请使用此身份验证方法。

![选择访问密钥和密钥身份验证时必填字段的图像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]访问密钥**&#x200B;和&#x200B;**[!DNL Amazon S3]密钥**：在[!DNL Amazon S3]中，生成一个`access key - secret access key`对以授予Experience Platform对您[!DNL Amazon S3]帐户的访问权限。 请参阅[Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)以了解详情。
* **[!UICONTROL Encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像。](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 使用 S3 的假设角色进行身份验证 {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="担任的角色身份验证"
>abstract="如果您不想与 Adobe 共享帐户密钥和私钥，请使用此身份验证类型。Experience Platform 而是会使用基于角色的访问权限连接到您的 Amazon S3 位置。粘贴您在 AWS 中为 Adobe 用户所创建角色的 ARN。该模式类似于 `arn:aws:iam::800873819705:role/destinations-role-customer` "

如果您不想与 Adobe 共享帐户密钥和私钥，请使用此身份验证类型。相反，Experience Platform会使用基于角色的访问连接到您的Amazon S3位置。

![选择假定的角色身份验证时必填字段的图像。](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**：将您在AWS中为Adobe用户创建的角色的ARN粘贴。 模式类似于`arn:aws:iam::800873819705:role/destinations-role-customer`。 有关如何正确配置S3访问权限的详细指导，请参阅以下步骤。
* **[!UICONTROL Encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。

为此，您需要在AWS控制台中创建一个假定的Adobe角色，该角色具有[写入Amazon S3存储桶所需的正确权限](#minimum-permissions-iam-user)。

**创建具有所需权限的策略**

1. 打开AWS控制台，然后转到IAM >策略>创建策略
2. 选择策略编辑器> JSON并添加以下权限。

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. 在下一页上，输入策略的名称并将其保存以供参考。 在下一步中创建角色时，您将需要此策略名称。

**在您的S3客户帐户中创建用户角色**

1. 打开AWS Console，然后转到IAM >角色>创建新角色
2. 选择&#x200B;**受信任的实体类型** > **AWS帐户**
3. 选择&#x200B;**一个AWS帐户** > **另一个AWS帐户**，并输入Adobe帐户ID： `670664943635`
4. 使用之前创建的策略添加权限
5. 输入角色名称（例如，`destinations-role-customer`）。 角色名称应被视为机密名称，与密码类似。 它最长可包含64个字符，可包含字母数字字符和以下特殊字符： `+=,.@-_`。 然后验证：
   * Adobe帐户ID `670664943635`存在于&#x200B;**[!UICONTROL Select trusted entities]**&#x200B;部分中
   * 之前创建的策略存在于&#x200B;**[!UICONTROL Permissions policy summary]**&#x200B;中

**为Adobe提供要承担的角色**

在AWS中创建角色后，您需要向Adobe提供角色ARN。 ARN遵循以下模式： `arn:aws:iam::800873819705:role/destinations-role-customer`

在AWS控制台中创建角色后，您可以在主页上找到ARN。 在创建目标时，您将使用此ARN。

**验证角色权限和信任关系**

确保您的角色具有以下配置：

* **权限**：角色应具有访问S3的权限（在上面的&#x200B;**创建具有所需权限的策略**&#x200B;步骤中提供的完全访问权限或最低权限）
* **信任关系**：该角色的信任关系中应该具有根Adobe帐户(`670664943635`)

**替代：限制为特定的Adobe用户（可选）**

如果您不希望允许使用整个Adobe帐户，则可以限制仅访问特定的Adobe用户。 为此，请使用以下配置编辑信任策略：

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

有关更多信息，请参阅有关创建角色的[AWS文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html)。



### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="存储桶名称"
>abstract="长度必须介于 3 和 63 个字符之间。必须以字母或数字开头和结尾。必须仅包含小写字母、数字或连字符 (-)。不得格式化为 IP 地址（例如，192.100.1.1）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="文件夹路径"
>abstract="必须仅包含字符 A-Z、a-z、0-9，并且可以包含以下特殊字符：`/!-_.'()"^[]+$%.*"`。要为每个受众文件创建一个文件夹，请将宏 `/%SEGMENT_NAME%`、`/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 插入文本字段。宏只能插入到文件夹路径的末尾。查看文档中的宏示例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="使用宏在存储位置创建一个文件夹"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：输入一个名称，以帮助您识别此目标。
* **[!UICONTROL Description]**：输入此目标的描述。
* **[!UICONTROL Bucket name]**：输入要由此目标使用的[!DNL Amazon S3]存储段的名称。
* **[!UICONTROL Folder path]**：输入将承载导出文件的目标文件夹的路径。
* **[!UICONTROL File type]**：选择Experience Platform应用于导出文件的格式。 在选择[!UICONTROL CSV]选项时，您还可以[配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL Compression format]**：选择Experience Platform应该用于导出文件的压缩类型。
* **[!UICONTROL Include manifest file]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为`manifest-<<destinationId>>-<<dataflowRunId>>.json`。 查看[样本清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)。 清单文件包含以下字段：
   * `flowRunId`：生成导出文件的[数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中保存导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（字节）。

>[!TIP]
>
>在连接目标工作流中，您可以在Amazon S3存储中为每个导出的受众文件创建一个自定义文件夹。 有关说明，请阅读[使用宏在存储位置](overview.md#use-macros)中创建文件夹。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

### 所需的[!DNL Amazon S3]权限 {#required-s3-permission}

要成功连接数据并将其导出到您的[!DNL Amazon S3]存储位置，请在[!DNL Experience Platform]中为[!DNL Amazon S3]创建标识和访问管理(IAM)用户，并为以下操作分配权限：

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### IAM角色身份验证所需的最低权限 {#minimum-permissions-iam-user}

在将IAM角色配置为客户时，请确保与角色关联的权限策略包括存储段中目标文件夹的所需操作以及存储段根的`s3:ListBucket`操作。 查看以下此身份验证类型的最低权限策略示例：

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

## 验证数据导出是否成功 {#exported-data}

要验证是否已成功导出数据，请检查您的[!DNL Amazon S3]存储并确保导出的文件包含预期的配置文件人口。

## IP地址允许列表 {#ip-address-allow-list}

如果您需要将Adobe 列入允许列表 IP添加到，请参阅[IP地址允许列表](ip-address-allow-list.md)一文。