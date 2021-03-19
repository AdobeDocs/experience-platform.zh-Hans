---
keywords: 移动；布雷兹；消息；
title: 布雷兹连接
description: Braze是一个全面的客户互动平台，可为客户与他们喜爱的品牌之间提供相关且难忘的体验。
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---


# （测试版）[!DNL Braze]连接

>[!IMPORTANT]
>
>Adobe Experience Platform中的Braze目标当前为测试版。 文档和功能可能会发生变化。

[!DNL Braze]目标可帮助您向[!DNL Braze]发送用户档案数据。

[!DNL Braze] 是一个全面的客户互动平台，可为客户与喜爱的品牌之间提供相关且难忘的体验。

要将用户档案数据发送到[!DNL Braze]，您必须首先连接到目标。

## 目标规范{#destination-specs}

请注意特定于[!DNL Braze]目标的以下详细信息：

* [!DNL Adobe Experience Platform] 段将导出到属 [!DNL Braze] 性的 `AdobeExperiencePlatformSegments` 下方。

>[!NOTE]
>
>请记住，向[!DNL Braze]发送其他自定义属性可能会导致[!DNL Braze]数据点消耗增加。 在发送其他自定义属性之前，请咨询您的[!DNL Braze]客户经理。

## 用例 {#use-cases}

作为营销人员，我希望在移动互动目标中目标用户，[!DNL Adobe Experience Platform]中内置细分。 此外，我希望在[!DNL Adobe Experience Platform]中更新细分和用户档案后，根据[!DNL Adobe Experience Platform]用户档案的属性，立即为他们提供个性化体验。

### 支持的身份{#supported-identities}

[!DNL Google Ad Manager] 支持下表所述身份的激活。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| external_id | 支持任何标识映射的自定义[!DNL Braze]标识符。 | 只要将任何[identity](../../../identity-service/namespaces.md)映射到[!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)，即可将其发送到[!DNL Braze]目标。 |

## 导出类型{#export-type}

**[!DNL Profile-based]**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)和/或身份。[!DNL Adobe Experience Platform] 段将导出到属 [!DNL Braze] 性的 `AdobeExperiencePlatformSegments` 下方。


## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择[!DNL Braze]，然后选择&#x200B;**[!UICONTROL Configure]**。

![配置布雷目标](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。
>
>![激活布雷兹目标](../../assets/catalog/mobile-engagement/braze/activate.png)

在[!UICONTROL Account]步骤中，您需要提供[!DNL Braze]帐户令牌。 这是您的[!DNL Braze] [!DNL API]键。 您可以在以下网址找到如何获取[!DNL API]键的详细说明：[REST API密钥概述](https://www.braze.com/docs/api/api_key/)。 输入标记，然后单击&#x200B;**[!UICONTROL Connect to destination]**。

![布雷兹目标帐户步骤](../../assets/catalog/mobile-engagement/braze/account.png)

单击 **[!UICONTROL Next]**。在[!UICONTROL Authentication]步骤中，您需要输入[!DNL Braze]连接详细信息：
* **[!UICONTROL Name]**:输入一个名称，您将通过该名称在将来识别此目标。
* **[!UICONTROL Description]**:输入说明，帮助您在将来识别此目标。
* **[!UICONTROL Endpoint Instance]**:请咨询您 [!DNL Braze] 的代表您应使用哪个终结点实例。
* **[!UICONTROL Marketing action]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![Braze身份验证步骤](../../assets/catalog/mobile-engagement/braze/authentication.png)

单击 **[!UICONTROL Create destination]**。您的目标现在已创建。 如果您希望稍后激活区段，可单击&#x200B;**[!UICONTROL Save & Exit]**，也可以选择&#x200B;**[!UICONTROL Next]**&#x200B;继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md#select-attributes)。

## 字段映射{#field-mapping}

要将您的受众数据从[!DNL Adobe Experience Platform]正确发送到[!DNL Braze]目标，您需要完成字段映射步骤。

映射包括在[!DNL Platform]帐户中的[!DNL Experience Data Model](XDM)模式字段与目标目标中对应的对等字段之间建立链接。

要正确地将XDM字段映射到[!DNL Braze]目标字段，请执行以下步骤：

在[!UICONTROL Mapping]步骤中，单击&#x200B;**[!UICONTROL Add new mapping]**。

![制作目标添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在[!UICONTROL Source Field]部分，单击空字段旁边的箭头按钮。

![布雷兹目标源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在[!UICONTROL Select source field]窗口中，您可以选择两类别XDM字段：
* [!UICONTROL Select attributes]:使用此选项可将特定字段从XDM模式映射到属 [!DNL Braze] 性。

![布雷兹目标映射源属性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]:使用此选项将标识 [!DNL Platform] 命名空间映射到 [!DNL Braze] 命名空间。

![制作目标映射源命名空间](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

选择源字段，然后单击&#x200B;**[!UICONTROL Select]**。

在[!UICONTROL Target Field]部分，单击字段右侧的映射图标。

![布雷兹目标目标映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在[!UICONTROL Select target field]窗口中，您可以选择以下三类别目标字段：
* [!UICONTROL Select attributes]:使用此选项可将XDM属性映射到标准 [!DNL Braze] 属性。
* [!UICONTROL Select identity namespace]:使用此选项可将身 [!DNL Platform] 份命名空间映射 [!DNL Braze] 到身份命名空间。
* [!UICONTROL Select custom attributes]:使用此选项可将XDM属性映射到您在 [!DNL Braze] 帐户中定义的自定义 [!DNL Braze] 属性。
* 您还可以使用此选项将现有XDM属性重命名为[!DNL Braze]。 例如，将`lastName` XDM属性映射到[!DNL Braze]中的自定义`Last_Name`属性时，将在[!DNL Braze]中创建`Last_Name`属性（如果尚不存在），并将`lastName` XDM属性映射到该属性。

![布雷兹目标目标映射字段](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

选择目标字段，然后单击&#x200B;**[!UICONTROL Select]**。

您现在应该可以在列表中看到字段映射。

![Braze目标映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，请重复上述步骤。

### 示例 {#mapping-example}

假设您的XDM用户档案模式和[!DNL Braze]实例包含以下属性和标识：

|  | XDM用户档案模式 | [!DNL Braze] 实例 |
|---|---|---|
| 属性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| 身份 | <ul><li>电子邮件</code></li><li>Google广告ID(GAID)</code></li><li>广告商的Apple ID(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正确的映射如下所示：

![Braze目标映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 导出的数据{#exported-data}

要验证数据是否已成功导出到[!DNL Braze]目标，请检查您的[!DNL Braze]帐户。 [!DNL Adobe Experience Platform] 段将导出到属 [!DNL Braze] 性的 `AdobeExperiencePlatformSegments` 下方。

## 数据使用和管理{#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](../../../data-governance/home.md)。

