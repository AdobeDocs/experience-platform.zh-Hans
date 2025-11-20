---
title: LiveRamp — 载入连接
description: 了解如何使用LiveRamp连接器将受众从Adobe Real-Time Customer Data Platform载入LiveRamp Connect。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 4%

---

# [!DNL LiveRamp - Onboarding]连接 {#liveramp-onboarding}

使用[!DNL LiveRamp - Onboarding]连接将受众从Adobe Real-Time Customer Data Platform载入[!DNL LiveRamp Connect]。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL LiveRamp - Onboarding]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

作为营销人员，我希望将受众从Adobe Experience Platform发送到将身份载入到[!DNL LiveRamp Connect]中，以便我使用[!DNL CTV]标识符可以在移动设备、打开Web、社交和[!DNL Ramp ID]平台上定位用户。

## 先决条件 {#prerequisites}

[!DNL LiveRamp - Onboarding]连接使用[LiveRamp的SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)存储导出文件。

在将数据从Experience Platform发送到[!DNL LiveRamp - Onboarding]之前，您需要您的[!DNL LiveRamp]凭据。 请联系您的[!DNL LiveRamp]代表以获取凭据（如果尚未获取）。

## 支持的身份 {#supported-identities}

[!DNL LiveRamp - Onboarding]支持激活标识，如基于PII的标识符、已知标识符和自定义ID，如官方[LiveRamp文档](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)中所述。

