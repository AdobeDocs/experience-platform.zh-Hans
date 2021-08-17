---
keywords: Azure事件中心目标；Azure事件中心；Azure事件Hub
title: （测试版）！DNL Azure Event Hubs]连接
description: 创建到！DNL Azure Event Hubs]存储的实时出站连接，以从Experience Platform流数据。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# （测试版）[!DNL Azure Event Hubs]连接

## 概述 {#overview}

>[!IMPORTANT]
>
>平台中的[!DNL Azure Event Hubs]目标当前处于测试阶段。 文档和功能可能会发生变化。

[!DNL Azure Event Hubs] 是一种大数据流平台和事件摄取服务。它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供程序或批量处理/存储适配器，可以转换和存储发送到事件中心的数据。

您可以创建到[!DNL Azure Event Hubs]存储的实时出站连接，以从Adobe Experience Platform流式传输数据。

* 有关[!DNL Azure Event Hubs]的更多信息，请参阅[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 要以编程方式连接到[!DNL Azure Event Hubs]，请参阅[流目标API教程](../../api/streaming-destinations.md)。
* 要使用Platform用户界面连接到[!DNL Azure Event Hubs]，请参阅以下部分。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 用例 {#use-cases}

通过使用[!DNL Azure Event Hubs]等流目标，您可以轻松地将高价值分段事件和关联的配置文件属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转化”区段的条件。 通过将潜在客户所在的区段映射到[!DNL Azure Event Hubs]目标，您将在[!DNL Azure Event Hubs]中收到此事件。 在这里，您可以采用DIY（自己动手）方法，并在活动之上描述业务逻辑，因为您认为最适合企业IT系统。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从受众激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-streaming-profile-destinations.md#select-attributes)。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL SAS密钥]** 名称 **[!UICONTROL 和SAS密钥]**:填写SAS密钥名称和密钥。了解在[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS密钥对[!DNL Azure Event Hubs]进行身份验证的信息。
* **[!UICONTROL 命名空间]**:填写命名 [!DNL Azure Event Hubs] 空间。了解[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)中的[!DNL Azure Event Hubs]命名空间。
* **[!UICONTROL 名称]**:填写与的连接名 [!DNL Azure Event Hubs]称。
* **[!UICONTROL 描述]**:提供连接的描述。示例：“高级顾客”、“男性对冲浪感兴趣”。
* **[!UICONTROL eventHubName]**:为到您目标的流提供名 [!DNL Azure Event Hubs] 称。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md)。

## 导出的数据 {#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式登陆[!DNL Azure Event Hubs]。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为ECID和电子邮件。

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
>* [连接到Azure事件中心并使用流服务API激活数据](../../api/streaming-destinations.md)
* [AWS Kinesis目标](./amazon-kinesis.md)
* [目标类型和类别](../../destination-types.md)

