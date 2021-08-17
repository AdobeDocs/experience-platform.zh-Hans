---
keywords: Amazon Kinesis;Kinesis目标；Kinesis
title: Amazon Kinesis连接
description: 创建到Amazon Kinesis存储的实时出站连接，以从Adobe Experience Platform流式传输数据。
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# （测试版）[!DNL Amazon Kinesis]连接

## 概述 {#overview}

>[!IMPORTANT]
>
>平台中的[!DNL Amazon Kinesis]目标当前处于测试阶段。 文档和功能可能会发生变化。

通过[!DNL Amazon Web Services]提供的[!DNL Kinesis Data Streams]服务，您可以实时收集和处理大量数据记录流。

您可以创建到[!DNL Amazon Kinesis]存储的实时出站连接，以从Adobe Experience Platform流式传输数据。

* 有关[!DNL Amazon Kinesis]的更多信息，请参阅[Amazon文档](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 要以编程方式连接到[!DNL Amazon Kinesis]，请参阅[流目标API教程](../../api/streaming-destinations.md)。
* 要使用Platform用户界面连接到[!DNL Amazon Kinesis]，请参阅以下部分。

![Amazon Kinesis在UI中](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 用例 {#use-cases}

通过使用[!DNL Amazon Kinesis]等流目标，您可以轻松地将高价值分段事件和关联的配置文件属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转化”区段的条件。 通过将潜在客户所在的区段映射到[!DNL Amazon Kinesis]目标，您将在[!DNL Amazon Kinesis]中收到此事件。 在这里，您可以采用DIY（自己动手）方法，并在活动之上描述业务逻辑，因为您认为最适合企业IT系统。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## 所需的[!DNL Amazon Kinesis]权限 {#required-kinesis-permission}

要成功连接数据并将数据导出到[!DNL Amazon Kinesis]流，Experience Platform需要拥有以下操作的权限：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

这些权限通过[!DNL Kinesis]控制台进行排列，在Platform用户界面中配置Kinesis目标后，Platform会检查这些权限。

以下示例显示成功将数据导出到[!DNL Kinesis]目标所需的最低访问权限。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `kinesis:ListStreams` | 列出Amazon Kinesis数据流的操作。 |
| `kinesis:PutRecord` | 将单个数据记录写入Kinesis数据流的操作。 |
| `kinesis:PutRecords` | 在单次调用中将多个数据记录写入Kinesis数据流的操作。 |

有关控制[!DNL Kinesis]数据流访问的更多信息，请阅读以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!DNL Amazon Web Services]访问密钥和密钥**:在中 [!DNL Amazon Web Services]，生成一 `access key - secret access key` 对以授予Platform对您帐户的访 [!DNL Amazon Kinesis] 问权限。请参阅[Amazon Web服务文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)，以了解更多信息。
* **区域**:指示要 [!DNL Amazon Web Services] 将数据流到的区域。
* **名称**:提供连接的名称  [!DNL Amazon Kinesis]
* **描述**:提供与的连接描 [!DNL Amazon Kinesis]述。
* **流**:提供帐户中现有数据流的名 [!DNL Amazon Kinesis] 称。平台会将数据导出到此流。

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 将区段激活到此目标 {#activate}

有关将受众区段激活到目标的说明，请参阅[将配置文件和区段激活到目标](../../ui/activate-destinations.md)。

## 导出的数据 {#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式登陆[!DNL Amazon Kinesis]。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为ECID和电子邮件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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



>[!MORELIKETHIS]
>
>* [连接到Amazon Kinesis并使用流量服务API激活数据](../../api/streaming-destinations.md)
* [Azure事件中心目标](./azure-event-hubs.md)
* [目标类型和类别](../../destination-types.md)

