---
title: 文档自助服务模板//将替换为您的目标名称
description: 使用此模板可在Adobe Experience Platform目录中为您的目标创建公共文档。//替换为“概述”部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 788c02622b5176b41eb6da70bed0994d4824c984
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 1%

---

# YourDestination连接 {#your-destination}

*在完成此模板时，请替换或删除所有斜体段落（从此模板开始）。*

*首先，更新页面顶部的元数据（标题和描述）。 请忽略此页面上的所有UICONTROL实例。 这是一个标记，可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 在您提交文档后，我们会为您的文档添加标记。*

>[!IMPORTANT]
>
>* 按模板中所述的顺序填写此模板中的所有部分。
>* 根据合作伙伴的反馈，此模板不常更新。 在开始为目标位置创作文档之前，请确保已下载 [模板的最新版本](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## 概述 {#overview}

*简要概述您的公司，包括公司为客户提供的价值。 包括指向产品文档主页的链接，以供进一步阅读。*

>[!IMPORTANT]
>
>此文档页面由 *YourDestination* 团队。 如有任何查询或更新请求，请直接联系 *插入链接或电子邮件地址，以访问此处进行更新，例如 `support@YourDestination.com`.*

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 *YourDestination* 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

*对于移动消息平台：*

*一个家庭租赁和销售平台希望将移动通知推送给客户的Android和iOS设备，以便让客户知道，在他们之前搜索的租金区域，有100个更新的房源。*

### 用例#2 {#use-case-2}

*对于社交网络平台：*

*一家运动服装品牌希望通过其社交媒体帐户联系现有客户。 服装品牌可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建区段，并将这些区段发送到您的目标，以在客户的社交媒体信息源中显示广告。*

## 先决条件 {#prerequisites}

*在此部分中添加有关客户在开始在Adobe Experience Platform用户界面中设置目标之前需要注意的任何内容的信息。 这可以是关于：*

* *需要添加到允许列表*
* *电子邮件哈希处理要求*
* *您方面的任何帐户详情*
* *如何获取连接到您平台的API密钥*

*如果相关文档对客户有用，您可以将其链接到相关文档。*

## 支持的身份 {#supported-identities}

*在此部分中添加有关目标支持的身份的信息。 我们已预填表中一些标准值。 删除未应用于您的目标的值以及未预填充的任何值。*

*YourDestination* 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| extern_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

*在表中，仅保留与目标对应的行。 您应该为“导出类型”设置一行，为“导出频率”设置一行。 删除不适用于您的目标的值。*

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 *YourDestination* 目标。 |
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

*添加客户在对目标进行身份验证时必须填写的字段。 这些字段特定于目标，取决于您在Destination SDK中的配置。 目标的字段可能与下面列出的字段不同。 另请包含与下面显示的示例屏幕截图类似的屏幕截图。*

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![显示如何对目标进行身份验证的示例屏幕截图](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL 载体令牌]**:填写承载令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

*添加客户在配置新目标时必须填写的字段。 这些字段特定于目标，取决于您在Destination SDK中的配置。 目标的字段可能与下面列出的字段不同。 另请包含与下面显示的示例屏幕截图类似的屏幕截图。*

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![示例屏幕截图，显示如何填写目标的详细信息](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 *YourDestination* 帐户ID。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 有关将受众区段激活到此目标的说明。

### 映射属性和标识 {#map}

*在激活工作流的映射步骤中添加有关源字段和目标字段之间支持映射的信息。 您的目标可能支持导出配置文件属性、身份命名空间或两者。 某些字段可能是必填字段。 Target属性可以是预定义属性，也可以是自定义属性。 请提出重要注意事项，并使用示例，最好包含屏幕截图。 可用作引用的目标页面的两个示例：*

* *[佩加](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅达利亚](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 导出的数据/验证数据导出 {#exported-data}

*添加有关如何将数据导出到目标的段落。 这将有助于客户确保他们已正确与您的目标集成。 例如，您可以提供类似于下面的示例JSON。 或者，您也可以从目标界面提供屏幕截图和信息，以显示客户应如何预期区段在目标平台中填充。*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

*您可以提供产品文档的进一步链接，或您认为对于客户成功而言非常重要的任何其他资源。*