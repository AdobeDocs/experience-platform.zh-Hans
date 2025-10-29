---
title: RainFocus与会者个人资料
description: 了解如何使用RainFocus与会者个人资料目标连接器，将受众个人资料与RainFocus全球与会者个人资料同步。
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 5%

---

# RainFocus与会者个人资料 {#rainfocus-destination}

## 概述 {#overview}

使用[!DNL RainFocus Attendee Profiles]目标将客户轮廓从 Adobe Experience Platform 传输到[!DNL RainFocus]平台，以创建和更新与会者轮廓。

>[!IMPORTANT]
>
>目标连接器和文档页面由[!DNL RainFocus]团队创建和维护。 如有任何查询或更新请求，请直接通过`clientcare@rainfocus.com`联系他们，或访问RainFocus [帮助中心](https://help.rainfocus.com/hc/en-us)。

## 用例 {#use-cases}

为了帮助您更好地了解您应当如何以及何时使用RainFocus目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

一家大型企业技术公司即将为其即将召开的全球博览会开放注册，并希望将客户配置文件推送到[!DNL RainFocus]以简化注册流程。

### 用例#2 {#use-case-2}

一家金融服务品牌即将举办一系列面向新客户和现有客户的路演。 他们与Adobe Experience Platform中的目标客户存在一系列受众区段。 使用[!DNL RainFocus]目标连接器，他们能够轻松地将这些配置文件发送到[!DNL RainFocus]进行激活。

## 先决条件 {#prerequisites}

在使用[!DNL RainFocus]目标之前，请确保满足以下先决条件：

* 使用OAuth（全局）创建[!DNL RainFocus] API配置文件。
   * 必须启用&#x200B;**Attendee Store**&#x200B;终结点。
   * 需要生成&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**。

您还必须具有RainFocus **事件代码**&#x200B;标识符，您希望将用户档案发送到该标识符。

## 支持的身份 {#supported-identities}

[!DNL RainFocus]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

![提供RainFocus目标连接器的身份验证详细信息](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**：填写由RainFocus API配置文件提供的[!DNL Client ID]。
* **[!UICONTROL Client secret]**：填写由RainFocus API配置文件提供的[!DNL Client Secret]。
* **[!UICONTROL Environment]**：指定您要连接到的RainFocus环境，例如`dev`、`prod`。
* **[!UICONTROL Org ID]**：为您的RainFocus实例提供唯一的`orgid`。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![提供RainFocus目标连接器的连接详细信息](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Event ID]**：您的[!DNL RainFocus]事件代码标识符，您希望将配置文件发送到该标识符。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

必须根据用例映射以下目标身份命名空间：

* **电子邮件**&#x200B;必须使用&#x200B;**目标字段>选择身份命名空间>电子邮件**&#x200B;映射为目标字段

![如何映射配置文件和标识字段](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

建议映射其他配置文件字段，因为这将确保完全填充[!DNL RainFocus]中的与会者配置文件。 [!DNL RainFocus]中提供了以下目标字段：

| 目标字段 | 描述 |
|------------|-------------|
| `address1` | 街道地址的第一行 |
| `address2` | 街道地址的第二行（如果适用） |
| `city` | 城市名称 |
| `companyname` | 公司的名称 |
| `countryid` | 国家的ISO 3166-1 alpha-2国家/地区代码标识符 |
| `email` | 电子邮件地址 |
| `firstname` | 人员的名字 |
| `lastname` | 人员的姓氏 |
| `jobtitle` | 人员职务 |
| `phone` | 电话号码 |
| `state` | 省/市/自治区的FIPS省/市/自治区字母代码 |
| `zip` | 邮政编码 |

{style="table-layout:auto"}

## 导出的数据/验证数据导出 {#exported-data}

将一组配置文件发送到[!DNL RainFocus]后，使用[!DNL RainFocus]中的API配置文件日志记录验证配置文件是否已成功摄取。

在RainFocus中查看API配置文件中的![日志](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![验证配置文件是否已成功摄取](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

* [RainFocus流Source连接器](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/analytics/rainfocus)
