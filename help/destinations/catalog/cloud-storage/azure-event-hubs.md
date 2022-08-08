---
keywords: Azure事件中心目标；Azure事件中心；Azure事件Hub
title: Azure事件中心连接
description: 创建与的实时出站连接 [!DNL Azure Event Hubs] 存储以从Experience Platform流数据。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '2003'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] 连接

## 概述 {#overview}

>[!IMPORTANT]
>
> 此目标仅对 [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

[!DNL Azure Event Hubs] 是一种大数据流平台和事件摄取服务。 它每秒可以接收和处理数百万个事件。 通过使用任何实时分析提供程序或批量处理/存储适配器，可以转换和存储发送到事件中心的数据。

您可以创建与的实时出站连接 [!DNL Azure Event Hubs] 存储以从Adobe Experience Platform流数据。

* 有关 [!DNL Azure Event Hubs]，请参阅 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 连接到 [!DNL Azure Event Hubs] 以编程方式，请参阅 [流目标API教程](../../api/streaming-destinations.md).
* 连接到 [!DNL Azure Event Hubs] 使用Platform用户界面，请参阅以下部分。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 用例 {#use-cases}

通过使用流目标，例如 [!DNL Azure Event Hubs]，则您可以轻松地将高价值分段事件和关联的配置文件属性馈送到所选系统中。

例如，潜在客户下载了一份白皮书，使其符合“高倾向转化”区段的条件。 通过映射潜在客户所在的区段 [!DNL Azure Event Hubs] 目标，您将在 [!DNL Azure Event Hubs]. 在这里，您可以采用DIY（自己动手）方法，并在活动之上描述业务逻辑，因为您认为最适合企业IT系统。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP地址允许列表 {#ip-address-allowlist}

为满足客户的安全性和合规性要求，Experience Platform提供了一个静态IP列表，您可允许列表以在 [!DNL Azure Event Hubs] 目标。 请参阅 [流目标的IP地址允许列表](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以获取要的IP的完整列允许列表表。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 连接到此目标时，必须提供以下信息：

### 身份验证信息 {#authentication-information}

#### 标准身份验证 {#standard-authentication}

![UI屏幕的图像，显示Azure事件中心标准身份验证详细信息的已完成字段](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

如果您选择 **[!UICONTROL 标准身份验证]** 键入以连接到HTTP端点，输入以下字段并选择 **[!UICONTROL 连接到目标]**:

* **[!UICONTROL SAS密钥名称]**:授权规则的名称，也称为SAS密钥名称。
* **[!UICONTROL SAS密钥]**:事件中心命名空间的主键。 的 `sasPolicy` 该 `sasKey` 对应于必须拥有 **管理** 配置了权限，以便填充事件中心列表。 了解如何验证 [!DNL Azure Event Hubs] 在 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空间]**:填写 [!DNL Azure Event Hubs] 命名空间。 了解 [!DNL Azure Event Hubs] 命名空间 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### 共享访问签名(SAS)身份验证 {#sas-authentication}

![UI屏幕的图像，显示Azure事件中心标准身份验证详细信息的已完成字段](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

如果您选择 **[!UICONTROL 标准身份验证]** 键入以连接到HTTP端点，输入以下字段并选择 **[!UICONTROL 连接到目标]**:

* **[!UICONTROL SAS密钥名称]**:授权规则的名称，也称为SAS密钥名称。
* **[!UICONTROL SAS密钥]**:事件中心命名空间的主键。 的 `sasPolicy` 该 `sasKey` 对应于必须拥有 **管理** 配置了权限，以便填充事件中心列表。 了解如何验证 [!DNL Azure Event Hubs] 在 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空间]**:填写 [!DNL Azure Event Hubs] 命名空间。 了解 [!DNL Azure Event Hubs] 命名空间 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 命名空间]**:填写 [!DNL Azure Event Hubs] 命名空间。 了解 [!DNL Azure Event Hubs] 命名空间 [Microsoft文档](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="包括区段名称"
>abstract="如果您希望数据导出包含要导出的区段名称，则进行切换。 查看有关选定此选项的数据导出示例的文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="包含区段时间戳"
>abstract="如果您希望数据导出在创建和更新区段时包含UNIX时间戳，以及将区段映射到要激活的目标时包含UNIX时间戳，则进行切换。 查看有关选定此选项的数据导出示例的文档。"

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![UI屏幕的图像，显示Azure事件中心目标详细信息的已完成字段](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL 名称]**:填写连接的名称 [!DNL Azure Event Hubs].
* **[!UICONTROL 描述]**:提供连接的描述。  示例：“高级客户”、“对冲浪感兴趣的客户”。
* **[!UICONTROL eventHubName]**:为您的 [!DNL Azure Event Hubs] 目标。
* **[!UICONTROL 包括区段名称]**:如果您希望数据导出包含要导出的区段名称，则进行切换。 有关选中此选项的数据导出示例，请参阅 [导出的数据](#exported-data) 部分。
* **[!UICONTROL 包含区段时间戳]**:如果您希望数据导出在创建和更新区段时包含UNIX时间戳，以及将区段映射到要激活的目标时包含UNIX时间戳，则进行切换。 有关选中此选项的数据导出示例，请参阅 [导出的数据](#exported-data) 部分。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## 配置文件导出行为 {#profile-export-behavior}

Experience Platform会优化将用户档案导出到 [!DNL Azure Event Hubs] 目标，以便仅在区段鉴别或其他重要事件后对配置文件进行相关更新时，才将数据导出到您的目标。 在以下情况下，用户档案会导出到您的目标：

* 配置文件更新由至少一个映射到目标的区段的区段成员资格发生变化来确定。 例如，配置文件已符合映射到目标的其中一个区段的条件，或者已退出映射到目标的其中一个区段。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合映射到目标的某个区段资格条件的用户档案，已在身份映射属性中添加了新身份。
* 配置文件更新由至少一个映射到目标的属性的属性发生变化来确定。 例如，映射步骤中映射到目标的某个属性会添加到配置文件中。

在上述所有情况下，只会将发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段有一百个成员，并且有五个新的配置文件符合该区段的资格条件，则导出到目标的过程将是递增的，并且仅包含五个新配置文件。

请注意，无论更改位于何处，都会导出配置文件的所有映射属性。 因此，在上例中，即使属性本身未发生更改，也会导出这五个新配置文件的所有映射属性。

### 决定数据导出的因素以及导出中包含的内容 {#what-determines-export-what-is-included}

对于为给定用户档案导出的数据，了解 *什么决定了要将数据导出到 [!DNL Azure Event Hubs] 目标* 和 *导出中包含哪些数据*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段可用作目标导出的提示。 这意味着，如果任何映射的区段更改状态（从null更改为已实现或从已实现/现有更改为退出）或任何映射的属性已更新，则将开始目标导出。</li><li>由于身份当前无法映射到 [!DNL Azure Event Hubs] 目标中，给定配置文件中任何标识的更改也会决定目标导出。</li><li>属性的更改被定义为属性的任何更新，无论该更新是否与属性的值相同。 这意味着，即使值本身未发生更改，属性上的覆盖也会被视为更改。</li></ul> | <ul><li>所有区段（具有最新的成员资格状态），无论它们是否在数据流中映射，都会包含在 `segmentMembership` 对象。</li><li>中的所有标识 `identityMap` 对象(Experience Platform当前不支持在 [!DNL Azure Event Hubs] 目标)。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

例如，将此数据流视为 [!DNL Azure Event Hubs] 目标，其中在数据流中选择了三个区段，并有四个属性映射到目标。

![Amazon Kinesis目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的用户档案，可由符合或退出 *三个映射的区段*. 但是，在数据导出中， `segmentMembership` 对象(请参阅 [导出的数据](#exported-data) 部分)，则可能会显示其他未映射的区段，前提是该特定用户档案是其成员。 如果某个用户档案符合“使用德罗林汽车的客户”区段的资格条件，但同时也是“观看的‘回到未来’”电影和科幻片迷区段的成员，则另外两个区段也将出现在 `segmentMembership` 对象，即使这些对象未在数据流中映射。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个将出现在数据导出中。

## 历史数据回填 {#historical-data-backfill}

当您向现有目标添加新区段时，或者当您创建新目标并将区段映射到该目标时，Experience Platform会将历史区段鉴别数据导出到该目标。 符合区段资格条件的用户档案 *之前* 已添加到目标的区段会在大约一小时内导出到目标。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据登陆您的 [!DNL Azure Event Hubs] 目标。 例如，下面的导出包含符合特定区段资格条件、是另两个区段的成员并退出另一个区段的配置文件。 导出还包含配置文件属性名字、姓氏、出生日期和个人电子邮件地址。 此配置文件的标识为ECID和电子邮件。

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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

以下是导出数据的更多示例，具体取决于您在的连接目标流中为 **[!UICONTROL 包括区段名称]** 和 **[!UICONTROL 包含区段时间戳]** 选项：

+++ 以下数据导出示例包括 `segmentMembership` 部分

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 以下数据导出示例包括 `segmentMembership` 部分

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 限制和重试策略 {#limits-retry-policy}

在95%的时间内，Experience Platform尝试为成功发送的消息提供少于10分钟的吞吐量延迟，每个数据流的请求速率低于每秒10,000次，以发送到HTTP目标。

如果对HTTP API目标的请求失败，Experience Platform会存储失败的请求并重试两次，以将请求发送到您的端点。

>[!MORELIKETHIS]
>
>* [连接到Azure事件中心并使用流服务API激活数据](../../api/streaming-destinations.md)
>* [AWS Kinesis目标](./amazon-kinesis.md)
>* [目标类型和类别](../../destination-types.md)

