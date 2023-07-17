---
title: 文档自助模板//将替换为您的目标名称
description: 使用此模板可在Adobe Experience Platform目录中为您的目标创建公共文档。//替换为概述部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 1%

---

# 您的目标连接 {#your-destination}

*浏览此模板时，替换或删除所有斜体段落（从此段落开始）。*

*首先，在页面顶部更新元数据（标题和描述）。 请忽略此页面上的所有UICONTROL实例。 此标记可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 我们会在您提交文档后将标记添加到文档中。*

>[!IMPORTANT]
>
>* 按照模板中列出的顺序填写此模板中的所有部分。
>* 此模板很少根据合作伙伴反馈进行更新。 在开始为目标创作文档之前，请确保已下载 [模板的最新版本](../assets/docs-framework/yourdestination-template.zip).

## 概述 {#overview}

*提供贵公司的简短概览，包括贵公司为客户提供的价值。 包含指向产品文档主页的链接，以供进一步阅读。*

>[!IMPORTANT]
>
>此文档页面由创建 *您的目标* 团队。 如有任何查询或更新请求，请直接通过 *插入链接或电子邮件地址，您可以在其中获取更新，例如 `support@YourDestination.com`.*

## 用例 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 *您的目标* 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

*对于移动消息平台：*

*一家家庭租赁和销售平台希望向顾客的Android和iOS设备推送移动通知，让他们知道，他们之前搜索租房的区域有100个更新的房源。*

### 用例#2 {#use-case-2}

*对于社交网络平台：*

*一家运动服装品牌希望通过其社交媒体帐户吸引现有客户。 服装品牌可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建受众，并将这些受众发送到YourDestination，以便在客户的社交媒体馈送中显示广告。*

## 先决条件 {#prerequisites}

*在此部分中添加有关客户在Adobe Experience Platform用户界面中开始设置目标之前需要了解的任何信息。 这可能与以下内容有关：*

* *需要添加到允许列表*
* *电子邮件哈希处理要求*
* *任何账户详情*
* *如何获取API密钥以连接到您的平台*

*如果对客户有帮助，您可以链接到相关文档。*

## 支持的身份 {#supported-identities}

*在此部分添加有关目标所支持标识的信息。 我们已在表中预填了一些标准值。 删除不适用于目标的值和任何未预填充的值。*

*您的目标* 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 阅读以下文档： [ECID](/help/identity-service/ecid.md) 了解更多信息。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法对电子邮件地址进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 激活时自动散列数据。 |
| extern_id | 自定义用户ID | 当源身份是自定义命名空间时，选择此目标身份。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

*在表中，仅保留与您的目标对应的行。 对于“导出”类型，应有一行，对于“导出频率”，应有一行。 删除不适用于目标的值。*

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出受众的所有成员以及中使用的标识符（姓名、电话号码或其他）。 *您的目标* 目标。 |
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出类型 | **[!UICONTROL 数据集导出]** | 您正在导出未按受众兴趣或资格进行分组或构建的原始数据集。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

*添加客户在对目标进行身份验证时必须填写的字段。 这些字段特定于目标，并且取决于您在Destination SDK中的配置。 您目标的字段可能与下面列出的字段不同。 另请包含类似于下面显示的示例屏幕快照的屏幕快照。*

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![显示如何向目标进行身份验证的示例屏幕快照](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL 持有者令牌]**：填写持有者令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

*添加客户在配置新目标时必须填写的字段。 这些字段特定于目标，并且取决于您在Destination SDK中的配置。 您目标的字段可能与下面列出的字段不同。 另请包含类似于下面显示的示例屏幕快照的屏幕快照。*

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示如何填写目标的详细信息的示例屏幕截图](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 *您的目标* 帐户ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请阅读以下指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

*适当删除 — 如果您要记录新的流目标，请保留以下第一段。 如果您要记录新的基于文件的目标，请保留第二段。 如果您要记录导出数据集的目标，请保留第三段。*

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

读取 [（测试版）导出数据集](/help/destinations/ui/export-datasets.md) 以获取有关将数据集导出到此目标的详细说明。

### 映射属性和身份 {#map}

*在激活工作流的“映射”步骤中添加有关源字段和目标字段之间支持的映射的信息。 您的目标可能支持导出配置文件属性、身份命名空间或两者。 某些字段可能是必填字段。 目标属性可以是预定义或自定义的。 指出重要注意事项并使用示例，最好附上屏幕截图。 您可以用作引用的目标页面的两个示例包括：*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅达利亚](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 导出的数据/验证数据导出 {#exported-data}

*添加一个段落，介绍如何将数据导出到您的目标。 这将帮助客户确保他们正确地与您的目标集成。 例如，您可以提供一个类似于下面的JSON示例。 或者，您可以提供目标界面的屏幕截图和信息，以显示客户应如何期望受众在目标平台中填充。*

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
        "status": "realized"
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

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据治理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

*您可以提供指向产品文档或任何其他您认为对客户的成功很重要的资源的更多链接。*