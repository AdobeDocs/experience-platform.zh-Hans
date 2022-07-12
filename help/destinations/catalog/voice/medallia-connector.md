---
title: Medallia连接
description: 激活定向Media调查和反馈收集的用户档案，以更好地了解客户需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---

# Medallia连接

## 概述 {#overview}

激活定向Media调查和反馈收集的用户档案，以更好地了解客户需求和期望。

>[!IMPORTANT]
>
>此文档页面由Medallia团队创建。 如有任何查询或更新请求，请直接通过adobe-integrations@medallia.com联系。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时应使用Medallia目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

B2B品牌希望评估并简化其入门计划。 他们希望向刚刚完成入门流程的客户实时发送个性化调查。

### 用例#2

零售商希望更好地了解客户对订单履行的偏好。 他们希望向过去一个月在线和店内购买的客户发送一个简短的1问短信调查。

## 先决条件 {#prerequisites}

建立Medallia连接需要以下信息：
* **OAuth令牌端点URL**
* **客户端ID**
* **客户端密钥**
* **API网关URL**
* **导入API名称**

与您的Medallia投放团队合作以获取这些详细信息。

## 支持的身份 {#supported-identities}

Medallia支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址 | 如果要发送电子邮件邀请调查，请选择电子邮件目标身份。 当某个用户档案与多个电子邮件地址关联时，Medallia将仅触发第一封电子邮件的邀请。 |
| phone | 电话号码以E.164格式进行哈希处理 | 如果要发送基于短信的调查，请选择电话目标身份。 电话号码必须采用E.164格式，其中包括加号(+)、国际国家/地区通话代码、地区代码和电话号码。 例如：(+)（国家/地区代码）（区号）（电话号码）。 当用户档案与多个电话号码关联时，Medallia将仅触发第一个电话号码的邀请。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您正在导出区段的所有新合格成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL OAuth令牌端点URL]**:通常采用https://instance.medallia.tld/oauth/tenant/token形式。
* **[!UICONTROL 客户端ID]**:从您的Medallia投放团队获取。
* **[!UICONTROL 客户端密钥]**:从您的Medallia投放团队获取。

![显示此目标的身份验证屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL API网关URL]**:从您的Medallia投放团队获取。 通常采用https://instance-tenant.apis.medallia.com形式。
* **[!UICONTROL 导入API名称]**:从您的Medallia投放团队获取。 在此连接中使用的Medallia Import API（也称为Web Feed）的名称。 您可以将不同的区段激活到不同的导入API以触发不同的调查程序。

![显示此目标的目标详细信息屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和标识 {#map}

必须根据用例映射以下目标标识命名空间：
* 对于基于电子邮件的调查， **电子邮件** 必须映射为目标字段(使用 **目标字段** > **选择身份命名空间** > **电子邮件**
* 对于基于短信的调查， **手机** 必须映射为目标字段(使用 **目标字段** > **选择身份命名空间** > **手机**. 电话号码必须采用E.164格式，其中包括加号(+)、国际国家/地区通话代码、地区代码和电话号码

强烈建议您还映射其他目标自定义属性以创建个性化调查，并将有关客户的其他信息附加到调查记录：

* 个性化调查通常按名称向客户提供地址
   * 将客户的名字映射到 **目标字段** > **选择自定义属性** > **属性名称** > **名字**
   * 将客户的姓氏映射到 **目标字段** > **选择自定义属性** > **属性名称** > **lastname**
* 根据需要为任何其他目标自定义属性添加映射

![显示标识和属性的示例映射的图像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 与您的Medallia投放团队共享确切的 **属性名称** 用于 **目标字段** > **选择自定义属性** > **属性名称**. 您可能希望直接共享映射页面的屏幕截图。

## 导出的数据 {#exported-data}

在将区段激活到目标后，请通知您的Medallia投放团队，该团队将能够验证从Adobe Experience Platform到Medallia的导出数据。 请注意，只有在成功验证数据后，才能在Medallia内激活调查；在此之前，数据将导出到Medallia ，但不会触发针对客户的调查。

下面提供了导出数据的示例JSON，它使用 **映射属性和标识** 部分：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).
