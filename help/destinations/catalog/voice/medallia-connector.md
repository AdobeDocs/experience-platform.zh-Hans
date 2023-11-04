---
title: Medallia连接
description: 激活目标Medallia调查和反馈收集的用户档案，以更好地了解客户的需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---

# Medallia连接

## 概述 {#overview}

激活目标Medallia调查和反馈收集的用户档案，以更好地了解客户的需求和期望。

>[!IMPORTANT]
>
>此目标连接器和文档页面由Medallia团队创建和维护。 如有任何查询或更新请求，请直接通过adobe-integrations@medallia.com联系。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时应使用Medallia目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

B2B品牌希望评估和简化其入职计划。 他们希望向刚刚完成入门培训流程的客户实时发送个性化调查。

### 用例#2

零售商希望更好地了解客户对订单履行情况的偏好。 他们希望向过去一个月内在线和店内购买过产品的客户发送一份简短的1个问题短信调查。

## 先决条件 {#prerequisites}

建立Medallia连接需要以下信息：
* **OAuth令牌端点URL**
* **客户端ID**
* **客户端密码**
* **API网关URL**
* **导入API名称**

请与您的Medallia交付团队合作以获取这些详细信息。

## 支持的身份 {#supported-identities}

Medallia支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址 | 当您要发送电子邮件邀请调查时，请选择电子邮件目标身份。 当一个用户档案与多个电子邮件地址关联时，Medallia将仅触发对第一封电子邮件的邀请。 |
| phone | 以E.164格式散列的电话号码 | 当您要发送基于短信的调查时，请选择电话目标身份。 电话号码必须是E.164格式，其中包括加号(+)、国际国家/地区呼叫代码、本地区号和电话号码。 例如：(+)（国家代码）（区号）（电话号码）。 当配置文件与多个电话号码关联时，Medallia将仅触发第一个电话号码的邀请。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有新限定成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL OAuth令牌端点URL]**：通常采用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL 客户端ID]**：从Medallia投放团队获取。
* **[!UICONTROL 客户端密码]**：从Medallia投放团队获取。

![显示此目标的身份验证屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL API网关URL]**：从Medallia投放团队获取。 通常采用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL 导入API名称]**：从Medallia投放团队获取。 要在此连接中使用的Medallia Import API（也称为Web馈送）的名称。 您可以将不同的受众激活到不同的导入API，以触发不同的调查程序。

![显示此目标的目标详细信息屏幕的图像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射属性和身份 {#map}

必须根据用例映射以下目标身份命名空间：
* 对于基于电子邮件的调查， **电子邮件** 必须使用映射为目标字段 **目标字段** > **选择身份命名空间** > **电子邮件**
* 对于基于短信的调查， **电话** 必须使用映射为目标字段 **目标字段** > **选择身份命名空间** > **电话**. 电话号码必须是E.164格式，其中包括加号(+)、国际国家/地区呼叫代码、本地区号和电话号码

强烈建议您同时映射其他目标自定义属性以创建个性化调查，并将有关客户的附加信息附加到调查记录：

* 个性化调查通常按名称与客户交谈
   * 将客户的名字映射到 **目标字段** > **选择自定义属性** > **属性名称** > **名字**
   * 将客户的姓氏映射到 **目标字段** > **选择自定义属性** > **属性名称** > **姓氏**
* 根据需要为任何其他目标自定义属性添加映射

![显示身份和属性映射示例的图像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 将确切信息分享给您的Medallia交付团队 **属性名称** 对于您使用的每个目标自定义属性 **目标字段** > **选择自定义属性** > **属性名称**. 您可能希望直接共享映射页面的屏幕快照。

## 导出的数据 {#exported-data}

将区段激活到目标后，请通知您的Medallia交付团队，该团队将能够验证从Adobe Experience Platform导出到Medallia的数据。 请注意，调查只能在成功的数据验证后在Medallia中激活；在此之前，数据将导出到Medallia，但不会向客户触发调查。

下面提供了一个导出数据的JSON示例，该示例使用了上文中屏幕快照中的示例映射。 **映射属性和身份** 部分：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).
