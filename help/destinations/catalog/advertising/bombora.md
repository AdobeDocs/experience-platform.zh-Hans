---
title: 庞博拉连接
description: 根据客户受众，激活Bombora营销活动的用户档案，以实现受众定位、个性化和抑制。
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: 026d8e4c2bcea407d2a750e66b11766b1114b758
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 3%

---


# 庞博拉连接 {#bombora}

>[!AVAILABILITY]
>
>将Account Audiences激活到Bombra目标的功能适用于购买[Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)和[Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)版本的Real-Time Customer Data Platform的公司。

根据[帐户受众](/help/segmentation/types/account-audiences.md)，为您的Bombora营销活动激活用户档案，以实现受众定位、个性化和抑制。

## 用例 {#use-case}

为了帮助您更好地了解应该如何以及何时使用庞博拉目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### DSP集成 {#dsp-integration}

作为B2B营销人员，您可以在Real-time CDP中创建帐户列表，识别对您的产品表现出高意图的公司，然后使用此目标在Bombora中激活此列表。

通过与DSP集成，您可以使用Bombora数据开展有针对性的广告营销活动。 这可确保您的广告支出专注于最有可能转化的公司。

### Account-Based Marketing {#abm}

作为B2B营销人员，您可以根据CRM和营销信号构建帐户列表。 然后，您可以使用此目标在Bombora中激活此列表，其中ABM感知控件可帮助您定位这些公司的决策者。

### 基于帐户的多渠道营销激活 {#multi-channel-abm}

作为B2B营销人员，您可以在Real-time CDP中创建帐户列表，以识别意向强烈的公司。 然后，您可以使用此目标在Bombora中激活列表，以跨多个渠道运行目标营销活动。

在付费社交媒体上，您可以在目标帐户（如[!DNL LinkedIn]和[!DNL Facebook]）上向专业人员提供个性化广告。 使用原生广告平台，您可以确保内容可到达相关决策者。

您还可以将营销活动扩展到高级电视，向关键帐户投放广告。

这种多渠道方法可确保跨平台发送一致的消息，从而最大限度地提高参与度和转化率。

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | X | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 支持的身份 {#supported-identities}

Bombora需要下表描述的目标标识映射。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 |
|---|---|
| `primaryId` | Bombora需要此目标标识的映射，以便集成正常工作。 您可以将任何源字段映射到此标识。 此映射是强制性的，但不会将数据导出到Bombora。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-and-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有[!DNL Bombora]目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要将客户受众导出到Bombora，您需要以下信息。

1. 一个庞博拉的账户。
2. Bombora **[!UICONTROL 客户端ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密钥]**。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

![添加持有者令牌](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL 客户端ID]**：输入您的[!DNL Bombora]客户端ID。
* **[!UICONTROL 客户端密钥]**：输入您的[!DNL Bombora]客户端密钥。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![添加有关目标连接的信息](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

现在，您已准备好在庞博拉中激活受众。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将帐户受众激活到此目标的说明，请阅读[激活帐户受众](/help/destinations/ui/activate-account-audiences.md)。

### 强制映射 {#mapping}

Bombora目标要求您配置以下映射以便成功激活数据。



| 源字段 | 目标字段 | 描述 |
|---------|----------|---------|
| 任何值 | `Identity: primaryId` | 此映射对于Experience Platform建立与Bombora的连接是必需的。 此值不会导出到Bombora，但目标配置需要此值。 您可以为源字段选择任何属性。 |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora使用网站或域地址创建帐户列表。 |

![添加必需的映射](../..//assets/catalog/advertising/bombora/mappings.png)


## 其他注释和重要标注 {#additional-notes}

如果之前已将具有相同名称的帐户受众激活到Bombora，则当您尝试通过指向Bombora目标的不同数据流再次激活该受众时，将会收到错误。

