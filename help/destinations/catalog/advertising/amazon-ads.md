---
title: Amazon Ads
description: Amazon Ads提供一系列选项，帮助您向注册销售商、供应商、图书供应商、Kindle Direct Publishing (KDP)作者、应用程序开发人员和/或代理商实现广告目标。 Amazon Ads与Adobe Experience Platform的集成提供了与Amazon Ads产品(包括Amazon DSP (ADSP))的统包集成。 通过使用Adobe Experience Platform中的Amazon广告目标，用户能够定义广告商受众，以便在Amazon DSP中进行定位和激活。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: ba768b3148d57e9df12a34f0324c086a17a6d45a
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# (Beta) Amazon Ads连接 {#amazon-ads}

## 概述 {#overview}

[!DNL Amazon Ads] 提供一系列选项，帮助您向注册销售商、供应商、图书供应商、Kindle Direct Publishing (KDP)作者、应用程序开发人员和/或代理商实现广告目标。

此 [!DNL Amazon Ads] 与Adobe Experience Platform的集成提供了到 [!DNL Amazon Ads] 产品，包括Amazon DSP (ADSP)和AmazonMarketing Cloud(AMC)。

使用 [!DNL Amazon Ads] 目标：在Adobe Experience Platform中，用户能够定义广告商受众，以便在Amazon DSP中进行定位和激活。  此外，用户还可以将其数据上传到 [!DNL Amazon Marketing Cloud] 要按受众了解广告商提供的维度、Amazon区段中的会员资格或AMC中可用的其他信号等效果。 将广告商受众上传到AMC后，用户可以使用 [!DNL Amazon Marketing Cloud] 要使用中的Amazon信号修改、增强或附加到受众成员，请执行以下操作 [!DNL Amazon Marketing Cloud].

AMC将来自Amazon自有资产和运营资产的独特信号整合在一起，横跨各种媒体，包括显示器、视频、流电视、音频和赞助广告。 用户可轻松地将精选区段从Adobe Experience Platform发送到AMC，以增强学习，例如受众的市场内群组、生活方式同类群组以及品牌参与模式。 然后，可以使用增强的区段来优化Amazon DSP中的媒体激活。

