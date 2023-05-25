---
title: Snap Inc连接
description: 了解如何连接到Snapchat Ads平台并从Experience Platform导出受众区段。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 988ecbed3084ef162453c9f1124998c6e9ae2e45
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Snap Inc连接

## 概述 {#overview}

[Snapchat广告](https://forbusiness.snapchat.com/) 无论规模或行业如何，都可为所有企业量身打造。 Snapchatters每天都在与全屏数字广告对话，这些广告激发对您的业务最重要的人采取行动。

>[!IMPORTANT]
>
>此文档页面由创建 *Snap Inc* 团队。 如有任何查询或更新请求，请直接通过 *dev-support@snap.com*

## 用例 {#use-cases}

此目标允许营销人员将Experience Platform中创建的用户区段导入Snapchat广告，并使用它们定位其广告。

## 先决条件 {#prerequisites}

要使用此目标，您必须具有Snapchat Ads帐户。 有关如何创建模板的信息，请参阅此文档：

[Snapchat广告快速入门](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支持给定受众区段的多个身份。 激活区段时，请仅映射一个身份。
* Snap Inc不支持重命名区段。 要重命名区段，必须停用、重命名该区段，然后激活它。
* 无法为受众区段的成员定义保留期。 所有成员都具有生命周期保留期，它们将被保留在区段中，直到被删除。

## 支持的身份 {#supported-identities}

此 *Snap Inc* 目标支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

所有发送到以下对象的标识符： *Snap Inc* 目标必须采用SHA-256格式进行哈希处理。 要在将纯文本标识符发送到目标之前对其进行哈希处理，请检查 **[!UICONTROL 应用转换]** 选项。

>[!WARNING]
> 
> Snap Inc目标不会接受未经过哈希处理的标识符，发送这些标识符可能会导致错误。


>[!IMPORTANT]
> 
> Snap Inc目标不支持多个身份。 请仅选择一个身份。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| Email Address | SHA-256哈希电子邮件地址 | 将电子邮件地址映射到目标身份字段 *电子邮件地址*. |
| 电话号码 | SHA-256哈希电话号码 | 将电子邮件地址映射到目标身份字段 *phonenumber*. |
| GAID | SHA-256哈希后的Google广告ID | 将Google Advertising ID映射到目标标识字段 *gaid*. |
| IDFA | SHA-256哈希后的Apple广告ID | 将Apple Advertising ID映射到目标标识字段 *idfa*. |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员以及中使用的标识符（姓名、电话号码或其他）。 *您的目标* 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到Snap Inc {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请执行以下步骤：

1. 查找 *Snap Inc* 从Adobe Experience Platform目标目录中选择目标，然后选择 **设置**.
2. 选择 **[!UICONTROL 连接到目标]**. 您将被重定向到以下屏幕：
   ![身份验证屏幕1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 输入您的Snapchat凭据并选择 **登录**.
4. 您将看到Adobe Experience Platform能够访问的Snapchat数据。 选择 **继续** 以继续连接过程。

![身份验证屏幕2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

选择“继续”后，请等待，直到您被重定向回Adobe Experience Platform。

### 填写目标详细信息 {#destination-details}

![目标详细信息](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**.

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：与要将区段导入到的广告帐户关联的广告帐户ID。 有关如何查找此内容的更多信息，请参阅 [此文档位于Snapchat商务帮助中心](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>输入不正确或无效的Snapchat广告帐户ID将导致区段激活失败。 请仔细检查您输入的广告帐户ID是否正确。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 验证数据导出 {#exported-data}

将区段激活到 *Snap Inc* 目标，您将能够在快照广告管理器的 [**受众** 部分](https://businesshelp.snapchat.com/s/article/audience-sharing). 要导航到此部分，请执行以下步骤：

1. 登录 [Snap Ads管理器](https://ads.snapchat.com/)
2. 选择 **受众** 从屏幕左上角的下拉菜单中。 您将在受众库中看到在Adobe Experience Platform中激活的区段：

![受众](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

请注意，当Adobe区段首次激活到Snap Inc时，您最初会将其视为空受众。 这是因为Adobe Experience Platform在评估区段之前不会将成员数据导出到Snap Inc。 有关如何在Experience Platform中评估区段的更多信息，请参阅 [分段服务概述](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).
