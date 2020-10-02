---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: AmazonKinesis目的地
seo-title: AmazonKinesis目的地
description: 创建到您的AmazonKinesis存储的实时出站连接以从Adobe Experience Platform流数据。
seo-description: 创建到您的AmazonKinesis存储的实时出站连接以从Adobe Experience Platform流数据。
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---


# （测试版）目 [!DNL Amazon Kinesis] 标


>[!IMPORTANT]
>
>Adobe [!DNL Amazon Kinesis] 实时CDP中的目标当前处于测试阶段。 文档和功能可能会发生变化。

## 概述 {#overview}

通过 [!DNL Kinesis Data Streams] 该服 [!DNL Amazon Web Services] 务，您可以实时收集和处理大量数据记录流。

您可以创建到存储的实时出站连接，以 [!DNL Amazon Kinesis] 便从Adobe Experience Platform流数据。

* 有关详细信息， [!DNL Amazon Kinesis]请参阅 [Amazon文档](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 要使用API调 [!DNL Amazon Kinesis] 用连接到，请参阅流 [目标API教程](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)。
* 要使用Adobe [!DNL Amazon Kinesis] 实时CDP用户界面连接到，请参阅以下各节。

![AmazonKinesis在用户界面](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## 用例 {#use-cases}

通过使用流目标， [!DNL Amazon Kinesis]您可以轻松地将高价值细分事件和相关用户档案属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转换”区段的条件。 通过映射潜在客户所属的区段到目 [!DNL Amazon Kinesis] 标，您将在收到此事件 [!DNL Amazon Kinesis]。 在这里，您可以采用自行操作的方法，在事件上描述业务逻辑，就像您认为最适合企业IT系统一样。

## 导出类型 {#export-type}

**用户档案导出** -您正在导出区段的所有成员以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](/help/rtcdp/destinations/activate-destinations.md#select-attributes)。

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标(包括受支持的云存储目标)的说明，请参阅云目标工作 [!DNL Amazon]流。

对于 [!DNL Amazon Kinesis] 目标，在创建目标工作流中输入以下信息：

### 在身份验证步骤中 {#authentication-step}

* **[!DNL Amazon Web Services]访问密钥和密钥**:在中 [!DNL Amazon Web Services]，生成 `access key - secret access key` 一对，以授予Adobe对帐户的实时CDP访 [!DNL Amazon Kinesis] 问权。 在AmazonWeb服务文 [档中了解更多信息](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **区域**:指示要 [!DNL Amazon Web Services] 将数据流化到的区域。

![帐户步骤中的输入字段](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### 在设置步骤中 {#setup-step}

* **名称**:提供连接的名称 [!DNL Amazon Kinesis]
* **描述**:提供与的连接说明 [!DNL Amazon Kinesis]。
* **stream**:提供帐户中现有数据流的名 [!DNL Amazon Kinesis] 称。 Adobe实时CDP会将数据导出到此流。

![验证步骤中的输入字段](/help/rtcdp/destinations/assets/aws-kinesis-setup-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据以JSON [!DNL Amazon Kinesis] 格式登录。 例如，以下事件包含符合特定区段资格并退出另一区段的受众的电子邮件地址用户档案属性。 此潜在客户的标识为ECID和电子邮件。

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
>* [连接到AmazonKinesis并使用API调用激活数据](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Azure事件集线器目标](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [目标类型和类别](/help/rtcdp/destinations/destination-types.md)

