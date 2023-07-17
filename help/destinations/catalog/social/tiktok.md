---
title: TikTok 连接
description: 使用您的数据在 TikTok 上构建自定义受众，以便针对您的广告营销活动进行定位。这些受众可能是访问您的网站或与您的内容进行交互的人。 使用Adobe与TikTok Ads Manager的实时集成，快速而安全地将所需受众从Adobe Experience Platform推送到TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 5%

---

# TikTok 连接

## 概述 {#overview}

使用您的数据在 TikTok 上构建自定义受众，以便针对您的广告营销活动进行定位。这些受众可能是访问您的网站或与您的内容进行交互的人。 使用Adobe与TikTok Ads Manager的实时集成，快速而安全地将所需受众从Adobe Experience Platform推送到TikTok。 访问 [TikTok的业务帮助中心](https://ads.tiktok.com/help/article/audiences?lang=en) 了解更多信息。

>[!IMPORTANT]
>
>此文档页面由TikTok团队创建。 如有任何查询或更新请求，请直接通过 [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用TikTok目标，以下是Adobe Experience Platform客户的示例用例。

### 用例 {#use-case-1}

一家运动服装品牌希望通过其社交媒体帐户吸引现有客户。 服装品牌可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建受众，并将这些受众发送到TikTok，以在其客户的社交媒体馈送中显示广告。

## 先决条件 {#prerequisites}

将数据发送到您的之前 [!DNL TikTok Ads Manager] 帐户，您需要授予Adobe Experience Platform权限才能访问您的广告帐户 `Audience Management`. 可以通过在Experience Platform中输入您的广告商ID并遵循重定向以授予权限来提供此权限。 欲知更多相关说明，请参见 [TikTok API文档](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 支持的身份 {#supported-identities}

TikTok支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| 电话号码 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码，并且它们必须采用E.164格式。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |
| 电子邮件 | 使用SHA256算法对电子邮件地址进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在使用TikTok目标中使用的标识符（姓名、电话号码或其他）导出受众的所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，您将被重定向以登录 [!DNL TikTok Ads Manager] 帐户并授权Adobe代表您管理受众。

![TikTok权限选择](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用于选择权限的TikTok UI图像")

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标连接详细信息](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Platform UI的图像，显示要填充的目标连接详细信息")

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL TikTok广告管理器ID]**：您的 [!DNL TikTok Ads Manager ID]. 您可以在 [!DNL TikTok Ads manager] 帐户。

![TikTok广告管理器ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok广告管理器UI的图像，显示如何获取TikTok广告管理器ID")

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射身份 {#map}

下面是将受众导出到TikTok广告管理器时正确的标识映射示例。

选择源字段：

* 选择标识符(例如：` Email_LC_SHA256`)作为源标识，用于唯一标识Adobe Experience Platform中的用户档案，并且 [!DNL TikTok Ads Manager].

选择目标字段：

* 选择电子邮件命名空间作为目标标识。

![标识映射](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Platform UI的图像，标识映射")

## 导出的数据 {#exported-data}

检查您的 [!DNL TikTok Ads Manager] 帐户(在 **Assets >受众**)，以验证您的Experience Platform受众是否已成功导出。 受众将填充为受众类型： `Partner Audience`.

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据治理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

请参阅 [TikTok帮助中心页面](https://ads.tiktok.com/help/article/audiences?lang=en) 以获取其他信息。
