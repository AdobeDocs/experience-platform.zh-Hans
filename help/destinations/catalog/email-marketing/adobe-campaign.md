---
keywords: 电子邮件；电子邮件；电子邮件目标；adobe campaign；营销活动
title: Adobe Campaign连接
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 47e0dfb59edca58e205cb478e9ee624659753ab9
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# Adobe Campaign连接

## 概述 {#overview}

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。 参见 [Campaign Classic入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 了解更多信息。

要将区段数据发送到Adobe Campaign，您必须首先 [连接目标](#connect-destination) 在Adobe Experience Platform中，然后 [设置数据导入](#import-data-into-campaign) 从存储位置移至Adobe Campaign。

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
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

Adobe Campaign支持以下连接类型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 包含密码的SFTP]**
* **[!UICONTROL 使用SSH密钥的SFTP]**
* **[!UICONTROL Azure Blob]**

将数据发送到Adobe Campaign的首选方法是通过 [!DNL Amazon S3] 或 [!DNL Azure Blob].

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* 对象 **[!UICONTROL Amazon S3]** 连接，您必须提供 [!UICONTROL 访问密钥ID] 和 [!UICONTROL 访问密钥].
* 对象 **[!UICONTROL 包含密码的SFTP]** 连接，您必须提供 [!UICONTROL 域]， [!UICONTROL 端口]， [!UICONTROL 用户名]、和 [!UICONTROL 密码].
* 对象 **[!UICONTROL 使用SSH密钥的SFTP]** 连接，您必须提供 [!UICONTROL 域]， [!UICONTROL 端口]， [!UICONTROL 用户名]、和 [!UICONTROL SSH密钥].
* 对象 **[!UICONTROL Azure Blob]** 连接，您必须提供连接字符串。
* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到导出文件，位于 **[!UICONTROL 键]** 部分。 您的公钥必须写为 [!DNL Base64] 编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* **[!UICONTROL 存储段名称]**： *对于S3连接*. 输入S3存储段的位置，其中 [!DNL Platform] 会将您的导出数据另存为CSV文件。
* **[!UICONTROL 文件夹路径]**：提供存储位置中的路径，其中 [!DNL Platform] 会将您的导出数据另存为CSV文件。
* **[!UICONTROL 容器]**： *对于Blob连接*. 保存文件夹路径所在的Blob的容器。
* **[!UICONTROL 文件格式]**：选择 **CSV** 以将CSV文件导出到存储位置。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。


参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#destination-attributes}

将区段激活到此目标时，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对象 [!DNL Adobe Campaign] 目标， [!DNL Platform] 创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [验证区段激活](../../ui/activate-batch-profile-destinations.md#verify) 在区段激活教程中。

## 设置数据导入Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 请记住 [!DNL SFTP] 在执行此集成时，根据Adobe Campaign合同中的存储限制、数据库存储限制和活动配置文件限制。
>* 您需要使用以下方式在Adobe Campaign中计划、导入和映射导出的区段 [!DNL Campaign] 工作流。 请参阅 [设置循环导入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 在Adobe Campaign Classic文档和 [关于数据管理活动](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) 在Adobe Campaign Standard文档中。
>* 将数据发送到Adobe Campaign的首选方法是通过 [!DNL Amazon S3] 或 [!DNL Azure Blob].


连接后 [!DNL Platform] 敬您的 [!DNL Amazon S3] 或 [!DNL Azure Blob] 存储中，您必须设置将数据从存储位置导入Adobe Campaign。 要了解如何完成此任务，请参阅以下Adobe Campaign文档页面：
* [数据导入和导出入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans) 和 [正在加载数据（文件）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 在Adobe Campaign Classic文档中。
* [流程和数据管理入门](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和 [加载文件](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 在Adobe Campaign Standard文档中。
