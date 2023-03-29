---
title: Amazon Ads
description: Amazon Ads提供一系列选项，帮助您向已注册的销售商、供应商、图书供应商、Kindle Direct Publishing(KDP)作者、应用程序开发商和/或代理机构实现广告目标。 与Adobe Experience Platform的Amazon Ads集成提供了与Amazon Ads产品(包括Amazon DSP(ADSP))的转钥匙集成。 使用Adobe Experience Platform中的Amazon Ads目标，用户能够定义广告商受众，以便在Amazon DSP上进行定位和激活。
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (Beta)Amazon Ads连接 {#amazon-ads}

## 概述 {#overview}

Amazon Ads提供一系列选项，帮助您向已注册的销售商、供应商、图书供应商、Kindle Direct Publishing(KDP)作者、应用程序开发商和/或代理机构实现广告目标。

与Adobe Experience Platform的Amazon Ads集成提供了与Amazon Ads产品(包括Amazon DSP(ADSP))的转钥匙集成。 使用Adobe Experience Platform中的Amazon Ads目标，用户能够定义广告商受众，以便在Amazon DSP上进行定位和激活。

此连接支持在以下Amazon市场中创建受众： `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>此文档页面由 *Amazon Ads* 团队。 此产品目前是测试版产品，功能可能会发生更改。 如有任何查询或更新请求，请直接联系 *`amc-support@amazon.com`.*

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 *Amazon Ads* 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 激活和定位 {#activation-and-targeting}

与Amazon DSP的这一集成允许Amazon Ads广告商将广告商CDP区段从Adobe Experience Platform传递到Amazon DSP，以创建广告商受众以进行广告定位。 可以在Amazon DSP中选择受众以进行正面定位，以及负面定位（抑制）。 此外，使用通过AmazonMarketing Cloud生成的信号，广告商可以优化其广告商受众，从而将受众更改与Amazon DSP同步。

## 先决条件 {#prerequisites}

要与Adobe Experience Platform使用Amazon Ads连接，用户必须首先拥有Amazon DSP广告商帐户的访问权限。  要配置这些实例，请访问Amazon Ads网站上的以下页面：

* [开始使用Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 支持的身份 {#supported-identities}

的 *Amazon Ads* connection支持激活下表中描述的身份。 详细了解 [标识](/help/identity-service/namespaces.md). 有关Amazon Ads支持的身份的更多详细信息，请访问 [Amazon DSP支持中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 *Amazon Ads* 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

您将转到Amazon Ads连接界面，您将首先在该界面中选择要连接的广告商帐户。  连接后，您将被重定向回具有新连接的Adobe Experience Platform，该连接提供了您选择的广告商帐户ID。 在目标配置屏幕上选择相应的广告商帐户以继续操作。

* **[!UICONTROL 载体令牌]**:填写承载令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL Amazon广告商ID]**:选择用于目标的目标Amazon广告帐户的ID。

注意：选择此Amazon广告商ID后，您需要创建一个新目标来更改此ID。 如果您重新验证OAuth凭据并选择新的广告商ID，则您所做的更改将不适用。

![配置新目标](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和标识 {#map}

Amazon Ads连接支持用于身份匹配目的的经过哈希处理的电子邮件地址和经过哈希处理的电话号码。  以下屏幕截图提供了一个与Amazon Ads连接兼容的匹配示例：

![Adobe到Amazon广告的映射](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 要映射经过哈希处理的电子邮件地址，请选择 `Email_LC_SHA256` 作为源字段的身份命名空间。
* 要映射经过哈希处理的电话号码，请选择 `Phone_SHA256` 作为源字段的身份命名空间。
* 要映射未经过哈希处理的电子邮件地址或电话号码，请选择相应的身份命名空间作为源字段，然后检查 `Apply Transformation` 选项，以在激活时对Platform身份进行哈希处理。

强烈建议您映射尽可能多的可用字段。 如果只有一个源属性可用，则可以映射单个字段。  Amazon Ads目标会将所有映射的字段用于映射目的，如果提供了更多字段，则会生成更高的匹配率。 有关已接受标识符的更多信息，请访问 [Amazon Ads经过哈希处理的受众帮助页面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 导出的数据/验证数据导出 {#exported-data}

上传受众后，您可以使用以下步骤验证是否已创建并正确上传受众：

**对于Amazon DSP**

导航到您的广告商ID →受众→广告商受众。 如果您的受众已成功创建，并且符合受众成员的最少数量，您将看到状态为 `Active`.  有关受众大小和范围的其他详细信息，请参阅Amazon DSP用户界面右侧的“预测范围”面板。

![Amazon DSP受众创建验证](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关其他帮助文档，请访问以下Amazon Ads帮助资源：

* [Amazon DSP帮助中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
