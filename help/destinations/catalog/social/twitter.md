---
title: Twitter Custom Audiences连接
description: 通过激活在Twitter中构建的受众，定位您的现有关注者和客户，并创建相关的再营销活动
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# [!DNL Twitter Custom Audiences] 连接

## 概述 {#overview}

通过激活在Twitter中构建的受众，定位您的现有关注者和客户，并创建相关的再营销活动。

## 先决条件 {#prerequisites}

在配置之前 [!DNL Twitter Custom Audiences] 目标，请确保查看您需要满足的以下Twitter先决条件。

1. 您的 [!DNL Twitter Ads] 帐户必须符合广告资格。 新建 [!DNL Twitter Ads] 帐户在创建后头2周内没有资格获得广告。
2. 您授权在中访问的Twitter用户帐户 [!DNL Twitter Audience Manager] 必须具有 *[!DNL Partner Audience Manager]* 权限启用。

## 支持的身份 {#supported-identities}

[!DNL Twitter Custom Audiences] 支持激活下表所述的身份。 详细了解 [标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支持Google广告ID(GAID)和Apple ID for Advertisers(IDFA)。 请在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目标激活工作流的URL。 |
| 电子邮件 | 用户的电子邮件地址 | 请将纯文本电子邮件地址和SHA256哈希电子邮件地址映射到此字段。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 如果您在将客户电子邮件地址上传到Adobe Experience Platform之前对其进行哈希处理，请注意，这些身份必须使用SHA256进行哈希处理，而不必加任何盐。 |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及在Twitter自定义受众目标中使用的标识符。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL Twitter Custom Audiences] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

通过激活在Twitter中构建的受众(如 [!DNL List Custom Audiences] 在Twitter。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

1. 查找 [!DNL Twitter Custom Audiences] 目标目录中的目标，然后选择 **[!UICONTROL 设置]**.
2. 选择 **[!UICONTROL 连接到目标]**.
   ![验证LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 输入Twitter凭据并选择 **登录**.

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帐户 ID"
>abstract="您的 Twitter 广告帐户 ID。可以在 Twitter 广告设置中找到它。"

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Twitter Ads] 帐户ID。 这可在 [!DNL Twitter Ads] 设置。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

将受众区段映射到Twitter时，请确保满足以下区段命名要求：

1. 提供人类可读的区段映射名称。 我们建议您使用与Experience Platform区段相同的名称。
2. 请勿使用特殊字符（+和、%）：;@ / = ? $)。 如果您的Experience Platform区段名称包含这些字符，请先删除这些字符，然后再将区段映射到Twitter目标。

有关 [!DNL List Custom Audiences] 在Twitter，可以在 [Twitter文档](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
