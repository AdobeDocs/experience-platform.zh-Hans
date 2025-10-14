---
title: Azure事件中心Source连接器概述
description: 了解如何使用API或用户界面将Azure事件中心连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 02c777b5db9734cf45b35f131d83c35c5ce670fb
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# [!DNL Azure Event Hubs]源

>[!IMPORTANT]
>
>* [!DNL Azure Event Hubs]源在源目录中可供已购买Real-Time CDP Ultimate的用户使用。
>
>* 在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以使用[!DNL Azure Event Hubs]源。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将来自这些系统的数据导入Experience Platform。

云存储源可以将您自己的数据导入Experience Platform，而无需下载、设置格式或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 Experience Platform允许您从[!DNL Event Hubs]实时引入数据。

## 使用[!DNL Event Hubs]缩放

如果需要引入大量数据、增加并行度或提高Experience Platform上的引入速度，则必须增加[!DNL Event Hubs]实例的缩放因子。

### 传入更大容量数据

目前，您可以从[!DNL Event Hubs]帐户向Experience Platform引入的最大数据量为每秒2000条记录。 要扩展并摄取更大数量的数据，请联系您的Adobe代表。

### 提高[!DNL Event Hubs]和Experience Platform的并行度

并行是指在多个处理单元上同时执行相同的任务，以提高速度和性能。 您可以通过增加分区或为[!DNL Event Hubs]帐户获取更多处理单元来增加[!DNL Event Hubs]端的并行度。 有关详细信息，请参阅有关缩放[[!DNL Event Hubs] 的此](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability)文档。

要提高Experience Platform端的摄取速度，Experience Platform必须增加源连接器中要从[!DNL Event Hubs]分区中读取的任务数。 增加[!DNL Event Hubs]端的并行度后，请联系您的Adobe代表以根据新分区缩放Experience Platform任务。 目前，此过程未自动化。

## 使用虚拟网络连接到[!DNL Event Hubs]到Experience Platform

Experience Platform支持通过虚拟网络连接到[!DNL Event Hubs]。 这样，您就可以通过安全的专用连接（而非公共Internet）传输数据。 您可以允许列表Experience Platform VNet通过[!DNL Event Hubs]私有主干安全地路由[!DNL Azure]流量，同时保持现有的防火墙保护。

要设置虚拟网络，请转到此[[!DNL Event Hubs] 网络规则集文档](https://learn.microsoft.com/en-us/azure/event-hubs/network-security)，然后执行以下步骤：

* 从REST API面板中选择&#x200B;**尝试**；
* 在同一浏览器中使用你的凭据验证你的[!DNL Azure]帐户；
* 选择要带到Experience Platform的[!DNL Event Hubs]命名空间、资源组和订阅，然后选择&#x200B;**运行**；
* 在显示的JSON正文中，在`virtualNetworkRules`内的`properties`下添加以下Experience Platform子网：


>[!IMPORTANT]
>
>在使用Experience Platform子网更新`virtualNetworkRules`之前，必须对收到的JSON正文进行备份，因为它包含您现有的IP过滤规则。 否则，将在调用之后删除规则。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有关Experience Platform子网的不同区域，请参阅以下列表：

### VA7：北美

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

### NLD2：欧洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5：澳大利亚

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

有关网络规则集的详细信息，请参阅以下[[!DNL Event Hubs] 文档](https://learn.microsoft.com/en-us/azure/event-hubs/network-security)。

## 将[!DNL Event Hubs]连接到Experience Platform

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

以下文档提供了有关如何使用API或用户界面将[!DNL Event Hubs]连接到Experience Platform的信息：

### 使用API

* [使用流服务API创建事件中心源连接](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中创建事件中心源连接](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