在激活工作流的[映射步骤](#map)中，必须将目标映射定义为自定义属性。

## 支持的受众 {#supported-audiences}

本节介绍可以导出到此目标的受众类型。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform[分段服务](../../../segmentation/home.md)生成的访问群体。 |
| 自定义上传 | ✓ | 访问群体[已将](../../../segmentation/ui/audience-portal.md#import-audience)从CSV文件导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有[!DNL LiveRamp - Onboarding]目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Daily batch]** | 由于是根据受众评估在Experience Platform中更新用户档案的，因此用户档案（身份）每天都会在目标平台下游更新一次。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

**使用密码的SFTP身份验证** {#sftp-password}

![显示如何使用带有密码的SFTP向目标进行身份验证的示例屏幕截图](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Port]**：用于您的[!DNL LiveRamp - Onboarding]存储位置的端口。  使用与您所在地理位置对应的端口，如下所述：
   * **[!UICONTROL NA]**：使用端口`22`
   * **[!UICONTROL AU]**：使用端口`2222`
* **[!UICONTROL Username]**： [!DNL LiveRamp - Onboarding]存储位置的用户名。
* **[!UICONTROL Password]**： [!DNL LiveRamp - Onboarding]存储位置的密码。
* **[!UICONTROL PGP/GPG encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。
  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:If您提供了加密密钥，您还必须提供加密&#x200B;**[!UICONTROL Subkey ID]**。 请参阅[!DNL LiveRamp] [加密文档](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)以了解如何获取子密钥ID。

使用SSH密钥身份验证的&#x200B;**SFTP** {#sftp-ssh}

![显示如何使用SSH密钥向目标进行身份验证的示例屏幕截图](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Port]**：用于您的[!DNL LiveRamp - Onboarding]存储位置的端口。  使用与您所在地理位置对应的端口，如下所述：
   * **[!UICONTROL EU]**：使用端口`4222`
* **[!UICONTROL Username]**： [!DNL LiveRamp - Onboarding]存储位置的用户名。
* **[!UICONTROL SSH Key]**：用于登录到[!DNL SSH]存储位置的私有[!DNL LiveRamp - Onboarding]密钥。 私钥必须采用[!DNL Base64]编码的字符串格式，且不得受密码保护。

   * 若要将您的[!DNL SSH]密钥连接到[!DNL LiveRamp - Onboarding]服务器，您必须通过[!DNL LiveRamp]的技术支持门户提交票证，并提供您的公钥。 请参阅[LiveRamp文档](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client)中的详细信息。

* **[!UICONTROL PGP/GPG encryption key]**： （可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。
  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:If您提供了加密密钥，您还必须提供加密&#x200B;**[!UICONTROL Subkey ID]**。 请参阅[!DNL LiveRamp] [加密文档](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)以了解如何获取子密钥ID。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="加密子密钥 ID"
>abstract="用于加密（基于 LiveRamp 公共加密密钥）的子密钥 ID。如果您在身份验证步骤中提供了加密密钥，则此字段是必需的。"
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="了解如何获取子密钥 ID"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![Experience Platform UI屏幕截图显示如何填写目标的详细信息](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Region]**： LiveRamp SFTP存储实例的地理区域。
* **[!UICONTROL Folder path]**：将托管导出文件的[!DNL LiveRamp] `uploads`子文件夹的路径。 `uploads`前缀会自动添加到文件夹路径中。 [!DNL LiveRamp]建议为Adobe Real-Time CDP中的投放创建一个专用的子文件夹，以将文件与其他任何现有的馈送分开，并确保所有自动化运行顺利。
   * 例如，如果要将文件导出到`uploads/my_export_folder`，请在`my_export_folder`字段中键入&#x200B;**[!UICONTROL Folder path]**。
* **[!UICONTROL Compression format]**：选择Experience Platform应用于导出文件的压缩类型。 可用选项为&#x200B;**[!UICONTROL GZIP]**&#x200B;或&#x200B;**[!UICONTROL None]**。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请阅读有关使用UI订阅目标警报[的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，请选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[激活受众数据到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 日程计划 {#scheduling}

在[!UICONTROL Scheduling]步骤中，使用下面显示的设置为每个受众创建一个导出计划。

* **[!UICONTROL File export options]**： [!UICONTROL Export full files]。 [目标](../../ui/activate-batch-profile-destinations.md#export-incremental-files)当前不支持增量文件导出[!DNL LiveRamp]。
* **[!UICONTROL Frequency]**: [!UICONTROL Daily]
* **[!UICONTROL Date]**：根据需要选择导出开始和结束时间。

![显示受众计划步骤的Experience Platform UI屏幕截图。](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

导出的文件名当前不可由用户配置。 导出到[!DNL LiveRamp - Onboarding]目标的所有文件都会根据以下模板自动命名：

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Experience Platform UI屏幕截图显示了导出的文件名模板。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

例如，名为[!DNL Luma]的组织的导出文件的名称可能类似于以下内容：

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 映射属性和身份 {#map}

在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，您可以选择要为配置文件导出哪些属性和身份。

>[!IMPORTANT]
>
>此目标支持为每个激活流激活一个源标识命名空间。 如果需要导出多个标识命名空间（如`Email`和`Phone`），则必须为每个标识[创建单独的激活流](../../ui/activate-batch-profile-destinations.md)。

在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，**[!UICONTROL Target field]**&#x200B;映射定义导出的CSV文件中的列标题名称。 通过为&#x200B;**[!UICONTROL Target field]**&#x200B;提供自定义名称，您可以将导出文件中的CSV列标题更改为所需的任何友好名称。

>[!IMPORTANT]
>
>对于在首次将文件传递到[!DNL LiveRamp]后对目标字段所做的任何更改，请通知您的[!DNL LiveRamp]帐户团队或[向LiveRamp支持团队](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case)提交票证，以确保这些更改反映在自动化流程中。

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Add new mapping]**。 您将在屏幕上看到一个新的映射行。

   ![显示映射屏幕的Experience Platform UI屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select attributes]**&#x200B;类别并选择要映射的XDM属性，或选择&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;类别并选择要映射到目标的标识。

   ![显示源映射屏幕的Experience Platform UI屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;窗口中，输入要映射选定源字段的属性名称。 此处定义的属性名称将在导出的CSV文件中反映为列标题。

   ![Experience Platform UI屏幕快照显示目标映射屏幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   您还可以通过直接在&#x200B;**[!UICONTROL Target field]**&#x200B;中键入属性名称来输入该属性名称。

   ![Experience Platform UI屏幕快照显示目标映射屏幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

添加所有所需映射后，选择&#x200B;**[!UICONTROL Next]**&#x200B;并完成激活工作流。

## 导出的数据/验证数据导出 {#exported-data}

您的数据将导出到您配置的[!DNL LiveRamp - Onboarding]存储位置，即CSV文件。

导出的文件最大行数为1000万。 如果所选受众超过1000万行，则Experience Platform每次投放会生成多个文件。 如果您希望超过单个文件限制，请联系您的[!DNL LiveRamp]代表，让他们为您配置批量摄取。

将文件导出到[!DNL LiveRamp - Onboarding]目标时，Experience Platform为每个[合并策略ID](../../../profile/merge-policies/overview.md)生成一个CSV文件。

例如，我们来考虑以下受众：

* 受众A（合并策略1）
* 受众B（合并策略2）
* 受众C（合并策略1）
* 受众D（合并策略1）

Experience Platform会将两个CSV文件导出到[!DNL LiveRamp - Onboarding]：

* 一个包含受众A、C和D的CSV文件；
* 一个包含受众B的CSV文件。

导出的CSV文件包含具有选定属性和相应受众状态的配置文件，该文件位于单独的列中，具有属性名称，并且`audience_namespace:audience_ID`对作为列标题，如下面的示例所示：

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

导出文件中包含的用户档案可以与以下受众资格状态之一匹配：

* `Active`：配置文件当前符合受众条件。
* `Expired`：配置文件不再符合受众条件，但以前符合条件。
* `""`（空字符串）：个人资料从未符合受众的条件。

例如，如果导出的CSV文件具有一个`email`属性、两个源自Experience Platform [分段服务](../../../segmentation/home.md)的受众和一个[导入的](../../../segmentation/ui/audience-portal.md#import-audience)外部受众，则该文件可能如下所示：

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

在上述示例中，`ups_aa2e3d98-974b-4f8b-9507-59f65b6442df`和`ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f`部分描述了源自分段服务的受众，而`CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e`描述了作为[自定义上传](../../../segmentation/ui/audience-portal.md#import-audience)导入到Experience Platform中的受众。

由于Experience Platform为每个[合并策略ID](../../../profile/merge-policies/overview.md)生成一个CSV文件，因此它还为每个合并策略ID生成单独的数据流运行。

这意味着&#x200B;**[!UICONTROL Identities activated]**&#x200B;数据流运行&#x200B;**[!UICONTROL Profiles received]**&#x200B;页面中的[和](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)量度是为使用相同合并策略的每个受众组聚合的，而不是为每个受众显示的。

由于正在为使用相同合并策略的受众组生成数据流运行，因此受众名称不会显示在[监视仪表板](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)中。

![Experience Platform UI屏幕快照显示已激活身份指标。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## 将导出的数据上传到LiveRamp {#upload-to-liveramp}

将数据成功导出到[!DNL LiveRamp - Onboarding]存储之后，必须将数据上传到[!DNL LiveRamp]平台。

有关如何将文件从[!DNL LiveRamp - Onboarding]存储上传到[!DNL LiveRamp]受众的更多信息，请参阅以下文档： [将第一个文件上传到受众时的注意事项](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

有关如何配置[!DNL LiveRamp - Onboarding]存储空间的更多详细信息，请参阅[正式文档](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)。

## Changelog {#changelog}

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 3 月 | 功能和文档更新 | <ul><li>添加了对向欧洲和澳大利亚[!DNL LiveRamp]个[!DNL SFTP]实例的投放的支持。</li><li>更新了描述新支持区域的特定配置的文档。</li><li>已将最大文件大小增加到1,000万行（以前是500万行）。</li><li>更新了文档以反映增加的文件大小。</li></ul> |
| 2023 年 7 月 | 初始版本 | 发布了初始目标版本和文档。 |

{style="table-layout:auto"}

+++
