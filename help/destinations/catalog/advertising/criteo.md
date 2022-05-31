---
keywords: 广告；克雷蒂奥；
title: Criteo连接
description: Criteo支持可信且有影响力的广告，通过开放互联网为每位消费者提供更丰富的体验。 Criteo拥有世界上最大的商业数据集和一流的人工智能，可确保整个购物历程中的每个接触点都经过个性化，以便在适当的时间通过正确的广告来吸引客户。
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 07974f92c741d74e6d0289120538655379d3ca35
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 2%

---

# (Beta)Criteo连接

## 概述 {#overview}

>[!IMPORTANT]
>
>此文档页面由Criteo创建。 此产品目前是测试版产品，功能可能会发生更改。 如有任何查询或更新请求，请直接联系Criteo [此处](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo支持可信且有影响力的广告，通过开放互联网为每位消费者提供更丰富的体验。 Criteo拥有世界上最大的商业数据集和一流的人工智能，可确保整个购物历程中的每个接触点都经过个性化，以便在适当的时间通过正确的广告来吸引客户。

## 先决条件 {#prerequisites}

* 您需要具有管理员用户帐户 [Criteo管理中心](https://marketing.criteo.com).
* 您将需要您的Criteo广告商ID（如果您没有此ID，请咨询您的Criteo联系人）。
* 你需要提供 [!DNL GUM caller ID]，以防您使用 [!DNL GUM ID] 作为标识符。

## 限制 {#limitations}

* Criteo当前不支持从受众中删除用户。
* 克里蒂奥只接受 [!DNL SHA-256] — 经过哈希处理的纯文本电子邮件(要转换为 [!DNL SHA-256] 发送之前)。 请勿发送任何PII（个人身份信息，如个人姓名或电话号码）。
* Criteo需要客户端提供至少一个标识符。 它优先考虑 [!DNL GUM ID] 作为经过哈希处理的电子邮件的标识符，因为这有助于提高匹配率。

![先决条件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支持的身份 {#supported-identities}

Criteo支持激活下表所述的身份。 详细了解 [标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target标识 | 描述 | 注意事项 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA-256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 [!UICONTROL 应用转换] 选项，以使Platform自动对激活数据进行哈希处理。 |
| `gum_id` | 克里蒂奥 [!DNL GUM] cookie标识符 | [!DNL GUM IDs] 允许客户在其用户识别系统与Criteo的用户识别([!DNL UID])。 如果标识符类型为 `GUM`，则 [!DNL GUM Caller ID]，也必须包含。 请联系您的Criteo客户团队，以获取相应的 [!DNL GUM Caller ID] 或获取有关此项的更多信息 `GUM` 同步（如果需要）。 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
| --- | --- | --- |
| 导出类型 | 区段导出 | 您要导出区段（受众）的所有成员，以及 [!DNL Criteo] 目标。 |
| 导出频度 | 流 | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](../../destination-types.md#streaming-destinations). |

## 用例 {#use-cases}

以帮助您更好地了解如何使用 [!DNL Criteo] 目标，以下是Adobe Experience Platform客户可以通过 [!DNL Criteo]:

### 用例1 :获取流量

通过相关的产品优惠和灵活的创意展示您的业务。 借助智能产品推荐，您的广告将自动显示最有可能触发访问和参与的产品。 灵活定位允许您从Criteo的商务数据集或您自己的潜在客户列表和AdobeCDP区段构建受众。

### 用例2 :提高网站转化率

当访客离开您的网站时，请提醒他们重定位广告会丢失什么，这些广告会通过显示特惠优惠和与高度相关的选件来提高转化，无论他们下一步去哪里。 连接您的AdobeCDP区段，以重新吸引现有客户或定位与最忠诚的购物者类似的消费者。

## 连接到Criteo {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 验证Criteo

连接的步骤如下：

1. 登录到Adobe Experience Platform并连接到Criteo目标。

   ![登录](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 系统会将您重定向到Criteo以授权连接。 您可能需要首先使用Criteo凭据登录：

   ![Criteo登录](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Criteo登录](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Criteo登录](../../assets/catalog/advertising/criteo/log-in-3.png)


### 连接参数 {#connection-parameters}

在对目标进行身份验证后，请填写以下连接参数。

![连接参数](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 字段 | 描述 | 必需 |
| --- | --- | --- |
| 名称 | 一个名称，可帮助您识别未来的此目标。 您在此处选择的名称将是 [!DNL Audience] 名称，无法在以后的阶段修改。 | 是 |
| 描述 | 此描述可帮助您在将来确定此目标。 | 否 |
| API版本 | Criteo API版本。 请选择预览。 | 是 |
| 广告商ID | 贵组织的关键广告商ID。 请联系您的Criteo客户经理以获取此信息。 | 是 |
| 克里蒂奥 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 你的组织。 请联系您的Criteo客户团队，以获取相应的 [!DNL GUM Caller ID] 或获取有关此项的更多信息 [!DNL GUM] 同步（如果需要）。 | 是，只要 [!DNL GUM ID] 作为标识符提供 |

## 将区段激活到此目标 {#activate-segments}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

您可以在 [犯罪管理中心](https://marketing.criteo.com/audience-manager/dashboard).

收到的请求正文 [!DNL Criteo] 连接类似于以下内容：

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

## 数据使用和管理 {#data-usage}

所有Adobe Experience Platform目标在处理数据时都符合数据使用策略。 有关Adobe Experience Platform如何实施数据管理的详细信息，请阅读 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## 其他资源

* [克里蒂奥帮助中心](https://help.criteo.com/kb/en)
* [Criteo开发人员门户](https://developers.criteo.com)
