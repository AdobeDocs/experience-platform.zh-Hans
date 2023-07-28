---
title: LiveRamp — 载入连接
description: 了解如何使用LiveRamp连接器将受众从Adobe Real-time Customer Data Platform载入LiveRamp Connect。
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: b9100d5a0f5901a51b183cda49ac9591d74f2e2a
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 3%

---

# [!DNL LiveRamp - Onboarding] 连接 {#liveramp-onboarding}

使用 [!DNL LiveRamp - Onboarding] 从Adobe Real-time Customer Data Platform连接到载入受众到 [!DNL LiveRamp Connect].

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL LiveRamp - Onboarding] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

作为营销人员，我希望将受众从Adobe Experience Platform发送到以将身份载入 [!DNL LiveRamp Connect] 这样我就能定位移动设备、开放网络、社交和 [!DNL CTV] 平台，使用 [!DNL Ramp ID] 标识符。

## 先决条件 {#prerequisites}

此 [!DNL LiveRamp - Onboarding] 连接导出文件，使用 [LiveRamp的SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) 存储。

将数据从Experience Platform发送到之前 [!DNL LiveRamp - Onboarding]，您需要您的 [!DNL LiveRamp] 凭据。 请联系您的 [!DNL LiveRamp] 代表获取您的凭据（如果尚未获取）。

## 支持的身份 {#supported-identities}

