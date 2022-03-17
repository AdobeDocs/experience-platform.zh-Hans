---
keywords: 飞艇属性；飞艇目的地
title: 飞艇属性连接
description: 将Adobe受众数据无缝地作为受众属性传递到Airship，以便在Airship中进行定位。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Airship Attributes] 连接 {#airship-attributes-destination}

## 概述 {#overview}

[!DNL Airship] 是领先的客户参与平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全方位消息。

此集成可将Adobe配置文件数据传递到 [!DNL Airship] as [属性](https://docs.airship.com/guides/audience/attributes/) 进行定位或触发。

详细了解 [!DNL Airship]，请参阅 [Airship文档](https://docs.airship.com).

>[!TIP]
>
>此文档页面由 [!DNL Airship] 团队。 如有任何查询或更新请求，请直接联系 [support.airship.com](https://support.airship.com/).

## 先决条件 {#prerequisites}

在将受众区段发送到 [!DNL Airship]，您必须：

* 在 [!DNL Airship] 项目。
* 生成用于身份验证的载体令牌。

>[!TIP]
>
>创建 [!DNL Airship] 帐户通过 [此注册链接](https://go.airship.eu/accounts/register/plan/starter/) 如果您尚未访问，请执行以下操作：

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)和/或身份，具体取决于字段映射。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 启用属性 {#enable-attributes}

Adobe Experience Platform配置文件属性类似于 [!DNL Airship] 属性，并且可以使用此页面下面进一步演示的映射工具，在Platform中轻松地相互映射。

[!DNL Airship] 项目具有多个预定义属性和默认属性。 如果您有自定义属性，则必须在 [!DNL Airship] 第一个。 请参阅 [设置和管理属性](https://docs.airship.com/tutorials/audience/attributes/) 以了解详细信息。

## 生成载体令牌 {#bearer-token}

转到 **[!UICONTROL 设置]** &quot; **[!UICONTROL API和集成]** 在 [飞艇仪表板](https://go.airship.com) 选择 **[!UICONTROL 令牌]** 菜单中。

单击 **[!UICONTROL 创建令牌]**.

为令牌提供用户友好名称(例如“Adobe属性目标”)，然后为角色选择“全部访问”。

单击 **[!UICONTROL 创建令牌]** 并将细节保存为机密。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL Airship Attributes] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

利用在Adobe Experience Platform中收集的用户档案数据，对任何 [!DNL Airship]的渠道。 例如，利用 [!DNL Experience Platform] 配置文件数据，用于在 [!DNL Airship]. 这样，酒店品牌就可以显示每个用户最近的酒店位置的图像。

### 用例#2

利用Adobe Experience Platform中的属性进一步丰富 [!DNL Airship] 配置文件，并将其与SDK或 [!DNL Airship] 预测数据。 例如，零售商可以创建一个具有忠诚度状态和位置数据（来自Platform的属性）的区段，以及 [!DNL Airship] 预计会流失数据，以向生活在内华达州拉斯维加斯的黄金忠诚度状态用户发送极具针对性的消息，并且这些用户很可能会进行转发。

## 连接到目标 {#connect}

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 载体令牌]**:您从 [!DNL Airship] 功能板。
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 域]**:选择美国或欧盟的数据中心，具体取决于 [!DNL Airship] 数据中心适用于此目标。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship] 可以在渠道(表示设备实例，如iPhone)或指定用户（将用户的所有设备映射到通用标识符，如客户ID）上设置属性。 如果您的架构中将纯文本（未经过哈希处理）电子邮件地址作为主标识，请在 **[!UICONTROL 源属性]** 并映射到 [!DNL Airship] 右列下的指定用户 **[!UICONTROL Target标识]**，如下所示。

![命名用户映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

对于应映射到渠道（即设备）的标识符，请根据源映射到相应的渠道。 下图显示了如何创建两个映射：

* 将IDFA iOS广告ID添加到 [!DNL Airship] iOS渠道
* Adobe `fullName` 属性 [!DNL Airship] “全名”属性

>[!NOTE]
>
>使用 [!DNL Airship] 功能板。

**映射标识**

选择源字段：

![连接到Airship属性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

选择目标字段：

![连接到Airship属性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**映射属性**

选择源属性：

![选择源字段](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

选择目标属性：

![选择目标字段](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

验证映射：

![渠道映射](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](../../../data-governance/home.md).
