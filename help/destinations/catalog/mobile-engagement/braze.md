---
keywords: 移动设备；布雷；报文传送；
title: Braze连接
description: Braze是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且令人难忘的体验。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---

# （测试版）[!DNL Braze]连接

>[!IMPORTANT]
>
>Adobe Experience Platform中的Braze目标当前为测试版。 文档和功能可能会发生变化。

## 概述 {#overview}

[!DNL Braze]目标可帮助您将用户档案数据发送到[!DNL Braze]。

[!DNL Braze] 是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且难忘的体验。

要将用户档案数据发送到[!DNL Braze]，您必须先连接到目标。

## 目标详情 {#specifics}

请注意特定于[!DNL Braze]目标的以下详细信息：

* [!DNL Adobe Experience Platform] 区段将导出到 [!DNL Braze] 属性下 `AdobeExperiencePlatformSegments` 的。

>[!NOTE]
>
>请记住，向[!DNL Braze]发送其他自定义属性可能会导致[!DNL Braze]数据点使用量增加。 在发送其他自定义属性之前，请咨询您的[!DNL Braze]客户经理。

## 用例 {#use-cases}

作为营销人员，我希望定位移动设备参与目标中的用户，并在[!DNL Adobe Experience Platform]中构建区段。 此外，我希望在[!DNL Adobe Experience Platform]中更新区段和配置文件后，根据[!DNL Adobe Experience Platform]配置文件的属性，尽快向他们提供个性化体验。

## 支持的身份 {#supported-identities}

[!DNL Braze] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| external_id | 支持映射任何标识的自定义[!DNL Braze]标识符。 | 只要您将任何[identity](../../../identity-service/namespaces.md)映射到[!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)，就可以将任何标识发送到[!DNL Braze]目标。 |

## 导出类型 {#export-type}

**[!DNL Profile-based]**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)和/或身份，具体取决于字段映射。[!DNL Adobe Experience Platform] 区段将导出到 [!DNL Braze] 属性下 `AdobeExperiencePlatformSegments` 的。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Braze帐户令牌]**:这是你的 [!DNL Braze] [!DNL API] 钥匙。您可以在此处找到如何获取[!DNL API]键的详细说明：[REST API密钥概述](https://www.braze.com/docs/api/api_key/)。
* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 端点实例]**:请咨询您 [!DNL Braze] 的代表您应使用哪个端点实例。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到目标的说明，请参阅[将配置文件和区段激活到目标](../../ui/activate-destinations.md)。

## 映射注意事项 {#mapping-considerations}

要将受众数据从[!DNL Adobe Experience Platform]正确发送到[!DNL Braze]目标，您需要完成字段映射步骤。

映射包括在[!DNL Platform]帐户的[!DNL Experience Data Model](XDM)架构字段与目标目标中相应的对等字段之间创建链接。

要将XDM字段正确映射到[!DNL Braze]目标字段，请执行以下步骤：

在[!UICONTROL 映射]步骤中，单击&#x200B;**[!UICONTROL 添加新映射]**。

![制作目标添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在[!UICONTROL 源字段]部分中，单击空字段旁边的箭头按钮。

![Braze目标源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在[!UICONTROL 选择源字段]窗口中，您可以选择两类XDM字段：
* [!UICONTROL 选择属性]:使用此选项可将XDM架构中的特定字段映射到 [!DNL Braze] 属性。

![Braze目标映射源属性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 选择身份命名空间]:使用此选项可将身份命名 [!DNL Platform] 空间映射到命名 [!DNL Braze] 空间。

![Braze目标映射源命名空间](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

选择源字段，然后单击&#x200B;**[!UICONTROL 选择]**。

在[!UICONTROL 目标字段]部分中，单击字段右侧的映射图标。

![制作目标映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在[!UICONTROL 选择目标字段]窗口中，您可以选择以下三类目标字段：
* [!UICONTROL 选择属性]:使用此选项可将XDM属性映射到标准 [!DNL Braze] 属性。
* [!UICONTROL 选择身份命名空间]:使用此选项可将身份命名 [!DNL Platform] 空间映射到身 [!DNL Braze] 份命名空间。
* [!UICONTROL 选择自定义属性]:使用此选项可将XDM属性映射到您在帐 [!DNL Braze] 户中定义的自定义 [!DNL Braze] 属性。
* 您还可以使用此选项将现有XDM属性重命名为[!DNL Braze]。 例如，将`lastName` XDM属性映射到[!DNL Braze]中的自定义`Last_Name`属性时，将在[!DNL Braze]中创建`Last_Name`属性（如果不存在），并将`lastName` XDM属性映射到该属性。

![标记目标映射字段](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

选择目标字段，然后单击&#x200B;**[!UICONTROL 选择]**。

此时，您应会在列表中看到字段映射。

![制作目标映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，请重复上述步骤。

## 映射示例 {#mapping-example}

假设您的XDM配置文件架构和[!DNL Braze]实例包含以下属性和标识：

|  | XDM配置文件架构 | [!DNL Braze] 实例 |
|---|---|---|
| 属性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>电话号码</code></li></ul> |
| 标识 | <ul><li>电子邮件</code></li><li>Google广告ID(GAID)</code></li><li>适用于广告商的Apple ID(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正确的映射将如下所示：

![布雷兹目标映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Braze]目标，请检查您的[!DNL Braze]帐户。 [!DNL Adobe Experience Platform] 区段将导出到 [!DNL Braze] 属性下 `AdobeExperiencePlatformSegments` 的。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](../../../data-governance/home.md)。
