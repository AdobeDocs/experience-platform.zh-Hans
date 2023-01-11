---
keywords: Experience Platform；主页；热门主题；Azure事件中心；Azure事件中心；事件中心；事件中心
solution: Experience Platform
title: Azure事件集线器源连接器概述
description: 了解如何使用API或用户界面将Azure事件中心连接到Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 连接器

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]和 [!DNL Azure]. 您可以将这些系统中的数据导入平台。

云存储源可以将您自己的数据引入平台，而无需下载、设置或上传。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤都会集成到源工作流中。 平台允许您从 [!DNL Event Hubs] 实时。

## 缩放方式 [!DNL Event Hubs]

您的 [!DNL Event Hubs] 如果需要导入大容量数据、提高并行度或提高摄取平台的速度，则必须增加实例。

### 进入较高卷数据

当前，您可以从 [!DNL Event Hubs] 帐户到Platform的记录为每秒2000条。 要放大并摄取更大量的数据，请联系您的Adobe代表。

### 在 [!DNL Event Hubs] 和平台

并行性是指为了提高速度和性能，在多个处理单元上同时执行相同的任务。 您可以在 [!DNL Event Hubs] 通过增加分区或通过为 [!DNL Event Hubs] 帐户。 请参阅 [[!DNL Event Hubs] 缩放文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 以了解更多信息。

要提高平台端的摄取速度，平台必须增加源连接器中要从 [!DNL Event Hubs] 分区。 在 [!DNL Event Hubs] 另外，请联系您的Adobe代表以根据新分区来扩展平台任务。 当前，此过程未自动完成。

## 使用虚拟网络连接到 [!DNL Event Hubs] 到平台

您可以设置虚拟网络以连接 [!DNL Event Hubs] 启用防火墙措施时发送到平台。 要设置虚拟网络，请转到此 [[!DNL Event Hubs] 网络规则集文档](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 并按照下面列出的步骤操作：

* 选择 **试试** 从REST API面板；
* 验证 [!DNL Azure] 在同一浏览器中使用您的凭据；
* 选择 [!DNL Event Hubs] 命名空间、资源组和要引入平台的订阅，然后选择 **运行**;
* 在显示的JSON正文中，将以下Platform子网添加到 `virtualNetworkRules` in `properties`:


>[!IMPORTANT]
>
>在更新之前，您必须备份收到的JSON正文 `virtualNetworkRules` Platform子网，因为该子网包含您现有的IP过滤规则。 否则，将在调用后删除规则。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有关Platform子网的不同区域，请参阅下面的列表：

### VA7:北美洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2:欧洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### 澳大利亚5:澳大利亚

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

请参阅以下内容 [[!DNL Event Hubs] 文档](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) 以了解有关网络规则集的详细信息。

## 连接 [!DNL Event Hubs] 到平台

以下文档提供了有关如何连接的信息 [!DNL Event Hubs] 要使用API或用户界面实现平台，请执行以下操作：

### 使用API

* [使用流服务API创建事件中心源连接](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中创建事件中心源连接](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
