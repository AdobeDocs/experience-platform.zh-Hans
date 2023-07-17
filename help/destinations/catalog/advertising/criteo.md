---
keywords: 广告；标准；
title: 标准连接
description: 标准支持可信且有影响力的广告，为开放互联网上的每位消费者带来更丰富的体验。 凭借世界上最大的商业数据集和同类最佳的AI，Criteo可确保购物历程中的每个接触点都经过个性化，以便在适当的时间通过适当的广告吸引客户。
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 9ccfbeb6ef36b10b8ecbfc25797c26980e7d1dcd
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 3%

---

# (Beta)标准连接

## 概述 {#overview}

>[!IMPORTANT]
>
>此文档页面由Criteo创建。 此产品目前为测试版，其功能可能会有变动。 如有任何查询或更新请求，请直接与标准联系 [此处](mailto:criteoTechnicalPartnerships@criteo.com).

标准支持可信且有影响力的广告，为开放互联网上的每位消费者带来更丰富的体验。 凭借世界上最大的商业数据集和同类最佳的AI，Criteo可确保购物历程中的每个接触点都经过个性化，以便在适当的时间通过适当的广告吸引客户。

## 先决条件 {#prerequisites}

* 您需要具有管理员用户帐户 [标准管理中心](https://marketing.criteo.com).
* 您将需要您的Criteo广告商ID（如果您没有此ID，请咨询您的Criteo联系人）。
* 您需要提供 [!DNL GUM caller ID]，以防您使用 [!DNL GUM ID] 作为标识符。

## 限制 {#limitations}

* 标准仅接受 [!DNL SHA-256] — 散列和纯文本电子邮件(将转换为 [!DNL SHA-256] 之前)。 请勿发送任何PII（个人身份信息，如个人姓名或电话号码）。
* 标准要求客户端至少提供一个标识符。 它优先处理 [!DNL GUM ID] 作为经过哈希处理的电子邮件中的标识符，因为它有助于提高匹配率。

![先决条件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支持的身份 {#supported-identities}

标准支持激活下表中描述的标识。 详细了解 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| 目标身份 | 描述 | 注意事项 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256算法对电子邮件地址进行哈希处理 | Adobe Experience Platform支持纯文本和SHA-256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 [!UICONTROL 应用转换] 选项，以使Platform在激活时自动散列数据。 |
| `gum_id` | 标准 [!DNL GUM] Cookie标识符 | [!DNL GUM IDs] 允许客户在其用户标识系统与Criteo的用户标识之间保持通信([!DNL UID])。 如果标识符类型为 `gum_id`，另一个参数， [!DNL GUM Caller ID]还必须包含。 请联系您的Criteo客户团队获取相应的 [!DNL GUM Caller ID] 或获取有关此内容的更多信息 [!DNL GUM ID] 同步（如果需要）。 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
| --- | --- | --- |
| 导出类型 | 受众导出 | 您正在导出受众的所有成员以及中使用的标识符（姓名、电话号码或其他）。 [!DNL Criteo] 目标。 |
| 导出频率 | 流 | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](../../destination-types.md#streaming-destinations). |

## 用例 {#use-cases}

为了帮助您更好地了解如何使用 [!DNL Criteo] 目标，以下是Adobe Experience Platform客户可以通过实现的一些目标 [!DNL Criteo]：

### 用例1 ：获取流量

利用相关的产品选件和灵活的创意展示您的业务。 通过智能产品推荐，您的广告将自动包含最可能触发访问和参与度的产品。 通过灵活定位，您可以从Criteo的商务数据集或从您自己的潜在客户列表和AdobeCDP区段构建受众。

### 用例2：提高网站转化率

当访客离开您的网站时，提醒他们缺少什么，重新定位可通过显示特殊优惠和超级相关优惠来提高转化率的广告，无论他们接下来走到哪里。 连接您的AdobeCDP受众，重新吸引现有客户或定位类似于您最忠诚购物者的消费者。

## 连接到标准 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 验证标准

连接步骤如下：

1. 登录到Adobe Experience Platform并连接到Criteo目标。

   ![登录](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 您将被重定向到标准以授权连接。 您可能需要首先使用标准凭据登录：

   ![标准登录](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![标准登录](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![标准登录](../../assets/catalog/advertising/criteo/log-in-3.png)


### 连接参数 {#connection-parameters}

在对目标进行身份验证后，请填写以下连接参数。

![连接参数](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 字段 | 描述 | 必需 |
| --- | --- | --- |
| 名称 | 帮助您将来识别此目标的名称。 您在此处选择的名称将为 [!DNL Audience] 名称时，无法在以后修改此名称。 | 是 |
| 描述 | 帮助您将来标识此目标的描述。 | 否 |
| 广告商ID | 您组织的标准广告商ID。 请联系您的Criteo客户经理以获取此信息。 | 是 |
| 标准 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 您的组织的所有成员。 请联系您的Criteo客户团队获取相应的 [!DNL GUM Caller ID] 或获取有关此内容的更多信息 [!DNL GUM] 同步（如果需要）。 | 是，无论何时 [!DNL GUM ID] 作为标识符提供 |

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate-segments}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将用户档案和受众激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

您可以在中查看导出的受众 [标准管理中心](https://marketing.criteo.com/audience-manager/dashboard).

由收到的添加用户个人资料的请求正文 [!DNL Criteo] 连接看起来类似于下面的样子：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

由收到的删除用户配置文件的请求正文 [!DNL Criteo] 连接看起来类似于下面的样子：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## 数据使用和管理 {#data-usage}

在处理您的数据时，所有Adobe Experience Platform目标都符合数据使用策略。 有关Adobe Experience Platform如何实施数据管理的详细信息，请参阅 [数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源

* [Criteo帮助中心](https://help.criteo.com/kb/en)
* [标准开发人员门户](https://developers.criteo.com)
