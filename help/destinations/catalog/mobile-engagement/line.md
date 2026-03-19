---
keywords: 移动设备；移动参与目标；LINE；LINE移动参与目标
title: LINE连接
description: LINE目标允许您向Experience Platform受众添加配置文件，并为连接的用户提供个性化体验。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 3%

---

# [!DNL LINE]连接

## 概述 {#overview}

[[!DNL LINE]](https://line.me/en/)是一个连接人员、服务和信息的常用通信平台，已从聊天应用发展为娱乐、社交和日常活动的中心。

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)利用[[!DNL LINE] 消息传送API](https://developers.line.biz/en/reference/messaging-api/)。 您可以在[!DNL LINE]内激活来自Experience Platform受众的配置文件作为连接，以满足您的业务需求。

[!DNL LINE]使用持有者令牌作为与[!DNL LINE]消息传送API通信的身份验证机制。 下面在[!DNL LINE]向目标身份验证[部分中进一步提供了向您的](#authenticate)实例进行身份验证的说明。

## 用例 {#use-cases}

作为营销人员，您可以在[!DNL Adobe Experience Platform]中内置受众的移动参与目标中定位用户。 此外，一旦在[!DNL Adobe Experience Platform]中更新了受众和配置文件，即可根据其[!DNL Adobe Experience Platform]配置文件中的属性向他们提供个性化体验。

## 先决条件 {#prerequisites}

### [!DNL LINE]先决条件 {#prerequisites-destination}

注意[!DNL LINE]中的以下先决条件，以将数据从Experience Platform导出到您的[!DNL LINE]帐户：

#### 您需要拥有[!DNL LINE]帐户 {#prerequisites-account}

如果您还没有帐户，则需要注册并创建一个[!DNL LINE]帐户。 要创建帐户，请执行以下操作：

1. 导航到[!DNL LINE] [帐户登录](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F)页面
2. 选择 **[!UICONTROL Create an account]**。

#### 从[!DNL LINE channel access token (long-lived)]开发人员控制台收集[!DNL LINE] {#gather-credentials}

要允许Experience Platform访问[!DNL LINE]资源，您需要从所需的&#x200B;*[!DNL Channel access token (long-lived)]* [!DNL LINE]消息传送API *渠道获取*。

1. 使用您的[!DNL LINE]帐户登录到[[!DNL LINE] 开发人员控制台](https://developers.line.biz/console)。
1. 接下来，访问&#x200B;*[!DNL Providers]*&#x200B;列表，然后选择感兴趣的&#x200B;*[!DNL Provider]*，最后选择&#x200B;*消息传送API*&#x200B;渠道以访问其设置。 如果您是首次访问开发人员控制台，请按照[[!DNL LINE] 文档](https://developers.line.biz/en/docs/messaging-api/getting-started/)完成创建提供程序所需的步骤。
1. 最后，导航到&#x200B;***[!DNL Channel access token]***&#x200B;部分并复制&#x200B;***[!DNL Channel access token (long-lived)]***&#x200B;向目标进行身份验证[步骤中所需的](#authenticate)值。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的[!DNL LINE Channel access token (long-lived)]。 | `aaa2112XSMWqLXR7..........nyilFU=` |

有关通过[[!DNL LINE] 开发人员控制台创建渠道或将渠道添加到现有](https://developers.line.biz/en/docs/messaging-api/getting-started/)帐户的指导，请参阅[!DNL LINE]文档[!DNL LINE]。

## 支持的身份 {#supported-identities}

[!DNL LINE]支持更新和导出下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 |
|---|---|
| 广告商ID(IFA) | 当源标识为IFA *（广告商的Apple ID）*&#x200B;或GAID *(Google Advertising ID)命名空间时，选择广告商(IFA)目标标识的ID。 |
| 行用户ID | 当源标识为LINE用户ID时，选择UserID目标标识。 |

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 否 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 在其他Experience Platform应用程序（如Adobe Journey Optimizer）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在Adobe Experience Platform数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出具有[!DNL LINE]目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;内，搜索[!DNL LINE]。 或者，您可以在&#x200B;**[!UICONTROL Mobile engagement]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

要验证目标，请选择&#x200B;**[!UICONTROL Connect to destination]**。
![Experience Platform UI屏幕截图显示如何进行身份验证。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填写下面的必填字段。

* **[!UICONTROL Bearer token]**：从[!DNL LINE Channel access token (long-lived)]开发人员控制台中[!DNL LINE]。 请参阅[收集凭据](#gather-credentials)部分。

如果提供的详细信息有效，则UI会显示&#x200B;**[!UICONTROL Connected]**&#x200B;状态并显示绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Experience Platform UI屏幕截图显示目标详细信息。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Audience Type]**：如果您要导出的标识为广告商(IFA)**[!UICONTROL ID for Advertisers(IFAs)]**&#x200B;的&#x200B;*ID类型，请选择*。 如果要导出的标识的类型为&#x200B;**[!UICONTROL LINE user IDs]** LINE用户ID *，请选择*。 有关身份类型的详细信息，请参阅[支持的身份](#supported-identities)部分。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

要将受众数据从Adobe Experience Platform正确发送到[!DNL LINE]目标，您需要完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到[!DNL LINE]目标字段，请执行以下步骤：

根据您的源身份，必须映射以下目标身份命名空间：

| 目标身份 | 源字段 | 目标字段 |
| --- | --- | --- |
| 广告商ID(IFA) | `IDFA` 或 `GAID` | `LineId` |
| 行用户ID | `UserID` | `LineId` |

{style="table-layout:auto"}

如果您的目标身份是&#x200B;*LINE用户ID的*，则需要以下项：
![Experience Platform UI屏幕截图示例，显示将LINE用户ID用于Target身份时的Target映射。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果您的目标标识是广告商(IFA)*的*ID，则需要以下项：
![Experience Platform UI屏幕截图示例，显示将ID用于Advertisers (IFAs)作为Target标识时的Target映射。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 验证数据导出 {#exported-data}

成功从Experience Platform导出数据后，[!DNL LINE]目标将使用所选受众名称在[!DNL LINE]内创建新受众。

要验证您是否正确设置了目标，请执行以下步骤：

1. 在[!DNL LINE]中，登录到[管理器控制台](https://manager.line.biz/)。

1. 接下来，导航到&#x200B;**[!UICONTROL Data Controls]** > **[!UICONTROL Audiences]**，并在&#x200B;**[!UICONTROL Audience name]**&#x200B;列中检查与所选受众匹配的名称。

1. 更新的卷将匹配区段中的计数。

1. 如果您导出的标识的类型为&#x200B;*UserID*，则&#x200B;**[!UICONTROL UserID]** Type *列将提及*。 同样，如果您导出的标识的类型为&#x200B;*IDFA*，则&#x200B;**[!UICONTROL Mobile ad Id]** Type *列将提及*。

[!DNL LINE]中的示例设置如下所示：
![LINE UI屏幕截图显示受众数量。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
