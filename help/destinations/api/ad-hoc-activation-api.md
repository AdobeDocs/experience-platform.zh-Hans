---
keywords: Experience Platform；目标API；临时激活；激活区段临时
solution: Experience Platform
title: （测试版）通过临时激活API将受众区段激活到批量目标
description: This article illustrates the end-to-end workflow for activating audience segments via the ad-hoc activation API, including the segmentation jobs that take place before activation.
topic-legacy: tutorial
type: Tutorial
source-git-commit: 749fa5dc1e8291382408d9b1a0391c4c7f2b2a46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 2%

---


# （测试版）通过临时激活API将受众区段激活到批量目标

>[!IMPORTANT]
>
>的 [!DNL ad-hoc activation API] 平台中的当前为测试版。 文档和功能可能会发生变化。

## 概述 {#overview}

临时激活API允许营销人员以编程方式快速高效地将受众区段激活到目标，以应对需要立即激活的情况。

The diagram below illustrates the end-to-end workflow for activating segments via the ad-hoc activation API, including the segmentation jobs that take place in Platform every 24 hours.

![临时激活](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Ad-hoc audience激活仅受 [批量基于文件的目标](../destination-types.md#file-based).

## 用例 {#use-cases}

### Flash销售或促销

An online retailer is preparing a limited flash sale and wants to notify customers on a short notice. 通过Experience Platform临时激活API，营销团队可以按需导出区段，并快速向客户群发送促销电子邮件。


### 最新事件或突发新闻

A hotel expects inclement weather over the following days, and the team wants to inform the arriving guests quickly, so they can plan accordingly. The marketing team can use the Experience Platform ad-hoc activation API to export segments on-demand, and notify the guests.

### 集成测试

IT经理可以使用Experience Platform临时激活API按需导出区段，因此他们可以测试与Adobe Experience Platform的自定义集成，并确保一切正常工作。


## Guardrails {#guardrails}

使用临时激活API时，请记住以下护栏。

* 目前，每个临时激活作业最多可激活20个区段。 尝试激活每个作业20个以上的区段将导致作业失败。 此行为可能会在未来版本中发生更改。
* Ad-hoc activation jobs cannot run in parallel with scheduled [segment export jobs](../../segmentation/api/export-jobs.md). 在运行临时激活作业之前，请确保计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 例如，如果激活数据流显示 **[!UICONTROL 处理]** 状态，请等待其完成后再运行临时激活作业。
* 每个区段不要运行多个并发的临时激活作业。

## 分段注意事项 {#segmentation-considerations}

Adobe Experience Platform每24小时运行一次计划分段作业。 临时激活API根据最新的分段结果运行。

## 步骤1:先决条件 {#prerequisites}

在调用Adobe Experience Platform API之前，请确保满足以下先决条件：

* You have an IMS Organization account with access to Adobe Experience Platform.
* Your Experience Platform account has the `developer` and `user` roles enabled for the Adobe Experience Platform API product profile. 联系您的 [Admin Console](../../access-control/home.md) 管理员为您的帐户启用这些角色。
* 你有Adobe ID。 如果您没有Adobe ID，请转到 [Adobe开发人员控制台](https://developer.adobe.com/console) 并创建一个新帐户。

## Step 2: Gather credentials {#credentials}

要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的资源可以与特定虚拟沙箱隔离。 在对Platform API的请求中，您可以指定操作将在其中进行的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

All requests that contain a payload (POST, PUT, PATCH) require an additional media type header:

* Content-Type: `application/json`

## 步骤3:在平台UI中创建激活流程 {#activation-flow}

Before you can activate segments through the ad-hoc activation API, you must first have an activation flow configured in the Platform UI, for the chosen destination.

This includes going into the activation workflow, selecting your segments, configuring a schedule, and activating them.

有关如何为批处理目标配置激活流程的详细说明，请参阅以下教程： [激活受众数据以批量配置文件导出目标](../ui/activate-batch-profile-destinations.md).

## 步骤4:获取最新的区段导出作业ID {#segment-export-id}

在为批处理目标配置激活流程后，每24小时自动开始运行一次计划分段作业。

Before you can run the ad-hoc activation job, you must obtain the ID of the latest segment export job. 您必须在临时激活作业请求中传递此ID。

按照描述的说明操作 [此处](../../segmentation/api/export-jobs.md#retrieve-list) 以检索所有区段导出作业的列表。

在响应中，查找包含以下架构属性的第一个记录。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

区段导出作业ID位于 `id` 属性，如下所示。

![segment export job ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步骤5:运行临时激活作业 {#activation-job}

Adobe Experience Platform每24小时运行一次计划分段作业。 临时激活API根据最新的分段结果运行。

在运行临时激活作业之前，请确保区段的计划区段导出作业已完成。 请参阅 [目标数据流监控](../../dataflows/ui/monitor-destinations.md) 有关如何监控激活流状态的信息。 For example, if your activation dataflow shows a **[!UICONTROL Processing]** status, wait for it to finish before running the ad-hoc activation job.

区段导出作业完成后，您可以触发激活。

>[!NOTE]
>
>目前，每个临时激活作业最多可激活20个区段。 尝试激活每个作业20个以上的区段将导致作业失败。 此行为可能会在未来版本中发生更改。

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
   "exportIds":[
      "exportId1"
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 要激活区段的目标实例的ID。 |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | The IDs of the segments that you want to activate to the selected destination. |
| <ul><li>`exportId1`</li></ul> | 在响应 [区段导出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 请参阅 [步骤4:获取最新的区段导出作业ID](#segment-export-id) 以了解有关如何查找此ID的说明。 |

### 响应

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
| `segment` | The ID of the activated segment. |
| `order` | 区段被激活到的目标的ID。 |
| `statusURL` | 激活流程的状态URL。 您可以使用 [流量服务API](../../sources/tutorials/api/monitor.md). |


## API错误处理

目标SDK API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 和 [请求标头错误](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) 平台疑难解答指南中。
