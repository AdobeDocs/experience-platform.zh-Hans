---
title: Rokt
description: 了解如何将Adobe Experience Platform受众关联到Rokt，以通过更智能的定位、抑制和个性化来改进营销活动效果。
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# [!DNL Rokt]连接 {#rokt-destination}

## 概述 {#overview}

[[!DNL Rokt]](https://www.rokt.com)使用人工智能驱动的实时决策解锁电子商务中的值，以使每个事务时刻更™相关。 它提供个性化的体验，并将广告商与高意图客户联系起来。 将[!DNL Adobe Experience Platform]受众连接到[!DNL Rokt]以通过更智能的定位、抑制和个性化来改进营销活动效果。 在适当的时间联系适当的客户，同时减少浪费的支出。

>[!IMPORTANT]
>
>目标连接器和文档页面由[!DNL Rokt]团队创建和维护。 有关任何查询或更新请求，请与您的[!DNL Rokt]客户经理联系或联系`support@rokt.com`。

## 用例 {#use-cases}

以下用例显示了[!DNL Experience Platform]客户如何使用[!DNL Rokt]目标。

### 用例#1：重定位 {#use-case-1}

重新吸引访问您的网站或应用程序但未转化的高意图客户。 在[!DNL Experience Platform]中构建受众，包括浏览特定产品类别或放弃结账流的用户。 然后，将该受众推送到[!DNL Rokt]，以便在合作伙伴网站购买时提供个性化优惠。 [!DNL Rokt]在交易时间内运行，即客户在其他地方完成购买后立即运行。 当购买意向达到峰值时，会访问重定向的受众，与传统展示重定向相比，这种情况下会提高转化率。

### 用例#2：禁止列表 {#use-case-2}

通过抑制不应接收特定[!DNL Rokt]选件的受众，防止浪费的支出和不相关的体验。 常见的禁止使用案例包括排除最近的转化者、活跃促销中的忠诚会员或选择退出营销的用户。 例如，排除过去30天内购买的客户。 将这些禁止显示受众从[!DNL Experience Platform]实时同步到[!DNL Rokt]。 这使得营销活动始终专注于新用户或可重新参与的用户。 这提高了ROI并保护了客户体验。

## 先决条件 {#prerequisites}

在[!DNL Adobe Experience Platform]中设置[!DNL Rokt]目标之前，必须从&#x200B;**[!DNL Rokt]帐户管理员**&#x200B;获取以下凭据：

* **API密钥**：在[对目标连接](#authenticate)进行身份验证时，请将此密钥用作&#x200B;**[!UICONTROL Username]**。
* **API密钥**：在[对目标连接](#authenticate)进行身份验证时，请将此密钥用作&#x200B;**[!UICONTROL Password]**。

在安装之前，您的[!DNL Rokt]帐户管理员将在[!DNL Rokt]平台中配置这些凭据。 如果您尚未收到这些电子邮件，请联系您的客户经理。

## 支持的身份 {#supported-identities}

[!DNL Rokt]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 纯文本电子邮件地址 | 推荐。 用于[!DNL Rokt]中的配置文件匹配。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | 支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选择&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| 电话 | 纯文本电话号码 | 用于[!DNL Rokt]中的配置文件匹配。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | 支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选择&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| GAID | [!DNL Google] Advertising ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的[!DNL Apple] ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| aepProfileId | [!DNL Adobe Experience Platform]配置文件ID | 将配置文件ID (`xdm:_id`)映射为回退标识符。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过[!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入[!DNL Experience Platform]，](/help/segmentation/ui/audience-portal.md#import-audience)</li><li> 相似的受众， </li><li> 联合受众， </li><li> 在其他[!DNL Experience Platform]应用（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 基于客户配置文件。 使用这些功能定位营销活动的特定人员组。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在使用[!DNL Rokt]目标中使用的标识符（电子邮件、电话、移动广告ID或其他）导出受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在[!DNL Experience Platform]中更新了用户档案，连接器就会将更新发送到下游[!DNL Rokt]。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](/help/destinations/ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Username]**：您的API密钥，由[!DNL Rokt]帐户管理员提供。
* **[!UICONTROL Password]**：您的API密钥，由您的[!DNL Rokt]帐户管理员提供。

  ![[!DNL Experience Platform]中的[!DNL Rokt]目标配置屏幕，已填写帐户详细信息、身份验证字段和目标详细信息。](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称（例如，“[!DNL Rokt] — 重定位受众”）。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](/help/destinations/ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

[!DNL Rokt]目标支持从[!DNL Experience Platform]到[!DNL Rokt]标识字段的标识命名空间映射。 您必须至少映射一个标识才能成功激活受众。 下表显示了推荐的映射。

| 源字段 | 目标字段 | 注意事项 |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | 推荐 |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | 推荐 |
| `IdentityMap: Phone` | `Identity: phone` | 可选 |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | 可选 |
| `IdentityMap: GAID` | `Identity: gaid` | 可选 |
| `IdentityMap: IDFA` | `Identity: idfa` | 可选 |
| `xdm: _id` | `Identity: aepProfileId` | 可选 |

{style="table-layout:auto"}

以下是完整映射的示例：

![ [!DNL Experience Platform]中[!DNL Rokt]目标激活工作流的映射步骤，已配置源和目标标识字段。](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>强烈建议至少有一个基于电子邮件的标识映射（`email`或`emailSha256`），以在[!DNL Rokt]中最大限度地提高匹配率。

### 配置受众计划 {#audience-schedule}

完成映射步骤后，为每个选定的受众配置受众计划。 提供&#x200B;**[!UICONTROL Start date]**&#x200B;以及一个&#x200B;**[!UICONTROL Mapping ID]**（用于在[!DNL Rokt]中标识此受众的标签）。 您可以使用[!DNL Experience Platform]受众名称或有助于您和您的[!DNL Rokt]客户经理识别受众的任何描述性字符串。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Experience Platform]目标都符合数据使用策略。 有关[!DNL Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

* [[!DNL Rokt]开发人员文档](https://docs.rokt.com)
* [Adobe Experience Platform目标概述](/help/destinations/home.md)
