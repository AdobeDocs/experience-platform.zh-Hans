---
title: Medallia连接
description: 激活目标Medallia调查和反馈收集的用户档案，以更好地了解客户的需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 3%

---

# Medallia连接

## 概述 {#overview}

激活目标Medallia调查和反馈收集的用户档案，以更好地了解客户的需求和期望。

>[!IMPORTANT]
>
>此目标连接器和文档页面由Medallia团队创建和维护。 如有任何查询或更新请求，请直接通过adobe-integrations@medallia.com联系他们。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时应使用Medallia目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

B2B品牌希望评估和简化其入职计划。 他们希望向刚刚完成入门培训流程的客户实时发送个性化调查。

### 用例#2 {#use-case-2}

retailer希望更好地了解客户对订单履行情况的偏好。 他们希望向过去一个月内在线和店内购买过产品的客户发送一份简短的1个问题短信调查。

## 先决条件 {#prerequisites}

建立Medallia连接需要以下信息：

* **OAuth令牌端点URL**
* **客户端ID**
* **客户端密码**
* **API网关URL**
* **导入API名称**

请与您的Medallia交付团队合作以获取这些详细信息。

## 支持的身份 {#supported-identities}

Medallia支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址 | 当您要发送电子邮件邀请调查时，请选择电子邮件目标身份。 当一个用户档案与多个电子邮件地址关联时，Medallia将仅触发对第一封电子邮件的邀请。 |
| 电话 | 以E.164格式散列的电话号码 | 当您要发送基于短信的调查时，请选择电话目标身份。 电话号码必须是E.164格式，其中包括加号(+)、国际国家/地区呼叫代码、本地区号和电话号码。 例如：(+)（国家代码）（区号）（电话号码）。 当配置文件与多个电话号码关联时，Medallia将仅触发第一个电话号码的邀请。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 否 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有新限定成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL OAuth Token Endpoint URL]**：通常采用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL Client ID]**：从您的Medallia投放团队获取。
* **[!UICONTROL Client Secret]**：从您的Medallia投放团队获取。

![显示此目标的身份验证屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL API Gateway URL]**：从您的Medallia投放团队获取。 通常采用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL Import API Name]**：从您的Medallia投放团队获取。 要在此连接中使用的Medallia Import API（也称为Web馈送）的名称。 您可以将不同的受众激活到不同的导入API，以触发不同的调查程序。

![显示此目标的目标详细信息屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

必须根据用例映射以下目标身份命名空间：

* 对于基于电子邮件的调查，**电子邮件**&#x200B;必须使用&#x200B;**目标字段** > **选择身份命名空间** > **电子邮件**&#x200B;映射为目标字段
* 对于基于短信的调查，**电话**&#x200B;必须使用&#x200B;**目标字段** > **选择身份命名空间** > **电话**&#x200B;映射为目标字段。 电话号码必须是E.164格式，其中包括加号(+)、国际国家/地区呼叫代码、本地区号和电话号码

强烈建议您同时映射其他目标自定义属性以创建个性化调查，并将有关客户的附加信息附加到调查记录：

* 个性化调查通常按名称与客户交谈

   * 将客户的名字映射到&#x200B;**目标字段** > **选择自定义属性** > **属性名称** > **名字**
   * 将客户的姓氏映射到&#x200B;**目标字段** > **选择自定义属性** > **属性名称** > **姓氏**

* 根据需要为任何其他目标自定义属性添加映射

![显示身份和属性映射示例的图像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
>
> 使用&#x200B;**目标字段** > **选择自定义属性** > **属性名称**，与您的Medallia投放团队共享映射的每个目标自定义属性的确切&#x200B;**属性名称**。 您可能希望直接共享映射页面的屏幕快照。

## 导出的数据 {#exported-data}

将区段激活到目标后，请通知您的Medallia交付团队，该团队将能够验证从[!DNL Adobe Experience Platform]导出到Medallia的数据。 请注意，调查只能在成功的数据验证后在Medallia中激活；在此之前，数据将导出到Medallia，但不会向客户触发调查。

下面提供了一个导出数据的JSON示例，该示例使用上面&#x200B;**映射属性和身份**&#x200B;部分屏幕快照中的示例映射：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
