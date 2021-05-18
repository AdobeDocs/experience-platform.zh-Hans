---
keywords: Amazon Kinesis;kinesis目标；kinesis
title: Amazon Kinesis连接
description: 创建到Amazon Kinesis存储的实时出站连接以从Adobe Experience Platform流化数据。
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 7f15da092928ed09f898c9197c4679e834b11779
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# （测试版）[!DNL Amazon Kinesis]连接

## 概述 {#overview}

>[!IMPORTANT]
>
>平台中的[!DNL Amazon Kinesis]目标当前处于测试阶段。 文档和功能可能会发生变化。

[!DNL Amazon Web Services]提供的[!DNL Kinesis Data Streams]服务允许您实时收集和处理大型数据记录流。

您可以创建到[!DNL Amazon Kinesis]存储的实时出站连接以从Adobe Experience Platform流化数据。

* 有关[!DNL Amazon Kinesis]的详细信息，请参阅[Amazon文档](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 要以编程方式连接到[!DNL Amazon Kinesis]，请参阅[流目标API教程](../../api/streaming-destinations.md)。
* 要使用平台用户界面连接到[!DNL Amazon Kinesis]，请参阅以下部分。

![Amazon Kinesis在UI中](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 用例 {#use-cases}

通过使用流目标（如[!DNL Amazon Kinesis]），您可以轻松将高价值细分事件和关联的用户档案属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转换”区段的条件。 通过将潜在客户所属的区段映射到[!DNL Amazon Kinesis]目标，您将在[!DNL Amazon Kinesis]中收到此事件。 在这里，您可以采用自己动手的方法，在事件上描述业务逻辑，因为您认为最适合您的企业IT系统。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## 连接目标{#connect-destination}

有关如何连接到您的云存储目标（包括[!DNL Amazon]支持的目标）的说明，请参阅[云存储目标工作流](./workflow.md)。

对于[!DNL Amazon Kinesis]目标，在创建目标工作流中输入以下信息：

## 帐户步骤{#account-step}

* **[!DNL Amazon Web Services]访问密钥和密钥**:在中 [!DNL Amazon Web Services]，生成一 `access key - secret access key` 对以授予对您帐户的平台 [!DNL Amazon Kinesis] 访问权。请阅读[Amazon Web服务文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)了解更多信息。
* **区域**:指示要 [!DNL Amazon Web Services] 将数据流化到的区域。

![帐户步骤中的输入字段](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

## 身份验证步骤{#authentication-step}

* **名称**:提供连接的名称  [!DNL Amazon Kinesis]
* **描述**:提供与的连接说明 [!DNL Amazon Kinesis]。
* **stream**:提供帐户中现有数据流的名 [!DNL Amazon Kinesis] 称。平台会将数据导出到此流。
* **[!UICONTROL 营销操作]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![身份验证步骤中的输入字段](../../assets/catalog/cloud-storage/amazon-kinesis/authentication.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 导出的数据{#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式进入[!DNL Amazon Kinesis]。 例如，以下事件包含符合特定区段条件并退出另一区段的受众的电子邮件地址用户档案属性。 此潜在客户的身份为ECID和电子邮件。

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
>* [连接到Amazon Kinesis并使用Flow Service API激活数据](../../api/streaming-destinations.md)
* [Azure事件集线器目标](./azure-event-hubs.md)
* [目标类型和类别](../../destination-types.md)

