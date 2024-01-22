---
keywords: 流，Qualtrics目标
title: Qualtrics自动化
description: 同步体验和运营客户数据以大规模解锁个性化。 在Qualtrics Experience Id中，使用对Adobe Experience Platform中多个运营数据来源的聚合作为输入，以更好地了解您的客户，并实现有针对性的外联，在了解意图、情绪和体验驱动因素方面缩小差距。
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---

# Qualtrics自动化

## 概述 {#overview}

同步体验和运营客户数据以大规模解锁个性化。

在Qualtrics Experience Id中，使用对Adobe Experience Platform中多个运营数据来源的聚合作为输入，以更好地了解您的客户，并实现有针对性的外联，在了解意图、情绪和体验驱动因素方面缩小差距。

>[!IMPORTANT]
>
>目标连接器和文档页面由Qualtrics团队创建和维护。 如有任何查询或更新请求，请登录 [客户成功中心](https://support-portal.qualtrics.com/).

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 *Qualtrics自动化* 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

**方案**：公司希望跨各种数字接触点（如其网站和移动应用程序）衡量客户满意度。 他们使用Adobe Experience Platform根据用户交互来触发Qualtrics调查，例如完成购买或访问特定网页。

**结果**：通过收集实时反馈，公司可以对其客户体验进行数据驱动型改进，从而提高满意度和忠诚度。

### 用例#2 {#use-case-2}

**方案**：组织旨在增强员工入门流程。 他们利用Adobe Experience Platform通过Qualtrics调查从新员工那里收集反馈。 在预定义的入门培训期后，调查将自动触发。

**结果**：持续反馈使组织能够调整和改进载入流程，从而提高新员工的参与度和工作效率。

## 先决条件

在Adobe Experience Platform中设置Qualtrics目标之前，请确保满足以下先决条件：

* 您拥有Qualtrics帐户。
* 您已从Qualtrics获取必要的API令牌。

### 获取API令牌

以下是从Qualtrics获取API令牌的必要步骤。

1. 登录到您的Qualtrics帐户。
2. 转到 **帐户设置**.
3. 选择 **Qualtrics ID**.
4. 在此页面上，查找 **API** 部分，它包含 **令牌** 字段。 这是API令牌，在目标设置期间是必需的。

## 支持的身份 {#supported-identities}

*Qualtrics自动化* 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 纯文本电子邮件地址 | Qualtrics仅支持纯文本电子邮件地址。 |
| external_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员以及中使用的标识符（姓名、电话号码或其他）。 *Qualtrics自动化* 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

作为身份验证的一部分，您需要提供 **用户名** 和 **密码**. 用户名是您的Qualtrics用户名，密码是您的Qualtrics帐户的API令牌。 要检索API令牌，请按照 **先决条件** 部分。

![身份验证](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL URL]**：在中找到URL [JSON事件](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) 触发您的 [Qualtrics中的工作流](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). 有关示例，请参见下面的屏幕截图。

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

此目标具有打开的架构，因此您可以将任何资产发送到Qualtrics。

#### 映射属性

要向映射添加属性，只需选择 **自定义属性** 添加新映射时。 您可以为属性输入任何名称。 Qualtrics鼓励 *camelCase* 属性名称的命名约定（请参阅下面的屏幕快照以了解示例）。

![自定义属性](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

有关可能的属性映射的示例，请参见下面的屏幕截图。

![映射示例](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### 映射身份

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

要验证是否已在Qualtrics中摄取数据，请转到包含 **JSON事件**，从那里，转到 **运行历史记录** 其中，您应会看到工作流的执行。 每个工作流的状态为 **已成功** 或 **失败**. 选择特定执行会显示有关该执行的更多信息，从而允许您在遇到任何问题时进行故障排除。

如果中没有可见的执行 **运行历史记录**，这意味着尚未触发工作流，这表示可能存在问题。 确保已启用工作流，并且 **URL** Adobe Experience Platform中的目标中的是正确的。 工作流执行不是即时的，因此您可能必须等待一段时间才能完成。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