>[!IMPORTANT]
>
>此目标连接器和文档页面由 *[!DNL Amazon Ads]* 团队。 此产品目前为测试版，其功能可能会有变动。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： *`amc-support@amazon.com`.*

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 *[!DNL Amazon Ads]* 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 激活和定位 {#activation-and-targeting}

与Amazon DSP的这种集成允许 [!DNL Amazon Ads] 广告商可将广告商CDP受众从Adobe Experience Platform传递到Amazon的DSP，以创建用于广告定位的广告商受众。 可以在Amazon DSP中选择正确定位以及负确定位（抑制）的受众。

### Analytics and Measurement {#analytics-and-measurement}

此集成与 [!DNL Amazon Marketing Cloud] (AMC)允许 [!DNL Amazon Ads] 广告商将CDP区段从Adobe Experience Platform表单传递到AMC。 然后，广告商可以通过以下方式加入CDP输入 [!DNL Amazon Ads] 以符合隐私要求的格式发送信号，并对媒体影响、受众区段和客户历程等主题进行自定义分析。 例如，广告商可以上传其现有客户的列表来了解汇总的广告促销活动效果，或汇总Amazon上转化事件的统计信息，例如查看产品详细信息页面、将产品添加到购物车或购买产品。

### 广告优化：

此集成与 [!DNL Amazon Marketing Cloud] (AMC)允许广告商上传自己的客户列表，并使用 [!DNL Amazon Marketing Cloud] 在Amazon DSP中创建激活就绪受众以进行定位之前，SQL会定期对受众执行重叠分析、抑制、添加或优化。

## 先决条件 {#prerequisites}

要使用 [!DNL Amazon Ads] 与Adobe Experience Platform建立连接，用户必须首先有权访问Amazon DSP广告商帐户或 [!DNL Amazon Marketing Cloud] 实例。 要配置这些实例，请访问 [!DNL Amazon Ads] 网站：

* [Amazon DSP入门](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [AmazonMarketing Cloud入门](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## 支持的身份 {#supported-identities}

此 *[!DNL Amazon Ads]* connection支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service//features/namespaces.md). 有关支持的标识的更多详细信息 [!DNL Amazon Ads]，请访问 [Amazon DSP支持中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正使用 *[!DNL Amazon Ads]* 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

您被带到 [!DNL Amazon Ads] 连接界面，您可以在其中首次选择要连接的广告商帐户。 建立连接后，系统会通过新连接将您重定向回Adobe Experience Platform，同时还会提供您选择的广告商帐户ID。 请在目标配置屏幕上选择相应的广告商帐户以继续。

* **[!UICONTROL 持有者令牌]**：填写持有者令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Amazon Ads连接]**：选择目标的ID [!DNL Amazon Ads] 用于目标的帐户。

>[!NOTE]
>
>保存目标配置后，您将无法更改 [!DNL Amazon Ads] 广告商ID，即使您通过Amazon帐户重新进行身份验证也是如此。 使用不同的 [!DNL Amazon Ads] 广告商ID，您必须创建新的目标连接。

* **[!UICONTROL 广告商地区]**：选择托管您的广告商的适当区域。 有关每个区域支持的市场的更多信息，请访问 [Amazon Ads文档](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![配置新目标](../../assets/catalog/advertising/amazon_ads_image_4.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射属性和身份 {#map}

此 [!DNL Amazon Ads] connection支持经过哈希处理的电子邮件地址和电话号码，以便进行身份匹配。 下面的屏幕截图提供了与兼容的匹配示例 [!DNL Amazon Ads] 连接：

![Adobe到Amazon广告的映射](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 要映射经过哈希处理的电子邮件地址，请选择 `Email_LC_SHA256` 将命名空间标识为源字段。
* 要映射经过哈希处理的电话号码，请选择 `Phone_SHA256` 将命名空间标识为源字段。
* 要映射未经过哈希处理的电子邮件地址或电话号码，请选择相应的身份命名空间作为源字段，然后选中 `Apply Transformation` 用于使Platform在激活时散列身份的选项。

在的目标配置中，您只选择一次给定目标字段 [!DNL Amazon Ads] 连接器。  例如，如果提交企业电子邮件，则无法在同一目标配置中映射个人电子邮件。

强烈建议您映射尽可能多的可用字段。 如果只有一个源属性可用，则可以映射单个字段。 此 [!DNL Amazon Ads] 目标利用所有映射的字段进行映射，如果提供了更多字段，则可获得更高的匹配率。 有关接受的标识符的更多信息，请访问 [Amazon Ads哈希受众帮助页面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 导出的数据/验证数据导出 {#exported-data}

上传受众后，您可以使用以下步骤验证受众是否已正确创建和上传：

**适用于Amazon DSP**

导航到 **[!UICONTROL 广告商ID]** > **[!UICONTROL 受众]** > **[!UICONTROL 广告商受众]**. 如果受众已成功创建并且满足受众成员的最低数量，您将看到状态 `Active`. 有关受众规模和范围的其他详细信息，请参阅Amazon DSP用户界面右侧的预测范围面板。

![Amazon DSP受众创建验证](../../assets/catalog/advertising/amazon_ads_image_3.png)

**对象[!DNL Amazon Marketing Cloud]**

在左侧架构浏览器中，找到位于下的受众 **[!UICONTROL 广告商已上传]** > **[!UICONTROL aep_audiences]**. 然后，您可以在AMC SQL编辑器中使用以下子句查询受众：

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![AmazonMarketing Cloud受众创建验证](../../assets/catalog/advertising/amazon_ads_image_5.png)


## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关其他帮助文档，请访问以下页面 [!DNL Amazon Ads] 帮助资源：

* [Amazon DSP帮助中心](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 3 月 | 功能和文档更新 | 添加了用于导出受众的选项，以便 [!DNL Amazon Marketing Cloud] (AMC)。 |
| 2023 年 5 月 | 功能和文档更新 | <ul><li>在中增加了对广告商区域选择的支持 [目标连接工作流](#destination-details).</li><li>更新了文档以反映添加了“广告商区域”选择。 有关选择正确的广告商区域的详细信息，请参阅 [Amazon文档](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| 2023 年 3 月 | 初始版本 | 发布了初始目标版本和文档。 |

{style="table-layout:auto"}

+++