[!DNL LiveRamp - Onboarding] 支持激活身份，如基于PII的标识符、已知标识符和自定义ID，如官方网站所述 [LiveRamp文档](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

在 [映射步骤](#map) 在激活工作流中，必须将目标映射定义为自定义属性。

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表所述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 受众 [已导入](../../../segmentation/ui/overview.md#importing-an-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正使用 [!DNL LiveRamp - Onboarding] 目标。 |
| 导出频率 | **[!UICONTROL 每日批次]** | 由于用户档案是根据受众评估在Experience Platform中进行更新的，因此用户档案（身份）每天都会更新一次以流向目标平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

**使用密码的SFTP身份验证** {#sftp-password}

![显示如何使用带有密码的SFTP向目标进行身份验证的示例屏幕截图](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL 用户名]**：您的用户名 [!DNL LiveRamp - Onboarding] 存储位置。
* **[!UICONTROL 密码]**：您的密码 [!DNL LiveRamp - Onboarding] 存储位置。
* **[!UICONTROL PGP/GPG加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 查看下图中的加密密钥格式正确示例。 如果提供加密密钥，则还必须提供 **[!UICONTROL 加密子密钥Id]** 在 [目标详细信息](#destination-details) 部分。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)

**具有SSH密钥身份验证的SFTP** {#sftp-ssh}

![显示如何使用SSH密钥向目标进行身份验证的示例屏幕截图](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL 用户名]**：您的用户名 [!DNL LiveRamp - Onboarding] 存储位置。
* **[!UICONTROL SSH密钥]**：私有 [!DNL SSH] 用于登录到 [!DNL LiveRamp - Onboarding] 存储位置。 私钥必须设置为 [!DNL Base64] — 编码字符串，且不能受密码保护。

   * 连接您的 [!DNL SSH] 键到 [!DNL LiveRamp - Onboarding] 服务器，您必须通过提交票证 [!DNL LiveRamp]的技术支持门户，并提供您的公钥。 欲知更多信息，请参见 [LiveRamp文档](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 如果提供加密密钥，则还必须提供 **[!UICONTROL 加密子密钥Id]** 在 [目标详细信息](#destination-details) 部分。 查看下图中的加密密钥格式正确示例。

  ![显示UI中格式正确的PGP密钥示例的图像](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="加密子密钥 ID"
>abstract="用于加密（基于 LiveRamp 公共加密密钥）的子密钥 ID。如果您在身份验证步骤中提供了加密密钥，则此字段是必需的。"
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="了解如何获取子密钥 ID"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![平台UI屏幕截图，其中显示如何填写目标的详细信息](../../assets/catalog/advertising/liveramp-onboarding/liveramp-connection-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 文件夹路径]**：的路径 [!DNL LiveRamp] `uploads` 将托管导出文件的子文件夹。 此 `uploads` 前缀会自动添加到文件夹路径中。 [!DNL LiveRamp] 建议为Adobe Real-Time CDP中的投放创建一个专用的子文件夹，以将文件与其他任何现有的馈送分开，并确保所有自动操作平稳运行。
   * 例如，如果要将文件导出到 `uploads/my_export_folder`，键入 `my_export_folder` 在 **[!UICONTROL 文件夹路径]** 字段。
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。 可用选项包括 **[!UICONTROL GZIP]** 或 **[!UICONTROL 无]**.
* **[!UICONTROL 加密子密钥Id]**：用于加密的子密钥，基于 [!DNL LiveRamp] 公共加密密钥。 如果您在 [身份验证](#authenticate) 步骤。 请参阅 [!DNL LiveRamp] [加密文档](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) 以了解如何获取子键ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请阅读以下指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 计划 {#scheduling}

在 [!UICONTROL 正在计划] 步骤，使用下面显示的设置为每个受众创建导出计划。

>[!IMPORTANT]
>
>所有激活到此目标的受众都必须使用完全相同的计划进行配置，如下所示。

* **[!UICONTROL 文件导出选项]**： [!UICONTROL 导出完整文件]. [增量文件导出](../../ui/activate-batch-profile-destinations.md#export-incremental-files) 当前不支持 [!DNL LiveRamp] 目标。
* **[!UICONTROL 频率]**： [!UICONTROL 每日]
* 将导出时间设置为 **[!UICONTROL 区段评估后]**. 计划的受众导出和 [按需文件导出](../../ui/export-file-now.md) 当前不支持 [!DNL LiveRamp] 目标。
* **[!UICONTROL 日期]**：根据需要选择导出开始和结束时间。

![显示受众计划步骤的平台UI屏幕截图。](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

导出的文件名当前不可由用户配置。 所有导出到 [!DNL LiveRamp - Onboarding] 目标基于以下模板自动命名：

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![显示导出的文件名模板的平台UI屏幕截图。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

例如，为名为的组织导出的文件的名称 [!DNL Luma] 可能会与以下内容类似：

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 映射属性和身份 {#map}

在 **[!UICONTROL 映射]** 步骤，您可以选择要为用户档案导出的属性和身份。

>[!IMPORTANT]
>
>此目标支持为每个激活流激活一个源身份命名空间。 如果需要导出多个身份命名空间，例如 `Email` 和 `Phone`，您必须 [创建单独的激活流程](../../ui/activate-batch-profile-destinations.md) 每个身份。

在 **[!UICONTROL 映射]** 步骤， **[!UICONTROL 目标字段]** 映射定义导出的CSV文件中列标题的名称。 您可以通过提供自定义名称将导出文件中的CSV列标题更改为所需的任何友好名称 **[!UICONTROL 目标字段]**.

>[!IMPORTANT]
>
>用于在初次将文件交付到目标字段后对目标字段所做的任何更改 [!DNL LiveRamp]，请通知 [!DNL LiveRamp] 客户团队或 [向LiveRamp支持部门提交票证](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) 以确保更改反映在自动化流程中。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。

   ![显示“映射”屏幕的Experience PlatformUI屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择要映射的XDM属性，或选择 **[!UICONTROL 选择身份命名空间]** 类别并选择要映射到目标的标识。

   ![显示源“映射”屏幕的Experience PlatformUI屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. 在 **[!UICONTROL 选择目标字段]** 窗口中，输入要映射选定源字段的属性名称。 此处定义的属性名称将在导出的CSV文件中反映为列标题。

   ![显示Experience Platform“映射”屏幕的目标用户界面屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   也可以直接在“ ”中输入属性名称 **[!UICONTROL 目标字段]**.

   ![显示Experience Platform“映射”屏幕的目标用户界面屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

添加所有所需映射后，选择 **[!UICONTROL 下一个]** 并完成激活工作流。

## 导出的数据/验证数据导出 {#exported-data}

您的数据将导出到 [!DNL LiveRamp - Onboarding] 您配置的存储位置，如CSV文件。

将文件导出到 [!DNL LiveRamp - Onboarding] 目标，平台为每个目标生成一个CSV文件 [合并策略Id](../../../profile/merge-policies/overview.md).

例如，我们来考虑以下受众：

* 受众A（合并策略1）
* 受众B（合并策略2）
* 受众C（合并策略1）
* 受众D（合并策略1）

Platform会将两个CSV文件导出到 [!DNL LiveRamp - Onboarding]：

* 一个包含受众A、C和D的CSV文件；
* 一个包含受众B的CSV文件。

导出的CSV文件包含具有选定属性和相应受众状态的配置文件，这些配置文件位于单独的列中，并具有属性名称和 `audience_namespace:audience_ID` 对作为列标题，如以下示例所示：

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1:AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2:AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X:AUDIENCE_ID_X`

导出文件中包含的用户档案可以与以下受众资格状态之一匹配：

* `Active`：用户档案当前符合受众条件。
* `Expired`：用户档案不再符合受众条件，而是以前符合条件。
* `""`（空字符串）：个人资料从未符合受众条件。

例如，导出的CSV文件包含一个 `email` 属性，两个源自Experience Platform的受众 [分段服务](../../../segmentation/home.md)，和一个 [已导入](../../../segmentation/ui/overview.md#importing-an-audience) 外部受众，可能如下所示：

```csv
email,ups:aa2e3d98-974b-4f8b-9507-59f65b6442df,ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

在上例中， `ups:aa2e3d98-974b-4f8b-9507-59f65b6442df` 和 `ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` 部分介绍源自Segmentation Service的受众，而 `CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e` 描述导入到Platform as a的受众 [自定义上传](../../../segmentation/ui/overview.md#importing-an-audience).

因为Platform为每个生成一个CSV文件 [合并策略Id](../../../profile/merge-policies/overview.md)，它还会为每个合并策略ID生成单独的数据流运行。

这意味着 **[!UICONTROL 已激活身份]** 和 **[!UICONTROL 已接收配置文件]** 中的量度 [数据流运行](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 系统会为使用相同合并策略的每个受众组聚合页面，而不是为每个受众显示页面。

由于为使用相同合并策略的一组受众生成了数据流，因此受众名称不会显示在 [监视仪表板](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![显示“身份已激活”指标的Experience PlatformUI屏幕快照。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## 将导出的数据上传到LiveRamp {#upload-to-liveramp}

成功将数据导出到 [!DNL LiveRamp - Onboarding] 存储时，您必须将数据上传到 [!DNL LiveRamp] 平台。

有关如何从上传文件的更多信息 [!DNL LiveRamp - Onboarding] 存储到 [!DNL LiveRamp] 受众，请参阅以下文档： [将第一个文件上传到受众时的注意事项](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关如何配置 [!DNL LiveRamp - Onboarding] 存储，请参见 [官方文档](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
