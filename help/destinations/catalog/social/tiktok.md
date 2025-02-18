---
title: TikTok连接
description: 使用您的数据在TikTok上构建自定义受众，以便通过广告促销活动进行定位。 这些受众可能是访问您的网站或与您的内容进行交互的人。 使用Adobe与TikTok Ads Manager的实时集成，快速而安全地将所需受众从Adobe Experience Platform推送到TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 9a80a9b49b1983e8e488d11b114c02130b045686
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 3%

---

# TikTok连接

## 概述 {#overview}

使用您的数据在TikTok上构建自定义受众，以便通过广告促销活动进行定位。 这些受众可能是访问您的网站或与您的内容进行交互的人。 使用Adobe与TikTok Ads Manager的实时集成，快速而安全地将所需受众从Adobe Experience Platform推送到TikTok。 有关详细信息，请访问[TikTok的业务帮助中心](https://ads.tiktok.com/help/article/audiences)。

>[!IMPORTANT]
>
>此目标连接器和文档页面由TikTok团队创建和维护。 如有任何查询或更新请求，请直接通过[https://ads.tiktok.com/help/](https://ads.tiktok.com/help/)联系他们。

## 用例 {#use-cases}

为了帮助您更好地了解应当如何以及何时使用TikTok目标，以下是Adobe Experience Platform客户的示例用例。

### 用例 {#use-case-1}

一家运动服装品牌希望通过其社交媒体帐户吸引现有客户。 服装品牌可以从自己的CRM中摄取电子邮件地址到Adobe Experience Platform，从自己的离线数据构建受众，并将这些受众发送到TikTok以在其客户的社交媒体馈送中显示广告。

## 先决条件 {#prerequisites}

您需要对要将受众发送到的TikTok广告管理器帐户具有[!DNL Admin]或[!DNL Operator]访问权限。 可在[TikTok帮助中心](https://ads.tiktok.com/help/article/add-users-tiktok-business-center)上找到更多说明。

在将数据发送到您的TikTok广告管理器帐户之前，您需要授予Adobe Experience Platform权限以访问`Audience Management`的广告帐户。 可以通过以下方式提供此权限：[在Experience Platform UI中输入您的广告管理器ID](#authenticate)，并在重定向到您的TikTok广告管理器帐户后授予权限。

## 支持的身份 {#supported-identities}

TikTok支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| 电话号码 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码，并且它们必须采用E.164格式。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| 电子邮件 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |
| [!DNL Federated Audience Composition] | ✓ | 通过[联合受众构成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences)导入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有TikTok目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，您将被重定向以登录到您的[!DNL TikTok Ads Manager]帐户，并授权Adobe代表您管理受众。

![TikTok权限选择](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用于选择权限的TikTok UI图像")

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标连接详细信息](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "平台UI的图像，显示要填写的目标连接详细信息")

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL TikTok广告管理器ID]**：您的[!DNL TikTok Ads Manager ID]。 您可以在[!DNL TikTok Ads manager]帐户中找到此内容。

![TikTok广告管理器ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok广告管理器UI的图像，显示如何获取TikTok广告管理器ID")

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射身份标识 {#map}

下面是将受众导出到TikTok广告管理器时正确标识映射的示例。

选择源字段：

* 选择一个标识符（例如：` Email_LC_SHA256`）作为源标识，该标识符唯一标识Adobe Experience Platform和[!DNL TikTok Ads Manager]中的配置文件。

选择目标字段：

* 选择电子邮件命名空间作为目标标识。

![标识映射](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "平台UI的图像，标识映射")

## 导出的数据 {#exported-data}

检查您的[!DNL TikTok Ads Manager]帐户(位于&#x200B;**Assets >受众**&#x200B;下)以验证是否已成功导出Experience Platform受众。 受众将填充为受众类型： `Partner Audience`。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

请参阅[TikTok帮助中心页面](https://ads.tiktok.com/help/article/audiences)以获取更多信息。
