---
title: （测试版）Snap Inc连接
description: 了解如何连接到Snapchat Ads平台并从Experience Platform中导出受众区段。
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---


# （测试版）Snap Inc

## 概述 {#overview}

[Snapchat Ads](https://forbusiness.snapchat.com/) 不管规模大小或行业如何，每家企业都会生产。 通过全屏数字广告成为Snapchatters日常对话的一部分，这些广告能够激励那些对您的业务最为重要的人采取行动。

>[!IMPORTANT]
>
>此文档页面由 *Snap Inc* 团队。 此产品目前是测试版产品，功能可能会发生更改。 如有任何查询或更新请求，请直接联系 *dev-support@snap.com*

## 用例 {#use-cases}

此目标允许营销人员将Experience Platform中创建的用户区段导入Snapchat Ads，并使用这些区段定位其广告。

## 先决条件 {#prerequisites}

要使用此目的地，您必须拥有Snapchat Ads帐户。 有关如何创建文档的信息，请参阅此文档：

[Snapchat广告入门](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支持给定受众区段的多个标识。 激活区段时，请仅映射一个身份。
* Snap Inc不支持重命名区段。 要重命名区段，必须先将其停用、重命名，然后将其激活。
* 无法为受众区段的成员定义保留期。 所有成员都具有生命周期保留，并将一直保留在区段中，直到将其删除为止。

## 支持的身份 {#supported-identities}

的 *Snap Inc* 目标支持激活下表中描述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

发送到的所有标识符 *Snap Inc* 目标必须以SHA-256格式进行哈希处理。 要在将纯文本标识符发送到目标之前对其进行哈希处理，请检查 **[!UICONTROL 应用转换]** 选项。

>[!WARNING]
> 
> Snap Inc目标将不接受经过未哈希处理的标识符，并且发送它们可能会导致错误。


>[!IMPORTANT]
> 
> Snap Inc目标不支持多个标识。 请只选择一个身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| Email Address | SHA-256经过哈希处理的电子邮件地址 | 将电子邮件地址映射到目标身份字段 *emailAddress*. |
| 电话号码 | SHA-256哈希电话号码 | 将电子邮件地址映射到目标身份字段 *phoneNumber*. |
| GAID | SHA-256经过哈希处理的Google广告ID | 将Google广告ID映射到目标标识字段 *gaid*. |
| IDFA | SHA-256经过哈希处理的Apple广告ID | 将Apple广告ID映射到目标标识字段 *idfa*. |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 *您的目标* 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到Snap Inc {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请执行以下步骤：

1. 查找 *Snap Inc* 目标，并选择 **设置**.
2. 选择 **[!UICONTROL 连接到目标]**. 您将被重定向到以下屏幕：
   ![身份验证屏幕1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 输入您的Snapchat凭据并选择 **登录**.
4. 您将看到Adobe Experience Platform能够访问的Snapchat数据。 选择 **继续** 以继续连接过程。

![身份验证屏幕2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

选择继续后，等待您被重定向回Adobe Experience Platform。

### 填写目标详细信息 {#destination-details}

![目标详细信息](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**.

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:与您要将区段导入的广告帐户关联的广告帐户ID。 有关如何查找此内容的更多信息，请参阅 [有关Snapchat业务帮助中心的文档](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>输入不正确或无效的Snapchat广告帐户ID将导致区段激活失败。 请仔细检查您是否输入了正确的广告帐户ID。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 验证数据导出 {#exported-data}

在将区段激活到 *Snap Inc* 目标，您将能够在快照广告管理器的 [**受众** 部分](https://businesshelp.snapchat.com/s/article/audience-sharing). 要导航到此部分，请执行以下步骤：

1. 登录 [快照广告管理器](https://ads.snapchat.com/)
2. 选择 **受众** 菜单。 您将在受众库中看到在Adobe Experience Platform中激活的区段：

![受众](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

请注意，首次将Adobe区段激活到Snap Inc时，您最初会将其视为空受众。 这是因为Adobe Experience Platform在评估区段之前不会将成员数据导出到Snap Inc。 有关如何在Experience Platform中评估区段的更多信息，请参阅 [Segmentation Service概述](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).