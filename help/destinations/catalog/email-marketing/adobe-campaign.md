---
keywords: 电子邮件；电子邮件；电子邮件目标；adobe campaign；campaign
title: Adobe Campaign连接
description: Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 3%

---

# Adobe Campaign连接

## 概述 {#overview}

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。 请参阅 [Campaign Classic入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 以了解更多信息。

要将受众数据发送到Adobe Campaign，您必须首先 [连接目标](#connect-destination) 在Adobe Experience Platform中，然后 [设置数据导入](#import-data-into-campaign) 从存储位置移至Adobe Campaign。

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

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
* **[!UICONTROL 包含SSH密钥的SFTP]**
* **[!UICONTROL Azure Blob]**

将数据发送到Adobe Campaign的首选方法是通过 [!DNL Amazon S3] 或 [!DNL Azure Blob].

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* 对象 **[!UICONTROL Amazon S3]** 连接，您必须提供 [!UICONTROL 访问密钥ID] 和 [!UICONTROL 访问密钥].
* 对象 **[!UICONTROL 包含密码的SFTP]** 连接，您必须提供 [!UICONTROL 域]， [!UICONTROL 端口]， [!UICONTROL 用户名]、和 [!UICONTROL 密码].
* 对象 **[!UICONTROL 包含SSH密钥的SFTP]** 连接，您必须提供 [!UICONTROL 域]， [!UICONTROL 端口]， [!UICONTROL 用户名]、和 [!UICONTROL SSH密钥].
* 对象 **[!UICONTROL Azure Blob]** 连接，必须提供连接字符串。
* 或者，您可以附加RSA格式的公钥，将带有PGP/GPG的加密添加到导出文件中的 **[!UICONTROL 键]** 部分。 您的公钥必须编写为 [!DNL Base64] 编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* **[!UICONTROL 存储段名称]**： *对于S3连接*. 输入S3存储段的位置 [!DNL Platform] 会将您的导出数据另存为CSV文件。
* **[!UICONTROL 文件夹路径]**：提供存储位置中的路径，其中 [!DNL Platform] 会将您的导出数据另存为CSV文件。
* **[!UICONTROL 容器]**： *对于Blob连接*. 包含文件夹路径所在的Blob的容器。
* **[!UICONTROL 文件格式]**：选择 **CSV** 以将CSV文件导出到存储位置。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}


请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从 [合并架构](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关更多信息，请参阅 [将受众激活到电子邮件营销目标的最佳实践](overview.md#best-practices).

## 导出的数据 {#exported-data}

对象 [!DNL Adobe Campaign] 目标， [!DNL Platform] 创建 `.csv` 文件存储位置。 有关这些文件的详细信息，请参见 [验证受众激活](../../ui/activate-batch-profile-destinations.md#verify) 在audience activation教程中。

## 设置数据导入Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 请记住 [!DNL SFTP] 在执行此集成时，根据Adobe Campaign合同中的存储限制、数据库存储限制和活动配置文件限制。
>* 您需要使用以下方式在Adobe Campaign中计划、导入和映射导出的区段 [!DNL Campaign] 工作流。 请参阅 [设置循环导入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 在Adobe Campaign Classic文档和 [关于数据管理活动](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) 在Adobe Campaign Standard文档中。
>* 将数据发送到Adobe Campaign的首选方法是通过 [!DNL Amazon S3] 或 [!DNL Azure Blob].

连接后 [!DNL Platform] 敬您的 [!DNL Amazon S3] 或 [!DNL Azure Blob] 时，您必须设置数据从存储位置导入Adobe Campaign的过程。 要了解如何完成此操作，请参阅以下Adobe Campaign文档页面：
* [数据导入和导出入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans) 和 [数据加载（文件）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 请参阅Adobe Campaign Classic文档。
* [流程和数据管理入门](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和 [加载文件](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 请参阅Adobe Campaign Standard文档。
