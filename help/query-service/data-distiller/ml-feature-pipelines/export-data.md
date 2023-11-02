---
title: 将数据导出到外部ML环境
description: 了解如何将使用Data Distiller创建的准备好的训练数据集共享到ML环境可读取的云存储位置，以便对模型进行训练和评分。
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# 将数据导出到外部ML环境

本文档演示如何将使用Data Distiller创建的准备好的训练数据集共享到ML环境可读取的云存储位置，以便训练和评分模型。 此示例将训练数据集导出到 [数据登陆区(DLZ)](../../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). 您可以根据需要更改存储目标，以便与机器学习环境配合使用。

此 [目标的流服务](https://developer.adobe.com/experience-platform-apis/references/destinations/) 用于通过将计算功能的数据集登陆到适当的云存储位置来完成功能管道。

## 创建源连接 {#create-source-connection}

源连接负责配置与您的Adobe Experience Platform数据集的连接，以便生成的流确切知道应在何处查找数据以及采用何种格式。

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## 创建目标连接 {#create-target-connection}

目标连接负责连接到目标文件系统。 这需要先创建与云存储帐户（本示例中的数据登陆区）的基本连接，然后使用指定的压缩和格式选项创建与特定文件路径的目标连接。

可用的云存储目标分别由连接规范ID标识：

| 云存储类型 | 连接规范ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Azure Blob 存储 | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure数据湖 | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| 数据登陆区 | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google云存储 | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## 创建数据流 {#create-data-flow}

最后一步是在源连接中指定的数据集和目标连接中指定的目标文件路径之间创建数据流。

每个可用的云存储类型都由一个流量规范ID标识：

| 云存储类型 | 流量规范ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Azure Blob 存储 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure数据湖 | 17be2013-2549-41ce-96e7-a70363bec293 |
| 数据登陆区 | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google云存储 | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

以下代码创建一个数据流，其中计划设置为在未来的很长时间开始。 这允许您在模型开发期间触发临时流。 获得经过训练的模型后，您可以更新数据流的计划，以按所需的计划共享功能数据集。

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

创建数据流后，您现在可以触发临时流运行以按需共享功能数据集：

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## 简化共享到数据登陆区

要更轻松地将数据集共享到数据登陆区，请 `aepp` 库提供 `exportDatasetToDataLandingZone` 在单个函数调用中执行上述步骤的函数：

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

此代码基于提供的参数创建源连接、目标连接和数据流，并在单个步骤中执行数据流的随机运行。
