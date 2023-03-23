---
keywords: 流；HTTP目标
title: HTTP API连接
description: 使用Adobe Experience Platform中的HTTP API目标，将配置文件数据发送到第三方HTTP端点，以运行您自己的分析，或对导出为Experience Platform外的配置文件数据执行可能需要的任何其他操作。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: e22472443eef8aa053aeb0eb35488de581e4b2bd
workflow-type: tm+mt
source-wordcount: '2648'
ht-degree: 7%

---

# HTTP API连接

## 概述 {#overview}

>[!IMPORTANT]
>
> 此目标仅对 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

HTTP API目标是 [!DNL Adobe Experience Platform] 流目标，帮助您将用户档案数据发送到第三方HTTP端点。

要将用户档案数据发送到HTTP端点，您必须先 [连接到目标](#connect-destination) in [!DNL Adobe Experience Platform].

## 用例 {#use-cases}

利用HTTP API目标，可将XDM配置文件数据和受众区段导出到通用HTTP端点。 在此，您可以运行自己的分析，或对导出为非Experience Platform的用户档案数据执行任何其他所需操作。

HTTP端点可以是客户自己的系统或第三方解决方案。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](../../ui/activate-segment-streaming-destinations.md#mapping). |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要使用HTTP API目标导出Experience Platform外的数据，您必须满足以下先决条件：

* 您必须具有支持REST API的HTTP端点。
* 您的HTTP端点必须支持Experience Platform配置文件架构。 HTTP API目标不支持转换为第三方有效负载架构。 请参阅 [导出的数据](#exported-data) 部分，以了解Experience Platform输出模式的示例。
* 您的HTTP端点必须支持标头。

>[!TIP]
>
> 您还可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 以设置集成并将Experience Platform配置文件数据发送到HTTP端点。

## IP地址允许列表 {#ip-address-allowlist}

为满足客户的安全性和合规性要求，Experience Platform提供了一个静态IP列表，您可以允许列表为HTTP API目标进行管理。 请参阅 [流目标的IP地址允许列表](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以获取要的IP的完整列允许列表表。

## 支持的身份验证类型 {#supported-authentication-types}

HTTP API目标支持对HTTP端点进行多种身份验证类型：

* HTTP端点，且无身份验证；
* 承载令牌认证；
* [OAuth 2.0客户端凭据](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 使用body表单进行验证，使用 [!DNL client ID], [!DNL client secret] 和 [!DNL grant type] ，如以下示例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0客户端凭据](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 具有基本授权，且具有包含URL编码的授权标头 [!DNL client ID] 和 [!DNL client secret].

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
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 连接到此目标时，必须提供以下信息：

### 身份验证信息 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="客户端凭据类型"
>abstract="选择&#x200B;**编码的正文形式**&#x200B;以在请求正文中包含客户端 ID 和客户端密码，或选择&#x200B;**基本授权**&#x200B;以在授权标头中包含客户端 ID 和客户端密码。查看文档中的示例。"

#### 承载令牌身份验证 {#bearer-token-authentication}

如果您选择 **[!UICONTROL 载体令牌]** 连接到HTTP端点的身份验证类型，输入以下字段并选择 **[!UICONTROL 连接到目标]**:

![UI屏幕的图像，您可以在该屏幕中使用承载令牌身份验证连接到HTTP API目标](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 载体令牌]**:插入载体令牌以对HTTP位置进行身份验证。

#### 无身份验证 {#no-authentication}

如果您选择 **[!UICONTROL 无]** 连接到HTTP端点的身份验证类型：

![UI屏幕的图像，在该屏幕中，您无需进行身份验证即可连接到HTTP API目标](../../assets/catalog/http/http-api-authentication-none.png)

当您选择此身份验证打开时，您只需选择 **[!UICONTROL 连接到目标]** 并且已建立与您端点的连接。

#### OAuth 2密码验证 {#oauth-2-password-authentication}

如果您选择 **[!UICONTROL OAuth 2密码]** 连接到HTTP端点的身份验证类型，输入以下字段并选择 **[!UICONTROL 连接到目标]**:

![使用带密码身份验证的OAuth 2，可以连接到HTTP API目标的UI屏幕图像](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 访问令牌URL]**:您身边的URL，会发出访问令牌和（可选）刷新令牌的问题。
* **[!UICONTROL 客户端ID]**:的 [!DNL client ID] 系统分配给Adobe Experience Platform。
* **[!UICONTROL 客户端密钥]**:的 [!DNL client secret] 系统分配给Adobe Experience Platform。
* **[!UICONTROL 用户名]**:用于访问HTTP端点的用户名。
* **[!UICONTROL 密码]**:访问HTTP端点的密码。

#### OAuth 2客户端凭据身份验证 {#oauth-2-client-credentials-authentication}

如果您选择 **[!UICONTROL OAuth 2客户端凭据]** 连接到HTTP端点的身份验证类型，输入以下字段并选择 **[!UICONTROL 连接到目标]**:

![UI屏幕的图像，您可以在该屏幕中使用带有客户端凭据身份验证的OAuth 2连接到HTTP API目标](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL 访问令牌URL]**:您身边的URL，会发出访问令牌和（可选）刷新令牌的问题。
* **[!UICONTROL 客户端ID]**:的 [!DNL client ID] 系统分配给Adobe Experience Platform。
* **[!UICONTROL 客户端密钥]**:的 [!DNL client secret] 系统分配给Adobe Experience Platform。
* **[!UICONTROL 客户端凭据类型]**:选择您的端点支持的OAuth2客户端凭据授予类型：
   * **[!UICONTROL 已编码的正文形式]**:在本例中， [!DNL client ID] 和 [!DNL client secret] 包含 *请求正文中* 发送到您的目标。 有关示例，请参阅 [支持的身份验证类型](#supported-authentication-types) 中。
   * **[!UICONTROL 基本授权]**:在本例中， [!DNL client ID] 和 [!DNL client secret] 包含 *在 `Authorization` 标题* 进行base64编码并发送到您的目标后，Analytics会立即删除。 有关示例，请参阅 [支持的身份验证类型](#supported-authentication-types) 中。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="标头"
>abstract="按照以下格式输入要包含在目标调用中的任何自定义标头：`header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP 端点"
>abstract="要将配置文件数据发送到的 HTTP 端点的 URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包括区段名称"
>abstract="如果您希望数据导出包括正在导出的区段的名称，请进行切换。在选中此选项后查看数据导出示例的文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括区段时间戳"
>abstract="如果您希望数据导出包括区段创建时间和更新时间的 Unix 时间戳，以及区段映射到用于激活的目标时的 Unix 时间戳，请进行切换。在选中此选项后查看数据导出示例的文档。**在平台中监控用户活动**<h2>描述</h2><p>您可以以审核日志的形式监控各种平台服务和功能的用户活动。 这些日志构成一个记录的审核跟踪 <b>who</b> 执行 <b>什么</b> 操作和 <b>when</b>. 审核日志可帮助解决平台上的问题，并帮助您的企业有效遵守公司数据管理策略和法规要求。</p><h2>说明</h2><ul><li>选择 <b>审核</b> 中。 “审核”工作区会显示记录日志的列表，默认情况下，该列表按从最近到最近的顺序进行排序。</li>   <li> 注意：审核日志会保留365天，之后这些日志将从系统中删除。 因此，您最长只能返回365天。 如果您需要回顾超过365天的数据，则应当以常规频率导出日志，以满足内部策略要求。 </li><li>从列表中选择事件，以在右边栏中查看其详细信息。 </li><li>选择漏斗图标以显示过滤器控件列表，以帮助缩小结果范围。 无论选择何种过滤器，都只显示最后1000条记录。 </li><li>要导出当前审核日志列表，请选择 **下载日志**.</li><li>有关此功能的更多帮助，请参阅 <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hans">审核日志概述</a> Experience League。</li></ul>"

[!CONTEXTUALHELP]
id="platform_destinations_connect_http_queryparameters"
title="查询参数"
abstract="（可选）您可以将查询参数添加到 HTTP 端点 URL。格式化您使用的查询参数，如下所示：`parameter1=value&parameter2=value`。"

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示HTTP目标详细信息的已完成字段的UI屏幕图像](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 标题]**:按照以下格式，输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP端点]**:要将用户档案数据发送到的HTTP端点的URL。
* **[!UICONTROL 查询参数]**:或者，您也可以将查询参数添加到HTTP端点URL。 格式化您使用的查询参数，如下所示：`parameter1=value&parameter2=value`。
* **[!UICONTROL 包括区段名称]**:如果您希望数据导出包含要导出的区段名称，则进行切换。 有关选中此选项的数据导出示例，请参阅 [导出的数据](#exported-data) 部分。
* **[!UICONTROL 包含区段时间戳]**:如果您希望数据导出在创建和更新区段时包含UNIX时间戳，以及将区段映射到要激活的目标时包含UNIX时间戳，则进行切换。 有关选中此选项的数据导出示例，请参阅 [导出的数据](#exported-data) 部分。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

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
| <ul><li>映射的属性和区段可用作目标导出的提示。 这意味着，如果任何映射的区段更改状态（从null更改为已实现或从已实现/现有更改为退出）或任何映射的属性已更新，则将开始目标导出。</li><li>由于身份当前无法映射到HTTP API目标，因此给定配置文件中任何身份的更改也会决定目标导出。</li><li>属性的更改被定义为属性的任何更新，无论该更新是否与属性的值相同。 这意味着，即使值本身未发生更改，属性上的覆盖也会被视为更改。</li></ul> | <ul><li>的 `segmentMembership` 对象包括在激活数据流中映射的区段，在鉴别或区段退出事件后，配置文件的状态发生了更改。 请注意，如果配置文件符合条件的其他未映射区段属于同一区段，则这些区段可能属于目标导出的一部分 [合并策略](/help/profile/merge-policies/overview.md) 作为激活数据流中映射的区段。 </li><li>中的所有标识 `identityMap` 对象也包含在内(Experience Platform当前不支持HTTP API目标中的身份映射)。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

例如，将此数据流视为HTTP目标，在该目标中，在数据流中选择了三个区段，并且有四个属性被映射到该目标。

![HTTP API目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的用户档案，可由符合或退出 *三个映射的区段*. 但是，在数据导出中， `segmentMembership` 对象(请参阅 [导出的数据](#exported-data) 部分)，则可能会显示其他未映射的区段，如果该特定配置文件是其成员，并且这些区段与触发导出的区段共享相同的合并策略。 如果用户档案符合 **使用德罗林汽车的客户** 区段，但亦为 **观看了“回到未来”** 电影和 **科幻迷** 区段，则另外两个区段也将显示在 `segmentMembership` 数据导出对象，即使这些对象未在数据流中映射，但前提是它们与 **使用德罗林汽车的客户** 区段。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个将出现在数据导出中。

## 历史数据回填 {#historical-data-backfill}

当您向现有目标添加新区段时，或者当您创建新目标并将区段映射到该目标时，Experience Platform会将历史区段鉴别数据导出到该目标。 符合区段资格条件的用户档案 *之前* 已添加到目标的区段会在大约一小时内导出到目标。

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