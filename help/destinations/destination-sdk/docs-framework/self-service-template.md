---
title: 文档自助模板//将替换为您的目标名称
description: 使用此模板在Adobe Experience Platform目录中为您的目标创建公共文档。//替换为概述部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 2%

---

# 您的目标连接 {#your-destination}

*浏览此模板时，替换或删除所有斜体段落（从此段落开始）。*

*从更新页面顶部的元数据（标题和描述）开始。 请忽略此页面上的所有UICONTROL实例。 此标记可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 我们将在您提交文档后向文档中添加标记。*

>[!IMPORTANT]
>
>* 按照模板中列出的顺序填写此模板中的所有部分。
>* 此模板很少根据合作伙伴反馈进行更新。 开始为目标创作文档之前，请确保已下载[最新版本的模板](../assets/docs-framework/yourdestination-template.zip)。

## 概述 {#overview}

*提供贵公司的简短概述，包括贵公司为客户提供的价值。 包括产品文档主页的链接，以便进一步阅读。*

>[!IMPORTANT]
>
>此目标连接器和文档页面由&#x200B;*YourDestination*&#x200B;团队创建并维护。 对于任何查询或更新请求，请直接通过&#x200B;*插入链接或电子邮件地址与他们联系，您可以从中获取更新，例如`support@YourDestination.com`。*

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用&#x200B;*YourDestination*&#x200B;目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

*对于移动消息平台：*

*家庭租赁和销售平台想要将移动通知推送到客户的Android和iOS设备，以告知他们之前搜索租赁的区域有100个更新的列表。*

### 用例#2 {#use-case-2}

*对于社交网络平台：*

*运动服装品牌希望通过其社交媒体帐户联系现有客户。 服装品牌可以从自己的CRM中摄取电子邮件地址到Adobe Experience Platform，从自己的离线数据构建受众，并将这些受众发送到YourDestination，以在其客户的社交媒体源中显示广告。*

## 先决条件 {#prerequisites}

*在此部分添加有关客户在Adobe Experience Platform用户界面中开始设置目标之前需要了解的任何信息。 这可能大约为：*

* *需要添加到允许列表*
* 电子邮件散列的&#x200B;*要求*
* *你方的任何帐户详情*
* *如何获取API密钥以连接到您的平台*

*如果对客户有帮助，您可以链接到相关文档。*

## 支持的身份 {#supported-identities}

*在此部分添加有关目标支持的标识的信息。 我们已在表中预填了一些标准值。 删除不应用于目标的值和/或添加任何未预填充的值。*

*YourDestination*&#x200B;支持激活下表所述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请阅读以下有关[ECID](/help/identity-service/features/ecid.md)的文档。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

*在此部分添加有关目标支持的受众的信息。 我们已在表中预填了一些标准值。 使用`✓`和`X`字符标记此目标是否支持您的受众类型。*

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | X | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

*在表中，只保留与您的目标对应的行。 对于“导出”类型，应有一行，对于“导出频率”，应有一行。 删除不适用于目标的值。*

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有&#x200B;*YourDestination*&#x200B;目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出受众的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出类型 | **[!UICONTROL Dataset export]** | 您正在导出未按受众兴趣或资格进行分组或构建的原始数据集。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

*添加在对目标进行身份验证时客户必须填写的字段。 这些字段特定于目标，具体取决于您在Destination SDK中的配置。 目标字段可能与下面列出的字段不同。 请另外包含一个与下面显示的示例屏幕快照类似的屏幕快照。*

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

![显示如何向目标进行身份验证的示例屏幕截图](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Bearer token]**：填写持有者令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

*添加客户在配置新目标时必须填写的字段。 这些字段特定于目标，具体取决于您在Destination SDK中的配置。 目标字段可能与下面列出的字段不同。 请另外包含一个与下面显示的示例屏幕快照类似的屏幕快照。*

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示如何填写目标详细信息的示例屏幕截图](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Account ID]**：您的&#x200B;*目标*&#x200B;帐户ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请阅读有关使用UI订阅目标警报[的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

*根据需要删除 — 如果您正在记录新的流目标，请保留下面的第一段。 如果您要记录新的基于文件的目标，请保留第二段。 如果您正在记录导出数据集的目标，请保留第三段。*

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

有关将数据集导出到此目标的详细说明，请阅读[(Beta)导出数据集](/help/destinations/ui/export-datasets.md)。

### 映射属性和身份 {#map}

*在激活工作流的“映射”步骤中添加有关源字段和目标字段之间支持的映射的信息。 您的目标可能支持导出配置文件属性和/或身份命名空间。 某些字段可能是必填的。 目标属性可以是预定义或自定义的。 指出重要注意事项并使用示例，最好使用屏幕截图。 您可以用作引用的目标页面的两个示例为：*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅德利亚](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 导出的数据/验证数据导出 {#exported-data}

*添加一段关于如何将数据导出到目标的段落。 这将帮助客户确保他们正确地与您的目标集成。 例如，您可以提供类似于下面的JSON示例。 或者，您可以提供目标界面的屏幕截图和信息，显示客户应如何预期受众填充到目标平台中。*

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

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

*您可以提供产品文档或任何其他您认为对客户成功至关重要的资源的更多链接。*
