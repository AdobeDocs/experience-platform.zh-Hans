---
title: Amazon Ads
description: Amazon Ads提供一系列选项，帮助您向注册销售商、供应商、图书供应商、Kindle Direct Publishing (KDP)作者、应用程序开发人员和/或代理商实现广告目标。 Amazon Ads与Adobe Experience Platform的集成提供了与Amazon Ads产品(包括Amazon DSP (ADSP))的统包集成。 通过使用Adobe Experience Platform中的Amazon Ads目标，用户能够定义广告商受众，以便在Amazon DSP中进行定位和激活。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 9c1f3d5d5fc14941cb40adf02fd3d9acce5cf648
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 1%

---

# (Beta) Amazon Ads连接 {#amazon-ads}

## 概述 {#overview}

Amazon Ads提供一系列选项，帮助您向注册销售商、供应商、图书供应商、Kindle Direct Publishing (KDP)作者、应用程序开发人员和/或代理商实现广告目标。

Amazon Ads与Adobe Experience Platform的集成提供了与Amazon Ads产品(包括Amazon DSP (ADSP))的统包集成。 通过使用Adobe Experience Platform中的Amazon Ads目标，用户能够定义广告商受众，以便在Amazon DSP中进行定位和激活。

>[!IMPORTANT]
>
>此文档页面由创建 *Amazon Ads* 团队。 此产品目前为测试版，其功能可能会有变动。 如有任何查询或更新请求，请直接通过 *`amc-support@amazon.com`.*

## 用例 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 *Amazon Ads* 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 激活和定位 {#activation-and-targeting}

与Amazon DSP的这种集成允许Amazon Ads广告商将广告商CDP区段从Adobe Experience Platform传递到Amazon的DSP，以创建广告商受众进行广告定位。 可以在Amazon DSP中选择正面定位和负面定位（抑制）的受众。

## 先决条件 {#prerequisites}

要将Amazon Ads连接与Adobe Experience Platform结合使用，用户必须首先有权访问Amazon DSP广告商帐户。 要配置这些实例，请访问Amazon Ads网站上的以下页面：

* [Amazon DSP入门](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 支持的身份 {#supported-identities}

此 *Amazon Ads* 连接支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md). 有关Amazon Ads支持的标识的更多详细信息，请访问 [Amazon DSP支持中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法对电子邮件地址进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员以及中使用的标识符（姓名、电话号码或其他）。 *Amazon Ads* 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

您将转到Amazon Ads连接界面，在该界面中，您可以首先选择要连接的广告商帐户。 建立连接后，系统会通过新连接将您重定向回Adobe Experience Platform，同时提供您选择的广告商帐户ID。 在目标配置屏幕上选择适当的广告商帐户以继续。

* **[!UICONTROL 持有者令牌]**：填写持有者令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Amazon广告商ID]**：选择用于目标的目标Amazon Ads帐户的ID。
>[!NOTE]
>
>保存目标配置后，您将无法更改Amazon Ads广告商ID，即使您通过Amazon帐户重新进行身份验证也是如此。 要使用其他Amazon广告商ID，您必须创建新的目标连接。
* **[!UICONTROL 广告商地区]**：选择托管您的广告商的适当区域。 有关每个地区支持的市场的更多信息，请访问 [Amazon Ads文档](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![配置新目标](../../assets/catalog/advertising/amazon_ads_image_4.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

Amazon Ads连接支持经过哈希处理的电子邮件地址和经过哈希处理的电话号码，以便进行身份匹配。 下面的屏幕截图提供了与Amazon Ads连接兼容的匹配示例：

![Adobe到Amazon Ads的映射](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 要映射经过哈希处理的电子邮件地址，请选择 `Email_LC_SHA256` 标识命名空间作为源字段。
* 要映射经过哈希处理的电话号码，请选择 `Phone_SHA256` 标识命名空间作为源字段。
* 要映射未经过哈希处理的电子邮件地址或电话号码，请选择相应的身份命名空间作为源字段，然后检查 `Apply Transformation` 用于使Platform在激活时哈希标识的选项。

强烈建议您映射尽可能多的可用字段。 如果只有一个源属性可用，则可以映射单个字段。 Amazon Ads目标利用所有映射的字段进行映射，如果提供了更多字段，则可获得更高的匹配率。 有关接受的标识符的更多信息，请访问 [Amazon Ads哈希受众帮助页面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 导出的数据/验证数据导出 {#exported-data}

上传受众后，您可以使用以下步骤验证受众是否已正确创建和上传：

**对于Amazon DSP**

导航到您的广告商ID → Audiences → Advertiser Audiences。 如果受众创建成功且满足受众成员的最低数量，您将看到状态 `Active`. 有关受众规模和范围的其他详细信息，请参阅Amazon DSP用户界面右侧的预测范围面板。

![Amazon DSP受众创建验证](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据治理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关其他帮助文档，请访问以下Amazon广告帮助资源：

* [Amazon DSP帮助中心](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

### Changelog {#changelog}

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 5 月 | 功能和文档更新 | <ul><li>在目标连接工作流中添加了对广告商区域选择的支持。</li><li>更新了文档，以反映添加了“广告商区域”选择。 有关选择正确的广告商地区的详细信息，请参阅 [Amazon文档](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| 2023 年 3 月 | 初始版本 | 发布了初始目标版本和文档。 |

{style="table-layout:auto"}

+++
