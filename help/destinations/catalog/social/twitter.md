---
title: Twitter自定义受众连接
description: 在Twitter中定位现有的关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 5b529a1af62c2745c3226029de1a1ff508bddfc7
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 6%

---

# [!DNL Twitter Custom Audiences]连接

## 概述 {#overview}

>[!IMPORTANT]
>
>* 从2025年9月9日开始，您可以在目标目录中并排看到两张&#x200B;**[!DNL Twitter Custom Audiences]**&#x200B;卡。 这是由于目标服务内部升级造成的。现有的&#x200B;**[!DNL Twitter Custom Audiences]**&#x200B;目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用） Twitter自定义受众]**，现在您可以使用名为&#x200B;**[!UICONTROL Twitter自定义受众]**&#x200B;的新信息卡。
>* 在目录中使用新的&#x200B;**[!UICONTROL Twitter自定义受众]**&#x200B;连接获取新的激活数据流。 如果您有任何到&#x200B;**[!UICONTROL （已弃用） Twitter自定义受众]**&#x200B;目标的活动数据流，则会自动更新，因此您无需执行任何操作。
>* 如果您是通过[流服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/)创建数据流，则必须将[!DNL flow spec ID]和[!DNL connection spec ID]更新为以下值：
>   * 流量规范 ID：`903da9e4-7cf5-442a-9498-a237e4f064f9`
>   * 连接规范 ID：`9eb18875-a095-4b89-854e-39b9e29ccd41`

在Twitter中定位现有的关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动。

## 先决条件 {#prerequisites}

在配置[!DNL Twitter Custom Audiences]目标之前，请确保查看需要满足的以下Twitter先决条件。

1. 您的[!DNL Twitter Ads]帐户必须适用于广告。 新[!DNL Twitter Ads]帐户在创建后的前2周内没有资格进行广告。
2. 您在[!DNL Twitter Audience Manager]中授权访问的Twitter用户帐户必须已启用&#x200B;*[!DNL Partner Audience Manager]*&#x200B;权限。

## 支持的身份 {#supported-identities}

[!DNL Twitter Custom Audiences]支持激活下表中描述的标识。 了解有关[标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支持Google Advertising ID (GAID)和广告商Apple ID (IDFA)。 请在目标激活工作流的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中相应地映射源架构中的这些命名空间和/或属性。 |
| 电子邮件 | 用户的电子邮件地址 | 请将纯文本电子邮件地址和SHA256散列电子邮件地址映射到此字段。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 如果您在上传到Adobe Experience Platform之前对客户电子邮件地址进行了哈希处理，请注意，必须使用SHA256对这些身份进行哈希处理，而不需使用Salt。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在使用Twitter自定义受众目标中使用的标识符导出受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Twitter Custom Audiences]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

在Twitter中定位现有的关注者和客户，并通过在Twitter中将Adobe Experience Platform中构建的受众激活为[!DNL List Custom Audiences]来创建相关的再营销活动。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

1. 在目标目录中找到[!DNL Twitter Custom Audiences]目标并选择&#x200B;**[!UICONTROL 设置]**。
2. 选择&#x200B;**[!UICONTROL 连接到目标]**。
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 输入您的Twitter凭据并选择&#x200B;**登录**。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帐户 ID"
>abstract="您的 Twitter 广告帐户 ID。可以在 Twitter 广告设置中找到它。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL Twitter Ads]帐户ID。 这可以在[!DNL Twitter Ads]设置中找到。

>[!IMPORTANT]
>
>请勿使用特殊字符(+ &amp; ， % ： ； @ / = ？ $ \n)（受众、描述和受众映射名称中）。 如果您的Experience Platform受众名称包含这些字符，请在将受众映射到Twitter目标之前删除它们。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射注意事项 {#mapping-considerations}

将受众映射到Twitter时，提供人类可读的受众映射名称。 我们建议您使用与Experience Platform区段相同的名称。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。

## 其他资源 {#additional-resources}

有关Twitter中[!DNL List Custom Audiences]的详细信息，可在[Twitter文档](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)中找到。
