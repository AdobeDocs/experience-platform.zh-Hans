---
keywords: Azure事件集线器目标；Azure事件集线器；azure eventhub
title: （测试版）Azure事件集线器连接
description: 创建到Azure事件集线器存储的实时出站连接，以流式传输来自Experience Platform的数据。
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 2%

---


# （测试版）[!DNL Azure Event Hubs]连接

>[!IMPORTANT]
>
>平台中的[!DNL Azure Event Hubs]目标当前处于测试阶段。 文档和功能可能会发生变化。

[!DNL Azure Event Hubs] 是大数据流平台和事件摄取服务。它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供者或批处理/存储适配器，可以转换和存储发送到事件中心的数据。

您可以创建到[!DNL Azure Event Hubs]存储的实时出站连接以从Adobe Experience Platform流化数据。

* 有关[!DNL Azure Event Hubs]的详细信息，请参阅[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 要以编程方式连接到[!DNL Azure Event Hubs]，请参阅[流目标API教程](../../api/streaming-destinations.md)。
* 要使用平台用户界面连接到[!DNL Azure Event Hubs]，请参阅以下部分。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 用例 {#use-cases}

通过使用流目标（如[!DNL Azure Event Hubs]），您可以轻松将高价值细分事件和关联的用户档案属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转换”区段的条件。 通过将潜在客户所属的区段映射到[!DNL Azure Event Hubs]目标，您将在[!DNL Azure Event Hubs]中收到此事件。 在这里，您可以采用自己动手的方法，在事件上描述业务逻辑，因为您认为最适合您的企业IT系统。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

## 连接目标{#connect-destination}

有关如何连接到您的云存储目标（包括[!DNL Azure Event Hubs]）的说明，请参阅[云存储目标工作流](./workflow.md)。

对于[!DNL Azure Event Hubs]目标，在创建目标工作流中输入以下信息：

## 身份验证步骤{#authentication-step}

* **[!UICONTROL SAS Key Name]** 和 **[!UICONTROL SAS Key]**:填写您的SAS密钥名称和密钥。了解在[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中使用SAS键对[!DNL Azure Event Hubs]进行身份验证。
* **[!UICONTROL Namespace]**:填写您的 [!DNL Azure Event Hubs] 命名空间。了解[Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)中的[!DNL Azure Event Hubs]命名空间。

![身份验证步骤中所需的输入](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

## 设置步骤{#setup-step}

* **[!UICONTROL Name]**:填写连接的名称 [!DNL Azure Event Hubs]。
* **[!UICONTROL Description]**:提供连接描述。示例：“高级顾客”、“男性对风筝冲浪感兴趣”。
* **[!UICONTROL eventHubName]**:为流提供到目标的名 [!DNL Azure Event Hubs] 称。
* **[!UICONTROL Marketing actions]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![设置步骤中所需的数据](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。

## 导出的数据{#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式进入[!DNL Azure Event Hubs]。 例如，以下事件包含符合特定区段条件并退出另一区段的受众的电子邮件地址用户档案属性。 此潜在客户的身份为ECID和电子邮件。

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
>* [连接到Azure事件中心，并使用流服务API激活数据](../../api/streaming-destinations.md)
>* [AWS Kinesis目标](./amazon-kinesis.md)
>* [目标类型和类别](../../destination-types.md)