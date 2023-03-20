---
title: TikTok连接
description: 在TikTok上使用您的数据构建自定义受众，以便通过广告营销活动进行定位。 这些受众可以是访问您的网站或与您的内容进行交互的人员。 使用Adobe与TikTok Ads Manager的实时集成，快速、安全地将所需的区段从Adobe Experience Platform推送到TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# TikTok连接

## 概述 {#overview}

在TikTok上使用您的数据构建自定义受众，以便通过广告营销活动进行定位。 这些受众可以是访问您的网站或与您的内容进行交互的人员。 使用Adobe与TikTok Ads Manager的实时集成，快速、安全地将所需的区段从Adobe Experience Platform推送到TikTok。 访问 [TikTok业务帮助中心](https://ads.tiktok.com/help/article/audiences?lang=en) 以了解更多信息。

>[!IMPORTANT]
>
>此文档页面由TikTok团队创建。 如有任何查询或更新请求，请直接联系 [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用TikTok目标，以下是Adobe Experience Platform客户的示例用例。

### 用例 {#use-case-1}

一家运动服装品牌希望通过其社交媒体帐户联系现有客户。 该服装品牌可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建区段，并将这些区段发送到TikTok，以在其客户的社交媒体信息源中显示广告。

## 先决条件 {#prerequisites}

在将数据发送到 [!DNL TikTok Ads Manager] 帐户，您需要授予Adobe Experience Platform访问您的广告帐户的权限 `Audience Management`. 可以通过在Experience Platform中输入广告商ID并在重定向后授予权限来提供此权限。 您可以在 [TikTok API文档](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 支持的身份 {#supported-identities}

TikTok支持激活下表中描述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |
| 电话号码 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码，并且它们必须采用E.164格式。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| 电子邮件 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，以及TikTok目标中使用的标识符（名称、电话号码或其他）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，您将被重定向以登录到 [!DNL TikTok Ads Manager] 帐户并授权Adobe代表您管理受众。

![TikTok权限选择](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用于选择权限的TikTok UI图像")

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标连接详细信息](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "平台UI的图像，显示要填充的目标连接详细信息")

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL TikTok Ads Manager ID]**:您的 [!DNL TikTok Ads Manager ID]. 您可以在 [!DNL TikTok Ads manager] 帐户。

![TikTok Ads Manager ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok广告管理器UI的图像，显示如何获取TikTok广告管理器ID")

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射身份 {#map}

以下是将区段导出到TikTok Ads Manager时正确标识映射的示例。

选择源字段：

* 选择标识符(例如：` Email_LC_SHA256`)作为源标识，用于唯一标识Adobe Experience Platform中的用户档案和 [!DNL TikTok Ads Manager].

选择目标字段：

* 选择电子邮件命名空间作为目标标识。

![身份映射](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "平台UI的图像，身份映射")

## 导出的数据 {#exported-data}

检查 [!DNL TikTok Ads Manager] 帐户(在 **资产>受众**)来验证您的Experience Platform区段是否已成功导出。 受众将以受众类型填充： `Partner Audience`.

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

请参阅 [TikTok帮助中心页面](https://ads.tiktok.com/help/article/audiences?lang=en) 以了解其他信息。
