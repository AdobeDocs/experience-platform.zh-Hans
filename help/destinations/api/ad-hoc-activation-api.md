---
keywords: Experience Platform；目标api；临时激活；临时激活受众
solution: Experience Platform
title: 通过临时激活API将受众激活到批处理目标
description: 本文说明了用于通过临时激活API激活受众的端到端工作流，包括在激活之前执行的分段作业。
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 通过临时激活API将受众按需激活到批处理目标

>[!IMPORTANT]
>
>完成Beta阶段后，[!DNL ad-hoc activation API]现在可供所有Experience Platform客户正式使用(GA)。 在GA版本中，API已升级到版本2。 步骤4 （[获取最新的受众导出作业ID](#segment-export-id)）不再是必需的，因为API不再需要导出ID。
>
>有关详细信息，请参阅本教程中下面的[进一步运行临时激活作业](#activation-job)。

## 概述 {#overview}

临时激活API允许营销人员以编程方式快速高效地将受众受众激活到目标，以满足立即激活的需求。

使用临时激活API将完整文件导出到所需的文件接收系统。 仅基于[批处理文件的目标](../destination-types.md#file-based)支持临时受众激活。

下图说明了通过临时激活API激活受众的端到端工作流，包括每24小时在Experience Platform中执行一次的分段作业。

![临时激活](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## 用例 {#use-cases}

### Flash销售或促销

一家在线retailer正准备进行限时限价促销，希望能在短时间内通知客户。 通过Experience Platform临时激活API，营销团队可以按需导出受众，并快速向客户群发送促销电子邮件。

### 当前事件或突发新闻

一家酒店预计未来几天天气会很恶劣，团队希望尽快通知到来的客人，以便他们做出相应计划。 营销团队可以使用Experience Platform临时激活API根据需要导出受众并通知来宾。

### 集成测试

IT经理可以使用Experience Platform临时激活API按需导出受众，以便测试他们与Adobe Experience Platform的自定义集成，并确保一切正常运行。

## 护栏 {#guardrails}

在使用临时激活API时，请牢记以下护栏。

* 目前，每个临时激活作业最多可以激活80个受众。 尝试激活每个作业超过80个受众将导致作业失败。 此行为可能会在未来版本中发生更改。
* 临时激活作业无法与计划的[受众导出作业](../../segmentation/api/export-jobs.md)并行运行。 在运行临时激活作业之前，请确保已完成计划的受众导出作业。 有关如何监视激活流状态的信息，请参阅[目标数据流监视](../../dataflows/ui/monitor-destinations.md)。 例如，如果激活数据流显示&#x200B;**[!UICONTROL 正在处理]**&#x200B;状态，请等待它完成后再运行临时激活作业。
* 不要为每个受众运行多个并发临时激活作业。

## 分段注意事项 {#segmentation-considerations}

Adobe Experience Platform每24小时运行一次计划的分段作业。 临时激活API基于最新的分段结果运行。

## 步骤1：先决条件 {#prerequisites}

在调用Adobe Experience Platform API之前，请确保您满足以下先决条件：

* 您拥有有权访问Adobe Experience Platform的组织帐户。
* 您的Experience Platform帐户已为Adobe Experience Platform API产品配置文件启用`developer`和`user`角色。 请与您的[Admin Console](../../access-control/home.md)管理员联系，为您的帐户启用这些角色。
* 你有Adobe ID。 如果您没有Adobe ID，请转到[Adobe Developer Console](https://developer.adobe.com/console)并创建新帐户。

## 步骤2：收集身份证明 {#credentials}

要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的资源可以隔离到特定的虚拟沙箱。 在对Experience Platform API的请求中，您可以指定将执行操作的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

* 内容类型： `application/json`

## 步骤3：在Experience Platform UI中创建激活流程 {#activation-flow}

在通过临时激活API激活受众之前，您必须首先在Experience Platform UI中为所选目标配置激活流程。

这包括进入激活工作流，选择受众，配置计划并激活它们。 您可以使用UI或API创建激活流：

* [使用Experience Platform UI创建批量配置文件导出目标的激活流](../ui/activate-batch-profile-destinations.md)
* [使用流服务API连接到批处理配置文件导出目标并激活数据](../api/connect-activate-batch-destinations.md)

## 步骤4：获取最新的受众导出作业ID（v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在临时激活API v2中，您无需获取最新的受众导出作业ID。 您可以跳过此步骤并继续执行下一个步骤。

为批处理目标配置激活流后，计划的分段作业每24小时自动运行一次。

在运行临时激活作业之前，必须获取最新受众导出作业的ID。 您必须在临时激活作业请求中传递此ID。

按照[此处](../../segmentation/api/export-jobs.md#retrieve-list)的说明检索所有受众导出作业的列表。

在响应中，查找包含下面架构属性的第一个记录。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

受众导出作业ID位于`id`属性中，如下所示。

![受众导出作业ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步骤5：运行临时激活作业 {#activation-job}

Adobe Experience Platform每24小时运行一次计划的分段作业。 临时激活API基于最新的分段结果运行。

>[!IMPORTANT]
>
>请注意以下一次性限制：在运行临时激活作业之前，请确保根据您在[步骤3 — 在Experience Platform UI中创建激活流](#activation-flow)中设置的计划首次激活受众时起已过去至少一个小时。

在运行临时激活作业之前，请确保受众的计划受众导出作业已完成。 有关如何监视激活流状态的信息，请参阅[目标数据流监视](../../dataflows/ui/monitor-destinations.md)。 例如，如果激活数据流显示&#x200B;**[!UICONTROL 正在处理]**&#x200B;状态，请等待它完成后再运行临时激活作业以导出完整文件。

受众导出作业完成后，您可以触发激活。

>[!NOTE]
>
>目前，每个临时激活作业最多可以激活80个受众。 尝试激活每个作业超过80个受众将导致作业失败。 此行为可能会在未来版本中发生更改。

### 请求 {#request}

>[!IMPORTANT]
>
>必须在请求中包含`Accept: application/vnd.adobe.adhoc.activation+json; version=2`标头，才能使用临时激活API v2。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要将受众激活到的目标实例的ID。 您可以导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 浏览]**&#x200B;选项卡，然后单击所需的目标行在右边栏中显示目标ID，从而从Experience Platform UI获取这些ID。 有关详细信息，请阅读[目标工作区文档](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到所选目标的受众的ID。 您可以使用临时API导出Experience Platform生成的受众以及外部（自定义上传）受众。 激活外部受众时，请使用系统生成的ID而不是受众ID。 您可以在受众UI的受众摘要视图中找到系统生成的ID。<br> ![不应选择的受众ID视图。](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "不应选择的受众ID视图。"){width="100" zoomable="yes"} <br> ![应使用的系统生成的受众ID的视图。](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "应该使用的系统生成的受众ID的视图。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### 使用导出ID的请求 {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要将受众激活到的目标实例的ID。 您可以导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 浏览]**&#x200B;选项卡，然后单击所需的目标行在右边栏中显示目标ID，从而从Experience Platform UI获取这些ID。 有关详细信息，请阅读[目标工作区文档](/help/destinations/ui/destinations-workspace.md#browse)。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到所选目标的受众的ID。 |
| <ul><li>`exportId1`</li></ul> | [受众导出](../../segmentation/api/export-jobs.md#retrieve-list)作业的响应中返回的ID。 有关如何查找此ID的说明，请参阅[步骤4：获取最新的受众导出作业ID](#segment-export-id)。 |

{style="table-layout:auto"}

### 响应 {#response}

成功的响应返回HTTP状态200。

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `segment` | 已激活受众的ID。 |
| `order` | 受众激活到的目标的ID。 |
| `statusURL` | 激活流的状态URL。 您可以使用[流服务API](../../sources/tutorials/api/monitor.md)跟踪流进度。 |

{style="table-layout:auto"}

## API错误处理 {#api-error-handling}

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../landing/troubleshooting.md#request-header-errors)。

### 特定于ad hoc activation API的API错误代码和消息 {#specific-error-messages}

使用临时激活API时，您可能会遇到特定于此API端点的错误消息。 请查看表格以了解如何在它们出现时解决它们。

| 错误消息 | 解决方法 |
|---------|----------|
| 已为运行ID为`segment ID`的订单`dataflow ID`运行受众`flow run ID` | 此错误消息表示受众当前正在进行临时激活流程。 等待作业完成，然后再触发激活作业。 |
| 区段`<segment name>`不是此数据流的一部分或超出计划范围！ | 此错误消息表示您选择要激活的受众未映射到数据流，或者为受众设置的激活计划已过期或尚未开始。 检查受众是否确实映射到数据流，并验证受众激活计划是否与当前日期重叠。 |

## 相关信息 {#related-information}

* [使用流服务API连接到批处理目标并激活数据](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta)使用Experience Platform UI按需将文件导出到批处理目标](/help/destinations/ui/export-file-now.md)