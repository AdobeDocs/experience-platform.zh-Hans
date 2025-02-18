---
title: Snap Inc连接
description: 了解如何连接到Snapchat广告平台并从Experience Platform导出受众。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 9a80a9b49b1983e8e488d11b114c02130b045686
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 2%

---

# Snap Inc连接

## 概述 {#overview}

[Snapchat广告](https://forbusiness.snapchat.com/)是为每个企业制作的，无论其规模或行业如何。 Snapchatters每天都在与全屏数字广告对话，这些广告激发对您的业务最重要的人员采取行动。

>[!IMPORTANT]
>
>此目标连接器和文档页面由&#x200B;*快照公司*&#x200B;团队创建和维护。 如有任何查询或更新请求，请直接通过&#x200B;*dev-support@snap.com*&#x200B;联系他们

## 用例 {#use-cases}

此目标允许营销人员将在Experience Platform中创建的用户受众导入到Snapchat广告中，并使用这些受众定位其广告。

## 先决条件 {#prerequisites}

要使用此目标，您必须具有Snapchat广告帐户。 有关如何创建规则库的信息，请参阅此文档：

[开始使用Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支持给定受众区段的多个身份。 激活区段时，请仅映射一个身份。
* Snap Inc不支持重命名区段。 要重命名区段，您必须先取消激活、重命名该区段，然后再激活它。
* 无法为受众区段的成员定义保留期。 所有成员都具有生命周期保留期，在被移除之前，它们都将位于受众中。

## 支持的身份 {#supported-identities}

*Snap Inc*&#x200B;目标支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

发送到&#x200B;*Snap Inc*&#x200B;目标的所有标识符必须以SHA-256格式进行哈希处理。 要在将纯文本标识符发送到目标之前对其进行哈希处理，请在映射目标标识符到目标时选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项。

>[!WARNING]
> 
> Snap Inc目标不会接受未经过哈希处理的标识符，发送这些标识符可能会导致错误。


>[!IMPORTANT]
> 
> Snap Inc目标不支持多个身份。 请仅选择一个身份。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件地址 | SHA-256哈希电子邮件地址 | 将电子邮件地址映射到目标标识字段&#x200B;*emailAddress*。 |
| 电话号码 | SHA-256散列电话号码 | 将电子邮件地址映射到目标标识字段&#x200B;*phoneNumber*。 |
| GAID | SHA-256哈希后的Google Advertising ID | 将Google Advertising ID映射到目标标识字段&#x200B;*gaid*。 |
| IDFA | SHA-256哈希后的Apple Advertising ID | 将Apple Advertising ID映射到目标标识字段&#x200B;*idfa*。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |
| [!DNL Federated Audience Composition] | ✓ | 通过[联合受众构成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences)导入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Snap Inc目标中所用标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 正在连接到Snap Inc {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

### 验证目标 {#authenticate}

要向目标进行身份验证，请执行以下步骤：

1. 从Adobe Experience Platform的目标目录找到&#x200B;*快照公司*&#x200B;目标，然后选择&#x200B;**设置**。
2. 选择&#x200B;**[!UICONTROL 连接到目标]**。 您将被重定向到以下屏幕：
   ![身份验证屏幕1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 输入您的Snapchat凭据并选择&#x200B;**登录**。
4. 您将看到Adobe Experience Platform能够访问的Snapchat数据。 选择&#x200B;**继续**&#x200B;以继续连接过程。

![身份验证屏幕2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

选择“继续”后，请等待，直到您被重定向回Adobe Experience Platform。

### 填写目标详细信息 {#destination-details}

![目标详细信息](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

要配置目标的详细信息，请填写必填字段并选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：与要将受众导入到的广告帐户关联的广告帐户ID。 有关如何查找的详细信息，请参阅Snapchat业务帮助中心](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US)上的[此文档。

>[!IMPORTANT]
> 
>输入不正确或无效的Snapchat广告帐户ID将导致受众激活失败。 请仔细检查您输入的广告帐户ID是否正确。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

## 验证数据导出 {#exported-data}

将受众激活到&#x200B;*Snap Inc*&#x200B;目标后，您将能够在Snap Ads管理器的&#x200B;[**受众**&#x200B;部分](https://businesshelp.snapchat.com/s/article/audience-sharing)中查看受众。 要导航到此部分，请执行以下步骤：

1. 登录[快照广告管理器](https://ads.snapchat.com/)
2. 从屏幕左上角的下拉菜单中选择&#x200B;**受众**。 您将在受众库中看到在Adobe Experience Platform中激活的受众：

![受众](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

请注意，首次将Adobe受众激活到Snap Inc时，您最初会将其视为空受众。 这是因为Adobe Experience Platform在评估受众之前，不会将成员数据导出到Snap Inc。 有关如何在Experience Platform中评估受众的更多信息，请参阅[分段服务概述](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
