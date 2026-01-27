---
title: 索引交换
description: 连接到Index Exchange （索引）并激活您的数据，以便您的受众区段可以通过在索引UI中创建的交易定位。
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---


# [!DNL Index Exchange] {#index-exchange}

## 概述 {#overview}

[!DNL Index]是一个全球广告供应方平台，可帮助媒体所有者最大限度地实现其内容在每个屏幕上的价值。 凭借超过20年的行业领先地位，[!DNL Index]将世界上最大的品牌与高级体验制作者联系起来，以提供高质量的消费者体验。

使用此目标连接器将受众区段直接从Adobe Experience Platform导出到[!DNL Index Exchange]的程序化广告平台。

导出后，这些受众区段可用于定位媒体所有者、市场合作伙伴或市场供应商与发布者和策划人共享的交易内容。

>[!IMPORTANT]
>
>目标连接器和文档页面由[!DNL Index]团队创建和维护。 如有疑问或更新请求，请直接通过[technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com)与他们联系。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Index Exchange]目标，以下是Experience Platform客户可以使用此目标解决的示例用例。

### 在移动、Web和CTV平台上定位用户 {#targeting-users}

希望使用大量标识符将受众从Experience Platform发送到[!DNL Index]以定位移动、Web和CTV平台上的用户的媒体所有者、市场合作伙伴或市场供应商。

### 在移动、Web和CTV平台上定位特定内容 {#targeting-content}

希望将受众从Experience Platform发送到[!DNL Index]的媒体所有者、市场合作伙伴或市场供应商，以及使用特定URL、应用程序包或内容ID定位在移动设备、Web和CTV平台上查看特定内容的用户。

## 先决条件 {#prerequisites}

使用此目标时，必须使用其他进程向[!DNL Index]注册受众区段，然后才能在帐户中显示受众区段。 请联系您的[!DNL Index Exchange]客户代表以获得此流程的相关帮助。

## 支持的身份 {#supported-identities}

[!DNL Index]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

请注意，[!DNL Index Exchange]目标在每个上载中仅支持一种标识类型。 配置目标详细信息时，必须指定适当的标识符类型（请参阅下面的[“填写目标详细信息”](#destination-details)部分）。

要上载多个标识类型，请为每个标识类型创建[!DNL Index Exchange]目标的单独实例。

| 目标身份 | 描述 | 注意事项 |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | 如果源身份是GAID命名空间，请选择GAID作为目标身份。 |
| IDFA | 广告商的Apple ID | 如果您的源身份是IDFA命名空间，请选择IDFA目标身份。 |
| Windows AID | Windows Advertising ID | 如果源标识是Windows AID命名空间，请选择Windows AID目标标识。 |
| extern_id | 自定义用户标识 | 如果您的源身份是自定义命名空间，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些受众类型可以导出到此目标。

| 受众来源 | 支持 | 描述 |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
| --------- | ---------- | --------- | 
| 导出类型 | **[!UICONTROL Segment export]** | 使用[!DNL Index Exchange]目标中使用的标识符（IDFA、GAID或其他）导出区段（受众）的所有成员。 |
| 导出频率 | **[!UICONTROL Batch]** | 以3、6、8、12或24小时的时间间隔将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]：输入一个名称以帮助您以后识别此目标。
* [!UICONTROL Description]：输入描述以帮助您以后识别此目标。
* [!UICONTROL Identifier Type]：选择与要发送给[!DNL Index]的标识符匹配的索引提供的标识符类型。 请参阅下表支持的标识符类型。 如果不确定要使用哪种标识符类型，请联系您的[!DNL Index]代表。 要发送多种标识符类型，请为此目标创建单独的实例。
* [!UICONTROL Account ID]：输入您的[!DNL Index]帐户ID。 这与您的发布者ID不同。 如果您不确定要使用哪个ID，请联系您的[!DNL Index]代表。

#### 支持的标识符类型

| 标识符类型 | 描述 |
|------------------ | ------------- |
| [!DNL appbundle] | 移动应用程序捆绑包 |
| [!DNL contentid] | 内容Id |
| [!DNL deviceid] | 设备ID(例如 IDFA、GAID、WAID等) |
| [!DNL ip] | IP地址 |
| [!DNL postcode] | 邮政编码 |
| [!DNL url] | 站点URL |
| [!DNL ppid_xxx] | 有关PPID标识符，请联系您的[!DNL Index Exchange]帐户代表寻求帮助。 |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关此目标数据流状态的通知。 从列表中选择一个或多个警报以订阅数据流的状态通知。 有关详细信息，请参阅[使用UI订阅目标警报指南](../../ui/alerts.md)。
完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众区段激活到此目标的说明，请阅读[将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 映射属性和身份 {#map}

选择源字段：

* 选择标识符（通常是IDFA或自定义ID命名空间等命名空间）。 这必须对应于配置目标时选择的标识符类型。 例如，将IDFA标识符用作源字段时，目标必须已设置“deviceid”标识符类型。

选择目标字段：

* 目标字段的名称将被忽略，并且并不重要。 目标只关心所发送的标识符的类型，该类型由配置目标时选择的标识符类型确定。

![映射属性和标识](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### 向[!DNL Index]注册区段 {#register-segments}

将数据激活到目标之前或之后，请联系您的[!DNL Index]代表以注册您计划激活的区段。 您的代表将提供如何注册其他区段详细信息（包括名称、ID、描述和定价，如果适用）的说明。

## 导出的数据/验证数据导出 {#exported-data}

注册完成后，区段将可用于在您的[!DNL Index]帐户中进行定位。 要确认正确接收了数据，请联系您的[!DNL Index]代表，该代表可提供所接收区段数据量的详细信息。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有Experience Platform目标都符合数据使用策略。 有关Experience Platform如何实施数据治理的详细信息，请阅读[数据管理概述](/help/data-governance/home.md)。
