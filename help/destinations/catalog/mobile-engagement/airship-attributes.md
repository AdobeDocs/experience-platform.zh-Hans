---
keywords: 飞艇属性；飞艇目的地
title: 飞艇属性连接
description: 将Adobe受众数据无缝地作为受众属性传递到Airship，以便在Airship中进行定位。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# [!DNL Airship Attributes] 连接 {#airship-attributes-destination}

## 概述 {#overview}

[!DNL Airship] 是领先的客户参与平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全方位消息。

此集成将Adobe配置文件数据作为[Attributes](https://docs.airship.com/guides/audience/attributes/)传递到[!DNL Airship]中，以进行定位或触发。

要了解有关[!DNL Airship]的更多信息，请参阅[Airship Docs](https://docs.airship.com)。

>[!TIP]
>
>本文档页面由[!DNL Airship]团队创建。 如有任何查询或更新请求，请直接通过[support.airship.com](https://support.airship.com/)联系。

## 先决条件 {#prerequisites}

在将受众区段发送到[!DNL Airship]之前，您必须：

* 在[!DNL Airship]项目中启用属性。
* 生成用于身份验证的载体令牌。

>[!TIP]
>
>通过[此注册链接](https://go.airship.eu/accounts/register/plan/starter/)创建[!DNL Airship]帐户（如果尚未创建）。

## 启用属性 {#enable-attributes}

Adobe Experience Platform配置文件属性与[!DNL Airship]属性类似，并且可以使用本页下面进一步演示的映射工具，在Platform中轻松地相互映射。

[!DNL Airship] 项目具有多个预定义属性和默认属性。如果您有自定义属性，则必须先在[!DNL Airship]中定义该属性。 有关详细信息，请参阅[设置和管理属性](https://docs.airship.com/tutorials/audience/attributes/)。

## 生成载体令牌 {#bearer-token}

转到[Airship仪表板](https://go.airship.com)中的&#x200B;**[!UICONTROL Settings]**&quot; **[!UICONTROL API和集成]**，然后在左侧菜单中选择&#x200B;**[!UICONTROL 令牌]**。

单击&#x200B;**[!UICONTROL 创建令牌]**。

为令牌提供用户友好名称(例如“Adobe属性目标”)，然后为角色选择“全部访问”。

单击&#x200B;**[!UICONTROL 创建令牌]**&#x200B;并将详细信息另存为机密。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用[!DNL Airship Attributes]目标，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。

### 用例#1

利用Adobe Experience Platform中收集的用户档案数据，对任何[!DNL Airship]渠道中的消息和丰富内容进行个性化。 例如，利用[!DNL Experience Platform]配置文件数据在[!DNL Airship]中设置位置属性。 这样，酒店品牌就可以显示每个用户最近的酒店位置的图像。

### 用例#2

利用Adobe Experience Platform中的属性进一步丰富[!DNL Airship]配置文件，并将其与SDK或[!DNL Airship]预测数据相结合。 例如，零售商可以创建一个具有忠诚度状态和位置数据（来自Platform的属性）的区段，该区段预测会流失数据，从而向生活在内华达州拉斯维加斯的黄金忠诚度状态用户发送极具针对性的消息，这些用户很有可能会进行批量处理。[!DNL Airship]

## 连接到目标 {#connect}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 载体令牌]**:您从功能板生成的载体令 [!DNL Airship] 牌。
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 域]**:选择美国或欧盟的数据中心，具体取决于哪 [!DNL Airship] 个数据中心适用于此目标。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship] 可以在渠道（表示设备实例，如iPhone）或指定用户（将用户的所有设备映射到通用标识符，如客户ID）上设置属性。如果您的架构中将纯文本（未经过哈希处理）的电子邮件地址作为主标识，请选择&#x200B;**[!UICONTROL 源属性]**&#x200B;中的email字段，然后映射到&#x200B;**[!UICONTROL 目标标识]**&#x200B;下右列中的[!DNL Airship]指定用户，如下所示。

![命名用户映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

对于应映射到渠道（即设备）的标识符，请根据源映射到相应的渠道。 下图显示了如何创建两个映射：

* 将IDFA iOS广告ID发送到[!DNL Airship] iOS渠道
* Adobe`fullName`属性的“全名”属性[!DNL Airship]

>[!NOTE]
>
>使用[!DNL Airship]功能板中显示的用户友好名称，为属性映射选择目标字段。

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

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](../../../data-governance/home.md)。
