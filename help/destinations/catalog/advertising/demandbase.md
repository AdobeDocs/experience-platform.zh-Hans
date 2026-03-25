---
title: Demandbase连接
description: 使用此目标来激活 Account-Based Marketing (ABM) 用例的帐户受众。通过 DemandBase 的 B2B Demand Side Platform（DSP）向目标帐户中的相关用户画像和角色投放广告。目标帐户还可以通过 Demandbase 第三方数据进行丰富，以用于营销和销售中的其他下游用例。
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 15%

---


# Demandbase连接 {#demandbase}

>[!AVAILABILITY]
>
>向Demandbase目标激活帐户受众的功能适用于购买[的](/help/rtcdp/overview.md#rtcdp-b2b)企业对企业[和](/help/rtcdp/overview.md#rtcdp-b2p)企业对个人[!DNL Real-Time Customer Data Platform]版本的公司。

根据[帐户受众](/help/segmentation/types/account-audiences.md) ，激活Demandbase营销活动的配置文件以进行受众定位、个性化和抑制。

## 用例 {#use-case}

使用此目标来激活 Account-Based Marketing (ABM) 用例的帐户受众。通过 DemandBase 的 B2B Demand Side Platform（DSP）向目标帐户中的相关用户画像和角色投放广告。目标帐户还可以通过 Demandbase 第三方数据进行丰富，以用于营销和销售中的其他下游用例。

例如，利用Demandbase的广告技术DSP来定位关键客户中的特定角色或角色，以创造funnel顶级商机，或创建并扩大购买群体。 使用Demandbase目标来探索其他用例，以有效定位您的帐户。

利用此集成，您还可以使用实时帐户信息查找来优化参与，从而个性化网站体验。

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}

按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 是 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-and-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|--------------|-----------|---------------------------|
| 导出类型 | 受众导出 | 将使用关键标识符（如姓名、电话号码等）导出所有受众成员。 |
| 频率 | 流传输 | 基于“始终运行”API的连接。 配置文件更改后，更新会立即发送到下游。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要将帐户受众导出到Demandbase，您需要满足以下条件：

1. Demandbase帐户。
2. Demandbase API令牌。 您可以在Demandbase中使用用户生成API令牌。 要生成令牌，请在登录到Demandbase帐户后导航到[我的个人资料> API令牌](https://web.demandbase.com/o/ad/at)。

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

![添加持有者令牌](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer token]**：填写持有者令牌以对目标进行身份验证。 有关如何获取令牌的信息，请查看[先决条件](#prerequisites)。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![添加有关目标连接的信息](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Entity type]**：选择&#x200B;**[!UICONTROL Account]**&#x200B;作为实体类型。

现在，您已准备好在Demandbase中激活受众。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将帐户受众激活到此目标的说明，请阅读[激活帐户受众](/help/destinations/ui/activate-account-audiences.md)。

### 强制映射 {#mandatory-mappings}

将受众激活到[!DNL Demandbase]目标时，您必须在映射步骤中配置以下必填字段映射：

| 源字段 | 目标字段 | 描述 |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | 帐户的名称 |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | 帐户组织的电子邮件域 |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | 帐户的主要标识符 |

![Demandbase映射](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

目标需要这些映射才能正常运行，并且必须先配置这些映射，然后才能继续激活工作流。

## 其他注释和重要标注 {#additional-notes}

* **受众命名**：如果之前已将具有相同名称的帐户受众激活到Demandbase，则无法通过其他数据流将其再次激活到Demandbase目标。
* **Demandbase API护栏**：如果您已将受众导出到Demandbase，并且在Experience Platform中成功导出，但并非所有数据都到达Demandbase，则您可能会在Demandbase端遇到API限制。 请联系他们以获取说明。
* **列表删除**：帐户列表是唯一的，因此不能使用名称重新创建新列表。 当您从列表中删除帐户时，这些帐户将不再可用，但不会删除。
* **激活时间**：在Demandbase中加载的数据需要过夜处理。
