---
title: twitter自定义受众连接
description: 在Twitter中定位现有关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences] 连接

## 概述 {#overview}

在Twitter中定位现有关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动。

## 先决条件 {#prerequisites}

配置之前 [!DNL Twitter Custom Audiences] 目标，请确保查看您需要满足的以下Twitter先决条件。

1. 您的 [!DNL Twitter Ads] 帐户必须符合广告条件。 新建 [!DNL Twitter Ads] 帐户在创建后的前2周内没有资格进行广告。
2. 您在中授权访问的Twitter用户帐户 [!DNL Twitter Audience Manager] 必须具有 *[!DNL Partner Audience Manager]* 权限已启用。

## 支持的身份 {#supported-identities}

[!DNL Twitter Custom Audiences] 支持激活下表中描述的标识。 了解有关 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支持Google Advertising ID (GAID)和广告商Apple ID (IDFA)。 请在中相应地映射源架构中的这些命名空间和/或属性 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目标激活工作流的。 |
| 电子邮件 | 用户的电子邮件地址 | 请将纯文本电子邮件地址和SHA256散列电子邮件地址映射到此字段。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 如果您在上传到Adobe Experience Platform之前对客户电子邮件地址进行了哈希处理，请注意，必须使用SHA256对这些身份进行哈希处理，而不需使用Salt。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Twitter自定义受众目标中所用标识符的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Twitter Custom Audiences] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

在Twitter中定位现有关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动，作为 [!DNL List Custom Audiences] twitter中。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

1. 查找 [!DNL Twitter Custom Audiences] 目标目录中的目标并选择 **[!UICONTROL 设置]**.
2. 选择 **[!UICONTROL 连接到目标]**.
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 输入Twitter凭据并选择 **登录**.

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帐户 ID"
>abstract="您的 Twitter 广告帐户 ID。可以在 Twitter 广告设置中找到它。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 [!DNL Twitter Ads] 帐户ID。 您可在以下位置找到该链接： [!DNL Twitter Ads] 设置。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

将受众映射到Twitter时，请确保满足以下受众命名要求：

1. 提供易于用户识别的受众映射名称。 我们建议使用与Experience Platform区段相同的名称。
2. 请勿使用特殊字符(+ &amp; ， % ： ； @ / = ？ $)。 如果您的Experience Platform受众名称包含这些字符，请先删除这些字符，然后再将受众映射到Twitter目标。

有关以下内容的更多信息 [!DNL List Custom Audiences] 中的Twitter可在以下位置找到： [twitter文档](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
