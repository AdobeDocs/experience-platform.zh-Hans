---
keywords: Azure事件中心目标；Azure事件中心；Azure事件Hub
title: （测试版） [!DNL Azure Event Hubs] 连接
description: 创建与的实时出站连接 [!DNL Azure Event Hubs] 存储以从Experience Platform流数据。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: b0c2c8313e05d1316f23dc15d99893e1887f8dcf
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# （测试版） [!DNL Azure Event Hubs] 连接

## 概述 {#overview}

>[!IMPORTANT]
>
>的 [!DNL Azure Event Hubs] 平台中的目标当前为测试版。 文档和功能可能会发生变化。

[!DNL Azure Event Hubs] 是一种大数据流平台和事件摄取服务。 它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供程序或批量处理/存储适配器，可以转换和存储发送到事件中心的数据。

您可以创建与的实时出站连接 [!DNL Azure Event Hubs] 存储以从Adobe Experience Platform流数据。

* 有关 [!DNL Azure Event Hubs]，请参阅 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 连接到 [!DNL Azure Event Hubs] 以编程方式，请参阅 [流目标API教程](../../api/streaming-destinations.md).
* 连接到 [!DNL Azure Event Hubs] 使用Platform用户界面，请参阅以下部分。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 用例 {#use-cases}

通过使用流目标，例如 [!DNL Azure Event Hubs]，则您可以轻松地将高价值分段事件和关联的配置文件属性馈送到所选系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转化”区段的条件。 通过映射潜在客户所在的区段 [!DNL Azure Event Hubs] 目标，您将在 [!DNL Azure Event Hubs]. 在这里，您可以采用DIY（自己动手）方法，并在活动之上描述业务逻辑，因为您认为最适合企业IT系统。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从 [受众激活工作流](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL SAS密钥名称]** 和 **[!UICONTROL SAS密钥]**:填写SAS密钥名称和密钥。 了解如何验证 [!DNL Azure Event Hubs] 在 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空间]**:填写 [!DNL Azure Event Hubs] 命名空间。 了解 [!DNL Azure Event Hubs] 命名空间 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 名称]**:填写连接的名称 [!DNL Azure Event Hubs].
* **[!UICONTROL 描述]**:提供连接的描述。  示例：“高级顾客”、“男性对冲浪感兴趣”。
* **[!UICONTROL eventHubName]**:为您的 [!DNL Azure Event Hubs] 目标。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## 配置文件导出行为 {#profile-export-behavior}

Experience Platform会优化配置文件导出行为，以将数据导出到您的Azure事件中心目标，以便在区段鉴别或其他重要事件之后对配置文件进行相关更新时，才会将数据导出到您的目标。 在以下情况下，用户档案会导出到您的目标：

* 配置文件更新是由至少一个映射到目标的区段的区段成员资格发生更改而触发的。 例如，配置文件已符合映射到目标的其中一个区段的条件，或者已退出映射到目标的其中一个区段。
* 配置文件更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合映射到目标的某个区段资格条件的用户档案，已在身份映射属性中添加了新身份。
* 配置文件更新是由至少一个映射到目标的属性的属性发生更改而触发的。 例如，映射步骤中映射到目标的某个属性会添加到配置文件中。

在上述所有情况下，只会将发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段有一百个成员，并且有五个新的配置文件符合该区段的资格条件，则导出到目标的过程将是递增的，并且仅包含五个新配置文件。

请注意，无论更改位于何处，都会导出配置文件的所有映射属性。 因此，在上例中，即使属性本身未发生更改，也会导出这五个新配置文件的所有映射属性。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据登陆 [!DNL Azure Event Hubs] 格式。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为ECID和电子邮件。

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
>* [AWS Kinesis目标](./amazon-kinesis.md)
>* [目标类型和类别](../../destination-types.md)

