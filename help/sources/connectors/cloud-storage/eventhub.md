---
title: Azure事件中枢源连接器概述
description: 了解如何使用API或用户界面将Azure事件中心连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] 源

>[!IMPORTANT]
>
>此 [!DNL Azure Event Hubs] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]、和 [!DNL Azure]. 您可以将来自这些系统的数据导入Platform。

云存储源可以将您自己的数据引入Platform，而无需下载、格式化或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 Platform允许您从以下位置引入数据 [!DNL Event Hubs] 实时。

## 缩放方式 [!DNL Event Hubs]

的缩放因子 [!DNL Event Hubs] 如果需要引入大量数据、增加并行度或提高引入平台的速度，则必须增加实例。

### 输入较大量的数据

目前，您可以从 [!DNL Event Hubs] account to Platform是每秒2000条记录。 要扩展并摄取更大数量的数据，请联系您的Adobe代表。

### 增加上的并行度 [!DNL Event Hubs] 和平台

并行是指在多个处理单元上同时执行相同的任务，以提高速度和性能。 您可以提高 [!DNL Event Hubs] 增加分区或获取更多处理单元 [!DNL Event Hubs] 帐户。 查看此 [[!DNL Event Hubs] 缩放文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 了解更多信息。

要提高平台端的摄取速度，平台必须增加源连接器中要读取的任务数 [!DNL Event Hubs] 分区。 一旦您增加了 [!DNL Event Hubs] ，请联系您的Adobe代表以根据新分区扩展Platform任务。 目前，此过程未自动化。

## 使用虚拟网络连接到 [!DNL Event Hubs] 目标平台

您可以设置要连接的虚拟网络 [!DNL Event Hubs] 到Platform ，同时启用防火墙措施。 要设置虚拟网络，请转到此 [[!DNL Event Hubs] 网络规则集文档](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 并执行以下步骤：

* 选择 **试试看** 从REST API面板；
* 验证您的 [!DNL Azure] 在同一浏览器中使用您的凭据的帐户；
* 选择 [!DNL Event Hubs] 命名空间、资源组和订阅，然后选择 **运行**；
* 在显示的JSON正文中，添加以下平台子网至 `virtualNetworkRules` 内部 `properties`：


>[!IMPORTANT]
>
>在更新之前，必须对收到的JSON正文进行备份 `virtualNetworkRules` ，因为它包含您现有的IP过滤规则。 否则，将在调用后删除规则。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有关Platform子网的不同区域，请参阅以下列表：

### VA7：北美洲

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
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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

## Connect [!DNL Event Hubs] 目标平台

以下文档提供了有关如何连接的信息 [!DNL Event Hubs] 至使用API或用户界面的Platform：

### 使用API

* [使用流服务API创建事件中心源连接](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中创建事件中心源连接](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
