---
title: Twitter自定义受众连接
description: 在Twitter中锁定您现有的关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences]连接

## 概述 {#overview}

在Twitter中定位现有的关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动。

## 先决条件 {#prerequisites}

在配置[!DNL Twitter Custom Audiences]目标之前，请确保查看需要满足的以下Twitter先决条件。

1. 您的[!DNL Twitter Ads]帐户必须符合广告条件。 新[!DNL Twitter Ads]帐户在创建后的前2周内没有资格广告。
2. 您在[!DNL Twitter Audience Manager]中授权访问的Twitter用户帐户必须启用&#x200B;*[!DNL Partner Audience Manager]*&#x200B;权限。

## 支持的标识 {#supported-identities}

[!DNL Twitter Custom Audiences]支持激活下表所述的标识。 详细了解[标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans#getting-started)。

| 目标标识 | 描述 | 考虑事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支持Google广告ID (GAID)和广告商Apple ID (IDFA)。 请在目标激活工作流程的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中从源架构相应地映射这些命名空间和/或属性。 |
| 电子邮件 | 用户的电子邮件地址 | 请将纯文本电子邮件地址和SHA256散列电子邮件地址映射到此字段。 如果源字段包含未哈希处理的属性，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时让[!DNL Experience Platform]自动哈希数据。 如果您在将客户电子邮件地址上传到Adobe Experience Platform之前对其进行散列，请注意，必须使用SHA256来散列这些身份，无需使用盐。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 访问群体[已将](../../../segmentation/ui/audience-portal.md#import-audience)从CSV文件导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您将导出受众的所有成员及其“Twitter自定义受众”目标中使用的标识符。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流式传输目标为基于API的“始终打开”连接。 一旦基于受众评估在Experience Platform中更新了配置文件，连接器将更新向下游发送到目标平台。 阅读有关[流式传输目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用[!DNL Twitter Custom Audiences]目标，以下是Adobe Experience Platform客户可以使用此目标来解决的示例用例。

### 用例#1

在Twitter中将您现有的关注者和客户作为目标，并将您在Adobe Experience Platform中构建的受众激活为Twitter中的[!DNL List Custom Audiences]，以创建相关的再营销活动。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流程中，填写下面两部分列出的字段。

### 验证目标 {#authenticate}

1. 在目标目录中查找[!DNL Twitter Custom Audiences]目标并选择&#x200B;**[!UICONTROL Set Up]**。
2. 选择 **[!UICONTROL Connect to destination]**。
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 输入您的Twitter凭据，然后选择&#x200B;**登录**。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帐户 ID"
>abstract="您的 Twitter 广告帐户 ID。可以在 Twitter 广告设置中找到它。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Account ID]**：您的[!DNL Twitter Ads]帐户ID。 可在你的[!DNL Twitter Ads]设置中找到此项。

>[!IMPORTANT]
>
>请勿使用特殊字符(+ &amp; ， % ： ； @ / = ？ $ \n)（受众、描述和受众映射名称中）。 如果您的Experience Platform受众名称包含这些字符，请在将受众映射到Twitter目标之前删除它们。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的标识命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的标识命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射注意事项 {#mapping-considerations}

将受众映射到Twitter时，请提供易于读取的受众映射名称。 我们建议使用与Experience Platform段相同的名称。

## 数据使用和管理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何强制执行数据治理的详细信息，请参阅[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。

## 其他资源 {#additional-resources}

有关Twitter中[!DNL List Custom Audiences]的详细信息，可在[Twitter文档](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)中找到。
