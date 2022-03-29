---
keywords: 流；
title: HTTP API连接
description: 利用Adobe Experience Platform中的HTTP API目标，可将配置文件数据发送到第三方HTTP端点。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 7acacc4a5ddd10f47da59837ad7dab2615d41789
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---

# （测试版）HTTP API连接

>[!IMPORTANT]
>
>Platform中的HTTP API目标当前处于测试阶段。 文档和功能可能会发生变化。

## 概述 {#overview}

HTTP API目标是 [!DNL Adobe Experience Platform] 流目标，帮助您将用户档案数据发送到第三方HTTP端点。

要将用户档案数据发送到HTTP端点，您必须先 [连接到目标](#connect-destination) in [!DNL Adobe Experience Platform].

## 用例 {#use-cases}

HTTP目标面向需要将XDM配置文件数据和受众区段导出到通用HTTP端点的客户。

HTTP端点可以是客户自己的系统或第三方解决方案。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望为公司启用HTTP API目标测试版功能，请联系您的Adobe代表或Adobe客户关怀团队。

要使用HTTP API目标导出Experience Platform外的数据，您必须满足以下先决条件：

* 您必须具有支持REST API的HTTP端点。
* 您的HTTP端点必须支持Experience Platform配置文件架构。 HTTP API目标不支持转换为第三方有效负载架构。 请参阅 [导出的数据](#exported-data) 部分，以了解Experience Platform输出模式的示例。
* 您的HTTP端点必须支持标头。
* 您的HTTP端点必须支持 [OAuth 2.0客户端凭据](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 身份验证。 当HTTP API目标处于测试阶段时，此要求有效。
* 客户端凭据需要包含在对您端点的POST请求正文中，如以下示例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

您还可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 以设置集成并将Experience Platform配置文件数据发送到HTTP端点。

## IP地址允许列表 {#ip-address-allowlist}

为满足客户的安全性和合规性要求，Experience Platform提供了一个静态IP列表，您可以允许列表为HTTP API目标进行管理。 请参阅 [流目标的IP地址允许列表](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以获取要的IP的完整列允许列表表。

## 连接到目标 {#connect-destination}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL httpEndpoint]**:the [!DNL URL] 要将用户档案数据发送到的HTTP端点的URL。
   * （可选）您可以将查询参数添加到 [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**:the [!DNL URL] 用于 [!DNL OAuth2] 身份验证。
* **[!UICONTROL 客户端ID]**:the [!DNL clientID] 参数 [!DNL OAuth2] 客户端凭据。
* **[!UICONTROL 客户端密钥]**:the [!DNL clientSecret] 参数 [!DNL OAuth2] 客户端凭据。

   >[!NOTE]
   >
   >仅 [!DNL OAuth2] 当前支持客户端凭据。

* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 自定义标题]**:按照以下格式，输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >当前实施至少需要一个自定义标头。 此限制将在将来的更新中解决。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#attributes}

在 [[!UICONTROL 选择属性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步骤，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择唯一标识符以及要导出到目标的任何其他XDM字段。

## 配置文件导出行为 {#profile-export-behavior}

Experience Platform会优化配置文件导出行为以导出到您的HTTP API目标，以便仅在区段鉴别或其他重大事件之后对配置文件进行相关更新时，才将数据导出到您的API端点。 在以下情况下，用户档案会导出到您的目标：

* 配置文件更新由至少一个映射到目标的区段的区段成员资格发生变化来确定。 例如，配置文件已符合映射到目标的其中一个区段的条件，或者已退出映射到目标的其中一个区段。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合映射到目标的某个区段资格条件的用户档案，已在身份映射属性中添加了新身份。
* 配置文件更新由至少一个映射到目标的属性的属性发生变化来确定。 例如，映射步骤中映射到目标的某个属性会添加到配置文件中。

在上述所有情况下，只会将发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段有一百个成员，并且有五个新的配置文件符合该区段的资格条件，则导出到目标的过程将是递增的，并且仅包含五个新配置文件。

请注意，无论更改位于何处，都会导出配置文件的所有映射属性。 因此，在上例中，即使属性本身未发生更改，也会导出这五个新配置文件的所有映射属性。

### 决定数据导出的因素以及导出中包含的内容 {#what-determines-export-what-is-included}

对于为给定用户档案导出的数据，了解 *什么决定了导出到HTTP API目标的数据* 和 *导出中包含哪些数据*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段可用作目标导出的提示。 这意味着，如果任何映射的区段更改状态（从null更改为已实现或从已实现/现有更改为退出）或任何映射的属性已更新，则将开始目标导出。</li><li>由于身份当前无法映射到HTTP API目标，因此给定配置文件中任何身份的更改也会决定目标导出。</li><li>属性的更改被定义为属性的任何更新，无论该更新是否与属性的值相同。 这意味着，即使值本身未发生更改，属性上的覆盖也会被视为更改。</li></ul> | <ul><li>所有区段（具有最新的成员资格状态），无论它们是否在数据流中映射，都会包含在 `segmentMembership` 对象。</li><li>中的所有标识 `identityMap` 对象也包含在内(Experience Platform当前不支持HTTP API目标中的身份映射)。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

例如，将此数据流视为HTTP目标，在该目标中，在数据流中选择了三个区段，并且有四个属性被映射到该目标。

![HTTP API目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的用户档案，可由符合或退出 *三个映射的区段*. 但是，在数据导出中， `segmentMembership` 对象(请参阅 [导出的数据](#exported-data) 部分)，则可能会显示其他未映射的区段，前提是该特定用户档案是其成员。 如果某个用户档案符合“使用德罗林汽车的客户”区段的资格条件，但同时也是“观看的‘回到未来’”电影和科幻片迷区段的成员，则另外两个区段也将出现在 `segmentMembership` 对象，即使这些对象未在数据流中映射。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个将出现在数据导出中。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据登陆您的 [!DNL HTTP] 目标。 例如，下面的导出包含符合特定区段资格条件、是另两个区段的成员并退出另一个区段的配置文件。 导出还包含配置文件属性名字、姓氏、出生日期和个人电子邮件地址。 此配置文件的标识为ECID和电子邮件。

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
