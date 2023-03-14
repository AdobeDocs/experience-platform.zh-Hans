---
keywords: 流；HTTP目标
title: HTTP API连接
description: 使用Adobe Experience Platform中的HTTP API目标将配置文件数据发送到第三方HTTP端点，以运行您自己的Analytics或执行您可能需要对从Experience Platform导出的配置文件数据执行的任何其他操作。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: b6d7ae987bbc97b3f58bd10ef181145ae89aa63e
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---

# HTTP API连接

## 概述 {#overview}

>[!IMPORTANT]
>
> 此目标仅适用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

HTTP API目标是 [!DNL Adobe Experience Platform] 可帮助您将配置文件数据发送到第三方HTTP端点的流式目标。

要将配置文件数据发送到HTTP端点，您必须首先 [连接到目标](#connect-destination) 在 [!DNL Adobe Experience Platform].

## 用例 {#use-cases}

HTTP API目标允许您将XDM配置文件数据和受众区段导出到通用HTTP端点。 在那里，您可以运行自己的Analytics，或者对从Experience Platform中导出的用户档案数据执行任何其他您可能需要的操作。

HTTP端点可以是客户自己的系统或第三方解决方案。

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），这些字段是在 [目标激活工作流](../../ui/activate-segment-streaming-destinations.md#mapping). |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要使用HTTP API目标从Experience Platform中导出数据，您必须满足以下先决条件：

* 您必须具有支持REST API的HTTP端点。
* 您的HTTP端点必须支持Experience Platform配置文件架构。 HTTP API目标不支持转换到第三方有效负载架构。 请参阅 [导出的数据](#exported-data) 部分中的Experience Platform输出架构示例。
* 您的HTTP端点必须支持标头。

>[!TIP]
>
> 您还可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 以设置集成并将Experience Platform配置文件数据发送到HTTP端点。

## 允许列表 IP地址 {#ip-address-allowlist}

为了满足客户的安全性和合规性要求，Experience Platform提供了一个您可以为HTTP API目标允许列表的静态IP列表。 请参阅 [流目标的IP地址允许列表](/help/destinations/catalog/streaming/ip-address-allow-list.md) 要允许列表的IP的完整列表。

## 支持的身份验证类型 {#supported-authentication-types}

HTTP API目标支持对HTTP端点使用多种身份验证类型：

* 没有身份验证的HTTP端点；
* 持有者令牌认证；
* [OAuth 2.0客户端凭据](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 使用body表单进行身份验证，使用 [!DNL client ID]， [!DNL client secret] 和 [!DNL grant type] （在HTTP请求正文中），如以下示例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0客户端凭据](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 具有基本授权，并具有包含URL编码的授权标头 [!DNL client ID] 和 [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0密码授予](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## 连接到目标 {#connect-destination}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 连接到此目标时，必须提供以下信息：

### 身份验证信息 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="客户端凭据类型"
>abstract="选择 **正文表单已编码** 在请求正文中包含客户端ID和客户端密钥，或者 **基本授权** 在授权标头中包含客户端ID和客户端密码。 查看文档中的示例。"

#### 持有者令牌身份验证 {#bearer-token-authentication}

如果您选择 **[!UICONTROL 持有者令牌]** 要连接到HTTP端点的身份验证类型，请输入以下字段并选择 **[!UICONTROL 连接到目标]**：

![可在其中使用持有者令牌身份验证连接到HTTP API目标的UI屏幕的图像](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 持有者令牌]**：插入持有者令牌以对HTTP位置进行身份验证。

#### 无身份验证 {#no-authentication}

如果您选择 **[!UICONTROL 无]** 要连接到HTTP端点的身份验证类型：

![可在其中不使用身份验证连接到HTTP API目标的UI屏幕图像](../../assets/catalog/http/http-api-authentication-none.png)

当选择此身份验证打开时，您只需选择 **[!UICONTROL 连接到目标]** 并建立与端点的连接。

#### OAuth 2密码身份验证 {#oauth-2-password-authentication}

如果您选择 **[!UICONTROL OAuth 2密码]** 要连接到HTTP端点的身份验证类型，请输入以下字段并选择 **[!UICONTROL 连接到目标]**：

![UI屏幕的图像，您可以在其中使用带有密码身份验证的OAuth 2连接到HTTP API目标](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 访问令牌URL]**：您颁发访问令牌和刷新令牌（可选）的URL。
* **[!UICONTROL 客户端ID]**：此 [!DNL client ID] 系统分配给Adobe Experience Platform的区段。
* **[!UICONTROL 客户端密码]**：此 [!DNL client secret] 系统分配给Adobe Experience Platform的区段。
* **[!UICONTROL 用户名]**：用于访问HTTP端点的用户名。
* **[!UICONTROL 密码]**：用于访问HTTP端点的密码。

#### OAuth 2客户端凭据身份验证 {#oauth-2-client-credentials-authentication}

如果您选择 **[!UICONTROL OAuth 2客户端凭据]** 要连接到HTTP端点的身份验证类型，请输入以下字段并选择 **[!UICONTROL 连接到目标]**：

![UI屏幕的图像，您可以在其中通过客户端凭据身份验证使用OAuth 2连接到HTTP API目标](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL 访问令牌URL]**：您颁发访问令牌和刷新令牌（可选）的URL。
* **[!UICONTROL 客户端ID]**：此 [!DNL client ID] 系统分配给Adobe Experience Platform的区段。
* **[!UICONTROL 客户端密码]**：此 [!DNL client secret] 系统分配给Adobe Experience Platform的区段。
* **[!UICONTROL 客户端凭据类型]**：选择您的端点支持的OAuth2客户端凭据授予类型：
   * **[!UICONTROL 正文表单已编码]**：在本例中， [!DNL client ID] 和 [!DNL client secret] 包括 *在请求正文中* 已发送到您的目标。 有关示例，请参阅 [支持的身份验证类型](#supported-authentication-types) 部分。
   * **[!UICONTROL 基本授权]**：在本例中， [!DNL client ID] 和 [!DNL client secret] 包括 *在 `Authorization` 标头* 在经过base64编码并发送到您的目标之后。 有关示例，请参阅 [支持的身份验证类型](#supported-authentication-types) 部分。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="标头"
>abstract="按照以下格式，输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP端点"
>abstract="要将配置文件数据发送到的HTTP端点的URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包括区段名称"
>abstract="如果希望数据导出包含要导出的区段名称，请进行切换。 查看选中此选项的数据导出示例文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括区段时间戳"
>abstract="如果希望数据导出包括创建和更新区段时的UNIX时间戳，以及将区段映射到目标以供激活时的UNIX时间戳，请进行切换。 查看选中此选项的数据导出示例文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查询参数"
>abstract="或者，您也可以向HTTP端点URL添加查询参数。 将您使用的查询参数设置为如下格式： `parameter1=value&parameter2=value`."

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示HTTP目标详细信息的已完成字段的UI屏幕的图像](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名称]**：输入将来识别此目标时所依据的名称。
* **[!UICONTROL 描述]**：输入可帮助您将来识别此目标的描述。
* **[!UICONTROL 标头]**：输入要包含在目标调用中的任何自定义标头，格式如下： `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP端点]**：要将配置文件数据发送到的HTTP端点的URL。
* **[!UICONTROL 查询参数]**：或者，您也可以向HTTP端点URL添加查询参数。 将您使用的查询参数设置为如下格式： `parameter1=value&parameter2=value`.
* **[!UICONTROL 包括区段名称]**：如果希望数据导出包含要导出的区段名称，请进行切换。 有关选中此选项后数据导出的示例，请参阅 [导出的数据](#exported-data) 章节。
* **[!UICONTROL 包括区段时间戳]**：如果希望数据导出包括创建和更新区段时的UNIX时间戳，以及将区段映射到目标以供激活时的UNIX时间戳，请进行切换。 有关选中此选项后数据导出的示例，请参阅 [导出的数据](#exported-data) 章节。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#attributes}

在 [[!UICONTROL 选择属性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步骤，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。

## 配置文件导出行为 {#profile-export-behavior}

Experience Platform会优化将配置文件导出到HTTP API目标的行为，以便仅在符合区段资格或其他重要事件后对配置文件进行了相关更新时将数据导出到API端点。 在以下情况下，会将配置文件导出到您的目标：

* 配置文件更新由映射到目标的至少一个区段的区段成员资格更改确定。 例如，配置文件已符合映射到目标的其中一个区段的条件，或已退出映射到目标的其中一个区段。
* 配置文件更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已经符合映射到目标的其中一个区段资格的配置文件，已在标识映射属性中添加了一个新标识。
* 配置文件更新由映射到目标的至少一个属性的更改确定。 例如，会将映射步骤中映射到目标的某个属性添加到配置文件中。

在上述所有情况下，只会将已发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段具有一百个成员，并且有五个新用户档案符合该区段的条件，则导出到目标的操作将以增量方式进行，并且只包含五个新用户档案。

请注意，无论更改发生在何处，都将为配置文件导出所有映射的属性。 因此，在上面的示例中，将导出这五个新配置文件的所有映射属性，即使属性本身未发生更改也是如此。

### 决定数据导出的因素以及导出中包含的内容 {#what-determines-export-what-is-included}

对于为给定用户档案导出的数据，了解以下两个不同的概念很重要： *确定导出到HTTP API目标的数据的方法* 和 *哪些数据包含在导出中*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段会作为目标导出的提示。 这意味着，如果任何映射的区段更改状态（从null更改为已实现，或从已实现/现有更改为现有）或任何映射的属性被更新，则将启动目标导出。</li><li>由于身份当前无法映射到HTTP API目标，因此给定配置文件上任何身份的更改也将决定目标导出。</li><li>属性的更改被定义为属性上的任何更新，无论它是不是同一个值。 这意味着即使值本身未发生更改，对属性的覆盖也会被视为更改。</li></ul> | <ul><li>此 `segmentMembership` 对象包括激活数据流中映射的区段，在发生资格或区段退出事件后，用户档案的状态已发生更改。 请注意，配置文件符合条件的其他未映射区段也可以作为目标导出的一部分（如果这些区段属于同一个） [合并策略](/help/profile/merge-policies/overview.md) 区段在激活数据流中映射时相同。 </li><li>中的所有标识 `identityMap` 对象也包含在内(Experience Platform当前不支持HTTP API目标中的标识映射)。</li><li>目标导出中仅包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

例如，考虑将此数据流映射到HTTP目标，其中在数据流中选择了三个区段，并且四个属性映射到目标。

![HTTP API目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的配置文件可由符合或退出其中一个配置文件的配置文件来确定 *三个映射区段*. 但是，在数据导出中，在 `segmentMembership` 对象(请参阅 [导出的数据](#exported-data) 如果特定配置文件是其他未映射区段的成员，并且这些区段与触发导出的区段共享相同的合并策略，则可能会显示其他未映射区段。 如果配置文件符合 **使用德洛雷亚汽车的客户** 区段，但同时也是 **观看了《回到未来》** 电影和 **科幻迷们** 区段，则其他这两个区段也将显示在 `segmentMembership` 数据导出对象，即使这些对象未在数据流中映射，只要它们与共享相同的合并策略 **使用德洛雷亚汽车的客户** 区段。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个都将出现在数据导出中。

## 历史数据回填 {#historical-data-backfill}

向现有目标添加新区段时，或者创建新目标并将区段映射到该目标时，Experience Platform会将历史区段资格数据导出到该目标。 符合区段资格的用户档案 *早于* 添加到目标的区段会在大约1小时内导出到目标。

## 导出的数据 {#exported-data}

已导出 [!DNL Experience Platform] 数据登陆您的 [!DNL HTTP] JSON格式的目标。 例如，以下导出包含一个符合某个区段资格条件的配置文件，该配置文件是另一个区段的成员，并且退出另一个区段。 导出还包括配置文件属性的名字、姓氏、出生日期和个人电子邮件地址。 此配置文件的身份是ECID和电子邮件。

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

下面是导出数据的更多示例，具体取决于您在连接目标流中为选择的UI设置 **[!UICONTROL 包括区段名称]** 和 **[!UICONTROL 包括区段时间戳]** 选项：

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

在95%的时间中，Experience Platform会尝试为成功发送的消息提供少于10分钟的吞吐量延迟，每个数据流向HTTP目标的请求速率低于每秒10,000个请求。

如果对HTTP API目标的请求失败，Experience Platform会存储失败的请求，并重试两次以将请求发送到您的端点。