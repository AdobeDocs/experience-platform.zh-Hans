---
title: (API)OracleEloqua连接
description: (API) EloquaOracle允许您导出帐户数据，并在OracleEloqua中激活该数据，以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 使营销人员能够规划和执行营销活动，同时为其潜在客户提供个性化的客户体验。 借助集成的商机管理和轻松的营销活动创建，它可帮助营销人员在其购买者的历程中在适当的时间吸引适当的受众，并可通过精致的扩展来跨渠道（包括电子邮件、显示搜索、视频和移动设备）吸引受众。 销售团队能够以更快的速度完成更多交易，从而通过实时洞察提高营销投资回报率。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [更新联系人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 操作 [!DNL Oracle Eloqua] REST API，它允许您将区段中的标识更新为 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 用途 [基本身份验证](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 以与 [!DNL Oracle Eloqua] REST API。 向您的验证的说明 [!DNL Oracle Eloqua] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以根据用户的Adobe Experience Platform配置文件中的属性，为其提供个性化体验。 您可以从离线数据构建区段并将这些区段发送到 [!DNL Oracle Eloqua]，以便在Adobe Experience Platform中更新区段和配置文件后立即显示在用户的馈送中。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Oracle Eloqua] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档，了解 [“区段成员资格详细信息”架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指南。

### [!DNL Oracle Eloqua] 先决条件 {#prerequisites-destination}

为了将数据从Platform导出到 [!DNL Oracle Eloqua] 您需要拥有 [!DNL Oracle Eloqua] 帐户。

#### 收集 [!DNL Oracle Eloqua] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Oracle Eloqua] 目标：

| 凭据 | 描述 |
| --- | --- |
| `Username` | 您的用户名 [!DNL Oracle Eloqua] 帐户。 |
| `Password` | 您的密码 [!DNL Oracle Eloqua] 帐户。 |

## 护栏 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自定义联系人字段是使用以下期间选择的区段的名称自动创建的 **[!UICONTROL 选择区段]** 步骤。


* [!DNL Oracle Eloqua] 具有250个自定义联系人字段的最大限制。
* 在导出新区段之前，请确保Platform区段的数量和以下范围内的现有区段的数量： [!DNL Oracle Eloqua] 不要超过此限制。
* 如果超过此限制，您将在Experience Platform中遇到错误。 这是因为 [!DNL Oracle Eloqua] API无法验证请求，并使用 —  *400：存在验证错误*  — 描述问题的错误消息。
* 如果您已达到以上指定的限制，则需要从目标中删除现有映射，并删除中相应的自定义联系人字段。 [!DNL Oracle Eloqua] 帐户，然后才能导出更多区段。

* 请参阅 [oracleEloqua创建联系人字段](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 页面，以了解有关其他限制的信息。

## 支持的身份 {#supported-identities}

[!DNL Oracle Eloqua] 支持更新下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 示例 | 描述 | 必需 |
|---|---|---|---|
| `EloquaId` | `111111` | 联系人的唯一标识符。 | 是 |

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL (API) Oracle Eloqua]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 向目标进行身份验证 {#authenticate}

填写下面的必填字段。 请参阅 [收集 [!DNL Oracle Eloqua] 凭据](#gather-credentials) 部分获取任何指导。
* **[!UICONTROL 密码]**：您的密码 [!DNL Oracle Eloqua] 帐户。
* **[!UICONTROL 用户名]**：您的用户名 [!DNL Oracle Eloqua] 帐户。

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的Platform UI屏幕快照。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的详细信息有效，则UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的Platform UI屏幕快照。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Oracle Eloqua] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。

`EloquaID` 需要更新与标识对应的属性。 此 `emailAddress` 另外也很必要，因为如果不使用API，API会引发如下所示的错误：

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

中指定的属性 **[!UICONTROL 目标字段]** 应按照“属性映射”表中的说明进行命名，因为这些属性将构成请求正文。

中指定的属性 **[!UICONTROL 源字段]** 请勿遵守任何此类限制。 您可以根据需要进行映射，但是，如果数据格式在推送到时不正确 [!DNL Oracle Eloqua] 这会导致错误。

例如，您可以映射 **[!UICONTROL 源字段]** 身份命名空间 `contact key`， `ABC ID` 等等。 到 **[!UICONTROL 目标字段]** ： `EloquaID` 在确保ID值符合接受的格式之后 [!DNL Oracle Eloqua].

要将XDM字段正确映射到 [!DNL Oracle Eloqua] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别并根据需要选择属性。
   * 重复这些步骤以添加以下XDM配置文件架构与 [!DNL Oracle Eloqua] 实例： |源字段|目标字段|必填| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`|是 | |`IdentityMap: Eid`|`Identity: EloquaId`|是 |

   * 下面显示了使用这些映射的示例：
      ![具有属性映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >两者都是 `emailAddress` 和 `EloquaId` 目标属性映射是必需的。

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

>[!NOTE]
>
>当向发送联系人字段信息时，目标会在每次执行时自动为所选区段名称添加唯一标识符的后缀 [!DNL Oracle Eloqua]. 这可确保与区段名称对应的联系人字段名称不重叠。 请参阅 [验证数据导出](#exported-data) 部分屏幕快照示例 [!DNL Oracle Eloqua] “联系人详细信息”页面，其中包含使用区段名称创建的自定义联系人字段。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** 选项卡，然后选择区段名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数对应于区段内的计数。
   ![显示区段的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登录到 [!DNL Oracle Eloqua] 网站，然后导航到 **[!UICONTROL 联系人概述]** 页面以检查是否已添加区段中的配置文件。 要查看区段状态，请向下展开至 **[!UICONTROL 联系人详细信息]** 页面，并检查是否已创建具有选定区段名称作为其前缀的联系人字段。

![oracleEloqua UI屏幕截图，其中显示“联系人详细信息”页面，该页面带有使用区段名称创建的自定义联系人字段。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

在创建目标时，您可能会收到以下错误消息之一： `400: There was a validation error` 或 `400 BAD_REQUEST`. 当您超过250个自定义联系人字段限制时，会发生这种情况，如 [护栏](#guardrails) 部分。 要修复此错误，请确保您不超过 [!DNL Oracle Eloqua].
![平台UI屏幕截图显示错误。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

请参阅 [[!DNL Oracle Eloqua] HTTP状态代码](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 验证错误](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 页以了解状态和错误代码的完整列表及其说明。

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL Oracle ELoqua] 文档如下所示：
* [oracleEloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [用于OracleEloquaMarketing Cloud服务的REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)