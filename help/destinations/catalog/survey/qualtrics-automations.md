---
keywords: 流，Qualtrics目标
title: Qualtrics自动化
description: 同步体验和运营客户数据以大规模解锁个性化。 在Qualtrics Experience Id中，使用对Adobe Experience Platform中多个运营数据来源的聚合作为输入，以更好地了解您的客户，并实现有针对性的外联，在了解意图、情绪和体验驱动因素方面缩小差距。
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 3%

---

# Qualtrics自动化

## 概述 {#overview}

同步体验和运营客户数据以大规模解锁个性化。

在Qualtrics Experience iD中将[!DNL Adobe Experience Platform]中多个运营数据源的聚合用作输入，以更好地了解您的客户并实现有针对性的外联，从而在了解意图、情绪和体验驱动因素方面缩小差距。

>[!IMPORTANT]
>
>目标连接器和文档页面由Qualtrics团队创建和维护。 对于任何查询或更新请求，请登录[客户成功中心](https://support-portal.qualtrics.com/)直接与他们联系。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用&#x200B;*Qualtrics自动化*&#x200B;目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

**情景**：公司希望跨各种数字接触点（如其网站和移动设备应用程序）衡量客户满意度。 他们使用[!DNL Adobe Experience Platform]根据用户交互触发Qualtrics调查，如完成购买或访问特定网页。

**结果**：通过收集实时反馈，公司可以改进其客户体验，从而提高满意度和忠诚度。

### 用例#2 {#use-case-2}

**场景**：组织旨在增强其员工入职流程。 他们利用[!DNL Adobe Experience Platform]通过Qualtrics调查从新员工那里收集反馈。 在预定义的入门培训期后，调查将自动触发。

**结果**：持续反馈使组织能够调整和改进新员工上线流程，从而在新员工中提高参与度和工作效率。

## 先决条件 {#prerequisites}

在[!DNL Adobe Experience Platform]中设置Qualtrics目标之前，请确保满足以下先决条件：

* 您拥有Qualtrics帐户。
* 您已从Qualtrics获取必要的API令牌。

### 获取API令牌 {#obtaining-api-token}

以下是从Qualtrics获取API令牌的必要步骤。

1. 登录到您的Qualtrics帐户。
2. 转到&#x200B;**帐户设置**。
3. 选择&#x200B;**Qualtrics ID**。
4. 在此页面上查找&#x200B;**API**&#x200B;部分，其中包含&#x200B;**令牌**&#x200B;字段。 这是API令牌，在目标设置期间是必需的。

## 支持的身份 {#supported-identities}

*Qualtrics Automations*&#x200B;支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 纯文本电子邮件地址 | Qualtrics仅支持纯文本电子邮件地址。 |
| external_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

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
| 导出类型 | **[!UICONTROL Segment export]** | 您正在导出具有&#x200B;*Qualtrics自动化*&#x200B;目标中使用的标识符（姓名、电话号码或其他）的区段（受众）的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

作为身份验证的一部分，您需要提供&#x200B;**用户名**&#x200B;和&#x200B;**密码**。 用户名是您的Qualtrics用户名，密码是您的Qualtrics帐户的API令牌。 要检索API令牌，请按照上面&#x200B;**先决条件**&#x200B;部分中的说明操作。

![身份验证](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL URL]**：在[JSON事件](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About)中找到的URL将触发Qualtrics[中的](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About)工作流。 有关示例，请参见下面的屏幕截图。

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[将受众激活到流式目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

此目标具有打开的架构，因此您可以将任何资产发送到Qualtrics。

#### 映射属性 {#map-attributes}

若要向映射中添加属性，请在添加新映射时选择&#x200B;**自定义属性**。 您可以为属性输入任何名称。 Qualtrics鼓励对属性名称使用&#x200B;*camelCase*&#x200B;命名约定（请参阅下面的屏幕快照示例）。

![自定义属性](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

有关可能的属性映射的示例，请参见下面的屏幕截图。

![映射示例](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### 映射身份标识 {#map-identities}

必须为此目标选择身份命名空间。 目标字段映射的两个可能的源字段是：

| 源字段 | 目标字段 |
|--------------------|-----------------------|
| IdentityMap：电子邮件 | 身份：电子邮件 |
| IdentityMap： ECID | 标识： external_id |

有关示例，请参见下面的屏幕截图。

![身份命名空间](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## 导出的数据/验证数据导出 {#exported-data}

如前所述，此目标使用开放的架构，因此任何属性都可以发送到Qualtrics。 尽管如此，发送给Qualtrics的数据将遵循以下结构：

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

要验证是否已在Qualtrics中摄取数据，请转到包含&#x200B;**JSON事件**&#x200B;的工作流，从该处转到&#x200B;**运行历史记录**，您应在该处看到工作流的执行。 每个工作流的状态为&#x200B;**成功**&#x200B;或&#x200B;**失败**。 选择特定执行会显示有关该执行的更多信息，从而允许您在遇到任何问题时进行故障排除。

如果&#x200B;**运行历史记录**&#x200B;中没有可见的执行，则表示尚未触发工作流，这表示可能存在问题。 请确保工作流已启用，并且&#x200B;**中目标中的** URL[!DNL Adobe Experience Platform]正确。 工作流执行不是即时的，因此您可能必须等待一段时间才能完成。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
