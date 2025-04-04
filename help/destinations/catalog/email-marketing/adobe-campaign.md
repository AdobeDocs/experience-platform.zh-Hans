---
keywords: 电子邮件；电子邮件；电子邮件目标；adobe campaign；campaign
title: Adobe Campaign连接
description: Adobe Campaign 是一套可以帮助您跨所有线上和线下渠道定制和投放营销活动的解决方案。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 4%

---

# Adobe Campaign连接

## 概述 {#overview}

Adobe Campaign是一套解决方案，可帮助您在所有线上和线下渠道个性化和交付营销活动。 有关详细信息，请参阅[Campaign Classic入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)。

若要将受众数据发送到Adobe Campaign，您必须先[连接到Adobe Experience Platform中的目标](#connect-destination)，然后[设置数据导入](#import-data-into-campaign)(从您的存储位置导入Adobe Campaign)。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## IP地址允许列表 {#allow-list}

在使用SFTP存储设置电子邮件营销目标时，Adobe建议将某些IP范围添加到SFTP允许列表。

如果您需要将Adobe 列入允许列表 IP添加到SFTP允许列表，请参阅[SFTP目标的IP地址](../cloud-storage/ip-address-allow-list.md)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

Adobe Campaign支持以下连接类型：

* **[!UICONTROL Amazon S3]**
* 使用密码&#x200B;**[!UICONTROL SFTP]**
* 使用SSH密钥的&#x200B;**[!UICONTROL SFTP]**
* **[!UICONTROL Azure Blob]**

将数据发送到Adobe Campaign的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* 对于&#x200B;**[!UICONTROL Amazon S3]**&#x200B;连接，您必须提供您的[!UICONTROL 访问密钥ID]和[!UICONTROL 访问密钥]。
* 对于使用密码&#x200B;]**连接的**[!UICONTROL  SFTP，您必须提供[!UICONTROL 域]、[!UICONTROL 端口]、[!UICONTROL 用户名]和[!UICONTROL 密码]。
* 对于具有SSH密钥&#x200B;]**连接的**[!UICONTROL  SFTP，您必须提供[!UICONTROL 域]、[!UICONTROL 端口]、[!UICONTROL 用户名]和[!UICONTROL SSH密钥]。
* 对于&#x200B;**[!UICONTROL Azure Blob]**&#x200B;连接，必须提供连接字符串。
* 或者，您可以附加RSA格式的公钥，以将使用PGP/GPG的加密添加到&#x200B;**[!UICONTROL 密钥]**&#x200B;部分下的导出文件。 您的公钥必须编写为[!DNL Base64]编码字符串。
* **[!UICONTROL 名称]**：为您的目标选择相关的名称。
* **[!UICONTROL 描述]**：输入目标的描述。
* 对于S3连接&#x200B;*，**[!UICONTROL 存储段名称]**：*。 输入S3存储段的位置，[!DNL Experience Platform]会将您的导出数据存为CSV文件。
* **[!UICONTROL 文件夹路径]**：提供存储位置中的路径，其中[!DNL Experience Platform]会将导出数据存为CSV文件。
* **[!UICONTROL 容器]**：用于Blob连接的&#x200B;**。 包含文件夹路径所在的Blob的容器。
* **[!UICONTROL 文件格式]**：选择&#x200B;**CSV**&#x200B;以将CSV文件导出到您的存储位置。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}


有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

### 目标属性 {#destination-attributes}

将受众激活到此目标时，Adobe建议您从[合并架构](../../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择要导出到目标的唯一标识符和任何其他XDM字段。 有关详细信息，请参阅将受众激活到电子邮件营销目标时的最佳实践[](overview.md#best-practices)。

## 导出的数据 {#exported-data}

对于[!DNL Adobe Campaign]目标，[!DNL Experience Platform]会在您提供的存储位置中创建一个`.csv`文件。 有关这些文件的详细信息，请参阅Audience Activation教程中的[验证Audience Activation](../../ui/activate-batch-profile-destinations.md#verify)部分。

## 设置数据导入Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 在执行此集成时，请记住Adobe Campaign合同规定的[!DNL SFTP]存储限制、数据库存储限制和活动配置文件限制。
>* 您需要使用[!DNL Campaign]工作流在Adobe Campaign中计划、导入和映射导出的区段。 请参阅Adobe Campaign Classic文档中的[设置定期导入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html)和Adobe Campaign Standard文档中的[关于数据管理活动](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html)。
>* 将数据发送到Adobe Campaign的首选方法是通过[!DNL Amazon S3]或[!DNL Azure Blob]。

将[!DNL Experience Platform]连接到[!DNL Amazon S3]或[!DNL Azure Blob]存储空间后，您必须设置数据从存储位置导入Adobe Campaign。 要了解如何完成此操作，请参阅以下Adobe Campaign文档页面：
* [数据导入和导出入门](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hans)和Adobe Campaign Classic文档中的[数据加载（文件）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html)。
* [开始使用流程和数据管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html)和[在Adobe Campaign Standard文档中加载文件](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html)。
