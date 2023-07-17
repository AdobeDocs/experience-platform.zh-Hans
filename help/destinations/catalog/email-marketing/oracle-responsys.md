---
keywords: 电子邮件；电子邮件；电子邮件目标；oracleresponsys目标
title: oracleResponsys连接
description: Responsys是一款用于跨渠道营销活动的企业电子邮件营销工具，由Oracle提供，用于个性化电子邮件、移动设备、显示和社交之间的交互。
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# [!DNL Oracle Responsys] 连接

## 概述 {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) 是一款用于跨渠道营销活动的企业电子邮件营销工具，由 [!DNL Oracle] 使电子邮件、移动设备、显示和社交之间的交互个性化。

要将受众数据发送到，请执行以下操作 [!DNL Oracle Responsys]，您必须首先 [连接到目标](#connect-destination) 在Adobe Experience Platform中，然后 [设置数据导入](#import-data-into-responsys) 从存储位置到 [!DNL Oracle Responsys].

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

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议向允许列表添加特定IP范围。

请参阅 [SFTP目标的IP地址允许列表](../cloud-storage/ip-address-allow-list.md) (如果需要将AdobeIP添加到允许列表)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

此目标支持以下连接类型：

* **[!UICONTROL 包含密码的SFTP]**
* **[!UICONTROL 使用SSH密钥的SFTP]**

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* 对象 **[!UICONTROL 包含密码的SFTP]** 连接，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL 密码]
* 对象 **[!UICONTROL 使用SSH密钥的SFTP]** 连接，您必须提供：
   * [!UICONTROL 域]
   * [!UICONTROL 端口]
   * [!UICONTROL 用户名]
   * [!UICONTROL SSH密钥]
* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到导出文件，位于 **[!UICONTROL 键]** 部分。 您的公钥必须写为 [!DNL Base64] 编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* **[!UICONTROL 文件夹路径]**：提供存储位置中的路径，Platform会将导出数据作为CSV文件存储在该位置。
* **[!UICONTROL 文件格式]**：选择 **CSV** 以将CSV文件导出到存储位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对象 [!DNL Oracle Responsys] 目标，平台创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [验证受众激活](../../ui/activate-batch-profile-destinations.md#verify) 在audience activation教程中。

## 设置数据导入到 [!DNL Oracle Responsys] {#import-data-into-responsys}

连接后 [!DNL Platform] 敬您的 [!DNL SFTP] 存储时，您必须设置从存储位置导入到的数据导入过程 [!DNL Oracle Responsys]. 要了解如何完成此操作，请参阅 [正在导入联系人或帐户](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 在 [!DNL Oracle Responsys Help Center].
