---
keywords: Experience Platform；目标API；临时激活；激活区段临时
solution: Experience Platform
title: 通过临时激活API将受众区段激活到批量目标
description: 本文说明了通过临时激活API激活受众区段的端到端工作流程，包括激活前进行的分段作业。
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 8d67d89db6a8c179935b4fe709f91279860d464e
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 2%

---

# 通过临时激活API，按需将受众区段激活到批量目标

>[!IMPORTANT]
>
>完成测试阶段后， [!DNL ad-hoc activation API] 现在，所有Experience Platform客户均可使用(GA)。 在GA版本中，API已升级到版本2。 步骤4([获取最新的区段导出作业ID](#segment-export-id))，因为API不再需要导出ID。
>
>请参阅 [运行临时激活作业](#activation-job) 有关更多信息，请参阅本教程的下文。

## 概述 {#overview}

临时激活API允许营销人员以编程方式快速高效地将受众区段激活到目标，以应对需要立即激活的情况。

下图说明了通过临时激活API激活区段的端到端工作流程，包括每24小时在Platform中发生一次的分段作业。

![临时激活](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Ad-hoc audience激活仅受 [批量基于文件的目标](../destination-types.md#file-based).

## 用例 {#use-cases}

### Flash销售或促销

一家在线零售商准备进行有限的闪购，希望在短时间通知客户。 通过Experience Platform临时激活API，营销团队可以按需导出区段，并快速向客户群发送促销电子邮件。

### 最新事件或突发新闻

酒店预计接下来几天天气会很恶劣，团队想要迅速通知到达的客人，以便他们可以据此进行规划。 营销团队可以使用Experience Platform临时激活API根据需要导出区段，并通知客人。

### 集成测试

IT经理可以使用Experience Platform临时激活API按需导出区段，因此他们可以测试与Adobe Experience Platform的自定义集成，并确保一切正常工作。

## 护栏 {#guardrails}

使用临时激活API时，请记住以下护栏。

* 目前，每个临时激活作业最多可激活80个区段。 尝试激活每个作业80个以上的区段将导致作业失败。 此行为可能会在未来版本中发生更改。
* 临时激活作业不能与计划的同时运行 [区段导出作业](../../segmentation/api/export-jobs.md). 在运行临时激活作业之前，请确保计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 例如，如果激活数据流显示 **[!UICONTROL 处理]** 状态，请等待其完成后再运行临时激活作业。
* 每个区段不要运行多个并发的临时激活作业。

## 分段注意事项 {#segmentation-considerations}

Adobe Experience Platform每24小时运行一次计划分段作业。 临时激活API根据最新的分段结果运行。

## 步骤1:先决条件 {#prerequisites}

在调用Adobe Experience Platform API之前，请确保满足以下先决条件：

* 您拥有有权访问Adobe Experience Platform的IMS组织帐户。
* 您的Experience Platform帐户具有 `developer` 和 `user` 为Adobe Experience Platform API产品配置文件启用了角色。 联系您的 [Admin Console](../../access-control/home.md) 管理员为您的帐户启用这些角色。
* 你有Adobe ID。 如果您没有Adobe ID，请转到 [Adobe Developer控制台](https://developer.adobe.com/console) 并创建一个新帐户。

## 步骤2:收集凭据 {#credentials}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的资源可以与特定虚拟沙箱隔离。 在对Platform API的请求中，您可以指定操作将在其中进行的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 步骤3:在平台UI中创建激活流程 {#activation-flow}

您必须先在平台UI中为所选目标配置激活流程，然后才能通过临时激活API激活区段。

这包括转到激活工作流、选择您的区段、配置计划并激活它们。 您可以使用UI或API创建激活流程：

* [使用Platform UI创建激活流程以批量配置文件导出目标](../ui/activate-batch-profile-destinations.md)
* [使用流量服务API连接到批量配置文件导出目标并激活数据](../api/connect-activate-batch-destinations.md)

## 步骤4:获取最新的区段导出作业ID（v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在临时激活API的v2中，您无需获取最新的区段导出作业ID。 您可以跳过此步骤并继续执行下一步。

在为批处理目标配置激活流程后，每24小时自动开始运行一次计划分段作业。

在运行临时激活作业之前，必须获取最新区段导出作业的ID。 您必须在临时激活作业请求中传递此ID。

按照描述的说明操作 [此处](../../segmentation/api/export-jobs.md#retrieve-list) 以检索所有区段导出作业的列表。

在响应中，查找包含以下架构属性的第一个记录。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

区段导出作业ID位于 `id` 属性，如下所示。

![区段导出作业ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步骤5:运行临时激活作业 {#activation-job}

Adobe Experience Platform每24小时运行一次计划分段作业。 临时激活API根据最新的分段结果运行。

>[!IMPORTANT]
>
>请注意以下一次性约束：在运行临时激活作业之前，请确保从根据您在 [步骤3 — 在Platform UI中创建激活流程](#activation-flow).

在运行临时激活作业之前，请确保区段的计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 例如，如果激活数据流显示 **[!UICONTROL 处理]** 状态，请等待其完成后再运行临时激活作业。

区段导出作业完成后，您可以触发激活。

>[!NOTE]
>
>目前，每个临时激活作业最多可激活80个区段。 尝试激活每个作业80个以上的区段将导致作业失败。 此行为可能会在未来版本中发生更改。

### 请求 {#request}

>[!IMPORTANT]
>
>必须将 `Accept: application/vnd.adobe.adhoc.activation+json; version=2` 标头，以便使用ad-hoc激活API的v2。

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活区段的目标实例的ID。 您可以通过导航到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** ，然后单击所需的目标行以显示右边栏中的目标ID。 有关更多信息，请阅读 [目标工作区文档](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到选定目标的区段的ID。 |

{style=&quot;table-layout:auto&quot;}

### 具有导出ID的请求（将弃用） {#request-deprecated}

>[!IMPORTANT]
>
>**已弃用的请求类型**. 此示例类型描述API版本1的请求类型。 在临时激活API的v2中，您不需要包含最新的区段导出作业ID。

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活区段的目标实例的ID。 您可以通过导航到 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** ，然后单击所需的目标行以显示右边栏中的目标ID。 有关更多信息，请阅读 [目标工作区文档](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到选定目标的区段的ID。 |
| <ul><li>`exportId1`</li></ul> | 在响应 [区段导出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 请参阅 [步骤4:获取最新的区段导出作业ID](#segment-export-id) 以了解有关如何查找此ID的说明。 |

{style=&quot;table-layout:auto&quot;}

### 响应 {#response}

成功响应会返回HTTP状态200。

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
| `segment` | 已激活区段的ID。 |
| `order` | 区段被激活到的目标的ID。 |
| `statusURL` | 激活流程的状态URL。 您可以使用 [流量服务API](../../sources/tutorials/api/monitor.md). |

{style=&quot;table-layout:auto&quot;}

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

### 特定于临时激活API的API错误代码和消息 {#specific-error-messages}

使用临时激活API时，您可能会遇到特定于此API端点的错误消息。 查看表格，了解在表格显示时如何解决这些问题。

| 错误消息 | 分辨率 |
|---------|----------|
| 已针对区段运行 `segment ID` 订购 `dataflow ID` 使用运行id `flow run ID` | 此错误消息表示当前正在为区段进行临时激活流程。 等待作业完成，然后再次触发激活作业。 |
| 区段 `<segment name>` 不是此数据流的一部分或超出计划范围！ | 此错误消息表示您选择激活的区段未映射到数据流，或者为区段设置的激活计划已过期或尚未启动。 检查区段是否确实映射到数据流，并验证区段激活计划是否与当前日期重叠。 |

## 相关信息 {#related-information}

* [连接到批处理目标，并使用流量服务API激活数据](/help/destinations/api/connect-activate-batch-destinations.md)