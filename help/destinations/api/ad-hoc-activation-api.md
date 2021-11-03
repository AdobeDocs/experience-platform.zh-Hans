---
keywords: Experience Platform；目标API；临时激活；激活区段临时
solution: Experience Platform
title: （测试版）通过Experience Platform临时激活API激活受众区段
description: 本文说明了通过临时激活API激活区段的端到端工作流，包括激活之前进行的分段作业。
topic-legacy: tutorial
type: Tutorial
source-git-commit: 0c8fbaec9a592c9d5c20c077f31279f732ec2a0d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 2%

---


# （测试版）通过Experience Platform临时激活API激活受众区段

>[!IMPORTANT]
>
>的 [!DNL ad-hoc activation API] 平台中的当前为测试版。 文档和功能可能会发生变化。

## 概述 {#overview}

临时激活API允许营销人员以编程方式快速高效地将受众区段激活到目标，以应对需要立即激活的情况。

下图说明了通过临时激活API激活区段的端到端工作流程，包括每24小时在Platform中发生一次的分段作业。

![临时激活](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Ad-hoc audience激活仅受 [批量基于文件的目标](../destination-types.md#file-based).

## 用例 {#use-cases}

### Flash销售或促销

一家在线零售商准备进行有限的闪购，希望在短时间通知客户。 通过Experience Platform临时激活API，营销团队可以根据需要导出受众区段，并快速向客户群发送促销电子邮件。


### 最新事件或突发新闻

酒店预计接下来几天天气会很恶劣，团队想要迅速通知到达的客人，以便他们可以据此进行规划。 营销团队可以使用Experience Platform临时激活API根据需要导出受众区段，并通知客人。

### 集成测试

IT经理可以使用Experience Platform临时激活API按需导出受众区段，因此他们可以测试与Adobe Experience Platform的自定义集成，并确保一切正常工作。


## 护栏 {#guardrails}

使用临时激活API时，请记住以下护栏。

* 每个临时激活作业最多可激活20个区段。 尝试激活每个作业20个以上的区段将导致作业失败。
* 临时激活作业不能与计划的同时运行 [区段导出作业](../../segmentation/api/export-jobs.md). 在运行临时激活作业之前，请确保计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 例如，如果激活数据流显示 **[!UICONTROL 处理]** 状态，请等待其完成后再运行临时激活作业。
* 每个区段不要运行多个并发的临时激活作业。

## 分段注意事项 {#segmentation-considerations}

Adobe Experience Platform每24小时运行一次计划分段作业。 临时激活API根据最新的分段结果运行。

## 步骤1:先决条件 {#prerequisites}

在调用Adobe Experience Platform API之前，请确保满足以下先决条件：

* 您拥有有权访问Adobe Experience Platform的IMS组织帐户。
* 您的Experience Platform帐户具有 `developer` 和 `user` 为Adobe Experience Platform API产品配置文件启用了角色。 联系您的 [Admin Console](../../access-control/home.md) 管理员为您的帐户启用这些角色。
* 你有Adobe ID。 如果您没有Adobe ID，请转到 [Adobe开发人员控制台](https://developer.adobe.com/console) 并创建一个新帐户。

## 步骤2:收集凭据 {#credentials}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的资源可以与特定虚拟沙箱隔离。 在对Platform API的请求中，您可以指定操作将在其中进行的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 步骤3:在平台UI中创建激活流程 {#activation-flow}

您必须先在平台UI中为所选目标配置激活流程，然后才能通过临时激活API激活区段。

这包括转到激活工作流、选择您的区段、配置计划并激活它们。

有关如何为批处理目标配置激活流程的详细说明，请参阅以下教程： [激活受众数据以批量配置文件导出目标](../ui/activate-batch-profile-destinations.md).

## 步骤4:获取最新的区段导出作业ID {#segment-export-id}

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

在运行临时激活作业之前，请确保区段的计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 例如，如果激活数据流显示 **[!UICONTROL 处理]** 状态，请等待其完成后再运行临时激活作业。

区段导出作业完成后，您可以触发激活。

>[!NOTE]
>
>每个临时激活作业最多可激活20个区段。 尝试激活更多区段将导致作业失败。

### 请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "exportId":[
      "exportId1"
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活受众区段的目标实例的ID。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 要激活到选定目标的受众区段的ID。 |
| <ul><li>`exportId1`</li></ul> | 在响应 [区段导出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 请参阅 [步骤4:获取最新的区段导出作业ID](#segment-export-id) 以了解有关如何查找此ID的说明。 |

### 响应

成功响应会返回HTTP状态200。

```shell
{
   "code":"DEST-ADH-200",
   "message":"Adhoc run triggered successfully",
   "statusURLs":[
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-1",
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-2"
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `code` | API响应代码。 成功的调用会返回 `DEST-ADH-200` （状态代码200），当格式不正确时返回 `DEST-ADH-400` （状态代码400）。 |
| `message` | API返回的成功或错误消息。 |
| `statusURLs` | 激活流程的状态URL。 您可以使用 [流量服务API](../../sources/tutorials/api/monitor.md). |


## API错误处理

目标SDK API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 和 [请求标头错误](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) 平台疑难解答指南中。
