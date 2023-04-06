---
title: (API)OracleEloqua连接
description: (API)OracleEloqua目标允许您导出帐户数据，并在OracleEloqua中激活它以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: e8aa09545c95595e98b4730188bd8a528ca299a9
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 使营销人员能够在为潜在客户提供个性化客户体验的同时，规划和执行营销活动。 通过集成的潜在客户管理和轻松的营销活动创建，它可帮助营销人员在购买者历程的适当时间吸引适当的受众，并优雅地扩展以跨渠道（包括电子邮件、展示搜索、视频和移动设备）访问受众。 销售团队可以更快地完成更多交易，从而通过实时分析提高营销ROI。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [更新联系人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 操作 [!DNL Oracle Eloqua] REST API，它允许您 **更新身份** 在区段内输入 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 使用 [基本身份验证](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 与 [!DNL Oracle Eloqua] REST API。 验证的说明 [!DNL Oracle Eloqua] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

在线平台的营销部门希望向策划的潜在客户受众广播基于电子邮件的营销活动。 该平台的营销团队可以通过Adobe Experience Platform更新现有的潜在客户信息，从他们自己的离线数据构建区段，并将这些区段发送到 [!DNL Oracle Eloqua]，然后用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL Oracle Eloqua] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档，以了解 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

### [!DNL Oracle Eloqua] 先决条件 {#prerequisites-destination}

要将数据从Platform导出到 [!DNL Oracle Eloqua] 帐户 [!DNL Oracle Eloqua] 帐户。

#### 收集 [!DNL Oracle Eloqua] 凭据 {#gather-credentials}

在验证到 [!DNL Oracle Eloqua] 目标：

| 凭据 | 描述 |
| --- | --- |
| `Username` | 您的用户名 [!DNL Oracle Eloqua] 帐户。 |
| `Password` | 您的密码 [!DNL Oracle Eloqua] 帐户。 |

## 护栏 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自定义联系人字段会使用在 **[!UICONTROL 选择区段]** 中。


* [!DNL Oracle Eloqua] 最多限制为250个自定义联系字段。
* 在导出新区段之前，请确保平台区段的数量和 [!DNL Oracle Eloqua] 不要超过此限制。
* 如果超出此限制，您将在Experience Platform中遇到错误。 这是因为 [!DNL Oracle Eloqua] API无法验证请求，并以 —  *400:验证错误*  — 描述问题的错误消息。
* 如果您已达到上面指定的限制，则需要从目标中删除现有映射，并删除 [!DNL Oracle Eloqua] 帐户。

* 请参阅 [[!DNL Oracle Eloqua] 创建联系人字段](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 页面以了解有关其他限制的信息。

## 支持的身份 {#supported-identities}

[!DNL Oracle Eloqua] 支持更新下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 必需 |
|---|---|---|
| `EloquaId` | 联系人的唯一标识符。 | 是 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 对于Platform中的每个选定区段， [!DNL Oracle Eloqua] 区段状态会从平台中更新为其区段状态。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | <ul><li>流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL (API) Oracle Eloqua]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 对目标进行身份验证 {#authenticate}

填写以下必填字段。 请参阅 [收集 [!DNL Oracle Eloqua] 凭据](#gather-credentials) 部分。
* **[!UICONTROL 密码]**:您的密码 [!DNL Oracle Eloqua] 帐户。
* **[!UICONTROL 用户名]**:您的用户名 [!DNL Oracle Eloqua] 帐户。

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![Platform UI屏幕截图，其中显示了如何进行身份验证。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态为绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Oracle Eloqua] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。

将XDM字段映射到 [!DNL Oracle Eloqua] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别，然后选择XDM属性或 **[!UICONTROL 选择身份命名空间]** 并选择一个身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 选择身份，或选择 **[!UICONTROL 选择自定义属性]** 和在 **[!UICONTROL 属性名称]** 字段。 您提供的属性名称应与 [!DNL Oracle Eloqua]. 请参阅 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) ，以获取可在 [!DNL Oracle Eloqua].
   * 重复这些步骤，在XDM配置文件架构和 [!DNL Oracle Eloqua]: |源字段 |目标字段 |必填 | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`|是 | |`xdm: personalEmail.address`|`Attribute: emailAddress`|是 | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * 下面显示了具有上述映射的示例：
      ![Platform UI屏幕截图示例，其中包含属性映射。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 在 **[!UICONTROL 目标字段]** 名称应与 [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 因为这些属性将形成请求正文。
>* 在 **[!UICONTROL 源字段]** 不要遵守任何此类限制。 您可以根据需要映射数据格式，但如果数据格式在推送到 [!DNL Oracle Eloqua] 这会导致错误。 例如，您可以映射 **[!UICONTROL 源字段]** 标识命名空间 `contact key`, `ABC ID` 等。 to **[!UICONTROL 目标字段]** : `EloquaId` 确保ID值与接受的格式匹配 [!DNL Oracle Eloqua].
>* 的 `EloquaID` 必须进行映射才能更新与标识对应的属性。
>* 的 `emailAddress` 需要映射。 如果没有该函数，API会引发错误，如下所示：
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

完成为目标连接提供映射后，请选择 **[!UICONTROL 下一个]**.

>[!NOTE]
>
>在向发送联系人字段信息时，目标在每次执行时自动为所选区段名称添加唯一标识符后缀 [!DNL Oracle Eloqua]. 这可确保与区段名称对应的联系人字段名称不会重叠。 请参阅 [验证数据导出](#exported-data) 部分屏幕截图示例 [!DNL Oracle Eloqua] “联系人详细信息”页面，其中包含使用区段名称创建的自定义联系人字段。

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** ，然后选择区段名称。
   ![Platform UI屏幕截图示例，其中显示了目标激活数据。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 监控区段摘要，并确保用户档案的计数与区段内的计数相对应。
   ![平台UI屏幕截图示例，其中显示了区段。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登录到 [!DNL Oracle Eloqua] 网站，然后导航到 **[!UICONTROL 联系人概述]** 页面来检查是否已添加区段中的用户档案。 要查看区段状态，请向下展开 **[!UICONTROL 联系人详细信息]** 页面，并检查是否已创建以选定区段名称作为前缀的联系人字段。

![Oracle雄辩UI屏幕截图，显示“联系人详细信息”页面，其中包含使用区段名称创建的自定义联系人字段。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

创建目标时，您可能会收到以下错误消息之一： `400: There was a validation error` 或 `400 BAD_REQUEST`. 如果超过250个自定义联系字段限制，则会发生这种情况，如 [护栏](#guardrails) 中。 要修复此错误，请确保您未超过 [!DNL Oracle Eloqua].
![显示错误的平台UI屏幕截图。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

请参阅 [[!DNL Oracle Eloqua] HTTP状态代码](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 验证错误](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 页面，以获取状态和错误代码的完整列表，并提供说明。

## 其他资源 {#additional-resources}

有关更多详细信息，请参阅 [!DNL Oracle Eloqua] 文档：

* [OracleEloqua营销自动化](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [用于Oracle雄辩Marketing Cloud服务的REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)