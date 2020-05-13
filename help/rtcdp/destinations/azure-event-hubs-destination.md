---
title: （测试版）Azure事件集线器目标
seo-title: （测试版）Azure事件集线器目标
description: 创建到Azure事件中心存储的实时出站连接，以从Experience Platform流化数据。
seo-description: 创建到Azure事件中心存储的实时出站连接，以从Experience Platform流化数据。
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

---


# （测试版）Azure事件集线器目标

>[!IMPORTANT]
>
>Adobe [!DNL Azure Event Hubs] Real-time CDP中的目标当前为测试版。 文档和功能可能会发生变化。

## 概述 {#overview}

[!DNL Azure Event Hubs] 是大数据流平台和事件摄取服务。 它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供者或批处理/事件适配器，可以转换和存储发送到存储中心的数据。

您可以创建到存储的实时出站连接， [!DNL Azure Event Hubs] 以便从Adobe Experience Platform流化数据。

* 有关详细信息， [!DNL Azure Event Hubs]请参阅Microsoft [文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 要使用API调 [!DNL Azure Event Hubs] 用连接到，请参阅流 [目标API教程](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)。
* 要使用Adobe [!DNL Azure Event Hubs] 实时CDP用户界面连接到，请参阅以下各节。

![AWS Kinesis在UI中](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## 用例 {#use-cases}

通过使用Azure事件中心等流目标，您可以轻松地将高价值细分事件和相关用户档案属性馈送到您选择的系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转换”区段的条件。 通过将潜在客户所属的区段映射到Azure事件集线器目标，您将在Azure事件集线器中收到此事件。 在这里，您可以采用自行操作的方法，在事件上描述业务逻辑，就像您认为最适合企业IT系统一样。

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标（包括）的说明，请参阅云存储目标工作 [!DNL Azure Event Hubs]流。

对于 [!DNL Azure Event Hubs] 目标，在创建目标工作流中输入以下信息：

### 在帐户步骤中 {#account-step}

* **[!UICONTROL SAS密钥名]** 和 **[!UICONTROL SAS密钥]**: 填写您的SAS密钥名称和密钥。 了解Microsoft文档 [!DNL Azure Event Hubs] 中有关使用SAS密钥进 [行身份验证](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空间]**: 填写您的 [!DNL Azure Event Hubs] 命名空间。 了解Microsoft [!DNL Azure Event Hubs] 文档中 [的命名空间](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。

![身份验证步骤中所需的输入](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### 在身份验证步骤中 {#authentication-step}

* **[!UICONTROL 名称]**: 填写连接的名称 [!DNL Azure Event Hubs]。
* **[!UICONTROL 描述]**: 提供连接描述。  示例： “高级客户”、“男性对风筝冲浪感兴趣”。
* **[!UICONTROL eventHubName]**: 为流提供到目标的名 [!DNL Azure Event Hubs] 称。

![设置步骤中需要的数据](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。


## 导出的数据 {#exported-data}

导出的Experience Platform数据以JSON [!DNL Azure Event Hubs] 格式登录。 例如，包含已退出特定区段的事件的哈希电子邮件标识的受众流可能如下所示：

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* [连接到Azure事件中心，并使用API调用激活数据](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS Kinesis目标](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [目标类型和类别](/help/rtcdp/destinations/destination-types.md)