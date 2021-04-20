---
keywords: Experience Platform；主页；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: 创建用于捕获IAB TCF 2.0同意数据的数据集
topic: privacy events
description: 此文档提供了设置两个必需数据集以收集IAB TCF 2.0同意数据的步骤。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---


# 创建用于捕获IAB TCF 2.0同意数据的数据集

为了使Adobe Experience Platform能够按照IAB [!DNL Transparency & Consent Framework](TCF)2.0处理客户同意数据，必须将这些数据发送到模式包含TCF 2.0同意字段的数据集。

具体而言，捕获TCF 2.0同意数据需要两个数据集：

* 基于[!DNL XDM Individual Profile]类的数据集，在[!DNL Real-time Customer Profile]中启用。
* 基于[!DNL XDM ExperienceEvent]类的数据集。

本文档提供了设置这两个数据集以收集IAB TCF 2.0同意数据的步骤。 有关为TCF 2.0配置平台数据操作的完整工作流程的概述，请参阅[IAB TCF 2.0规范概述](./overview.md)。

## 先决条件

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成的基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):使您能够跨设备和系统从不同的数据源连接客户身份。
   * [身份命名空间](../../../../identity-service/namespaces.md):客户身份命名空间必须根据由Identity Service识别的特定身份数据提供。
* [实时客户用户档案](../../../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。[!DNL Real-time Customer Profile] 从Data Lake中提取数据，并将客户用户档案保留在其自己的单独数据存储中。

## [!UICONTROL 隐私详] 细信息混合结构  {#structure}

[!UICONTROL 隐私详细信息] mixin提供TCF 2.0支持所需的客户同意字段。 此混音有两种版本：一个与[!DNL XDM Individual Profile]类兼容，另一个与[!DNL XDM ExperienceEvent]类兼容。

以下各节说明了每个混合的结构，包括在摄取期间他们期望的数据。

### 用户档案混音{#profile-mixin}

对于基于[!DNL XDM Individual Profile]的模式,[!UICONTROL 隐私详细信息] mixin提供单个映射类型字段`xdm:identityPrivacyInfo`，该字段将客户身份映射到其TCF同意偏好。 以下JSON是`xdm:identityPrivacyInfo`在数据获取时所需的数据类型的示例：

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

如示例所示，`xdm:identityPrivacyInfo`的每个根级别键都与由Identity Service识别的身份命名空间相对应。 反过来，每个命名空间属性必须至少有一个子属性，其密钥与该命名空间的相应标识值相匹配。 在此示例中，客户的Experience CloudID(`ECID`)值为`13782522493631189`。

>[!NOTE]
>
>虽然上例使用单个命名空间/值对来表示客户的身份，但您可以为其他命名空间添加附加键，并且每个命名空间可以具有多个身份值，每个身份值都具有各自的TCF同意首选项集。

标识值对象中是单个字段，`xdm:identityIABConsent`。 此对象捕获指定身份命名空间和值的客户的TCF同意值。 此字段中包含的子属性如下所示：

| 属性 | 描述 |
| --- | --- |
| `xdm:consentTimestamp` | TCF同意值更改时的[ISO 8601](https://www.ietf.org/rfc/rfc3339.txt)时间戳。 |
| `xdm:consentString` | 包含客户更新的同意数据和其他上下文信息的对象。 请参阅[同意字符串属性](#consent-string)中的部分，了解此对象的必需子属性。 |

### 事件混音{#event-mixin}

对于基于[!DNL XDM ExperienceEvent]的模式,[!UICONTROL 隐私详细信息]混音提供单个阵列类型字段：`xdm:consentStrings`。 此数组中的每个项都必须是包含TCF同意字符串必需属性的对象，与用户档案混音中的`xdm:consentString`字段类似。 有关这些子属性的详细信息，请参阅[下一节](#consent-string)。

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### 同意字符串属性{#consent-string}

[!UICONTROL 隐私详细信息]混音的两个版本至少需要一个对象来捕获描述客户的TCF同意字符串的必要字段。 这些属性的说明如下：

| 属性 | 描述 |
| --- | --- |
| `xdm:consentStandard` | 数据适用的同意框架。 对于TCF规范，值必须为`IAB TCF`。 |
| `xdm:consentStandardVersion` | 由`xdm:consentStandard`指示的同意框架的版本号。 对于TCF 2.0规范，值必须为`2.0`。 |
| `xdm:consentStringValue` | 由同意管理平台(CMP)基于客户的选定设置生成的同意字符串。 |
| `xdm:gdprApplies` | 一个布尔值，指示GDPR是否适用于此客户。 必须将值设置为`true`，才能执行TCF 2.0。 如果未包括，则默认为`true`。 |
| `xdm:containsPersonalData` | 一个布尔值，指示同意更新是否包含个人数据。 如果未包括，则默认为`false`。 |

## 创建客户同意模式{#create-schemas}

为了创建捕获同意数据的数据集，您必须首先创建XDM模式以基于这些数据集。

在平台UI中，在左侧导航中选择&#x200B;**[!UICONTROL 模式]**&#x200B;以打开[!UICONTROL 模式]工作区。 在此处，请按照以下部分中的步骤创建每个必需的模式。

>[!NOTE]
>
>如果您有要用来捕获同意数据的现有XDM模式，则可以编辑这些模式，而不是创建新数据。 但是，如果现有模式已启用在实时客户用户档案中使用，则其主要标识不能是禁止在基于兴趣的广告（如电子邮件地址）中使用的直接可识别字段。 如果您不确定哪些字段受限，请咨询您的法律顾问。
>
>此外，编辑现有模式时，只能进行附加（不中断）更改。 有关详细信息，请参见[模式演化原则](../../../../xdm/schema/composition.md#evolution)一节。

### 创建基于记录的同意模式{#profile-schema}

在&#x200B;**[!UICONTROL 模式]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 创建模式]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL XDM单个用户档案]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

出现[!DNL Schema Editor]，显示画布中模式的结构。 使用右边栏为模式提供名称和说明，然后在画布左侧的&#x200B;**[!UICONTROL Mixins]**&#x200B;部分下选择&#x200B;**[!UICONTROL 添加]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-profile.png)

将显示&#x200B;**[!UICONTROL 添加mixin]**&#x200B;对话框。 从此处，从列表中选择&#x200B;**[!UICONTROL 隐私详细信息]**。 您可以选择使用搜索栏缩小结果范围，以便更轻松地定位混音。 选择混音后，选择&#x200B;**[!UICONTROL 添加混音]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

画布将重新出现，显示`identityPrivacyInfo`字段已添加到模式结构。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

在此处，重复上述步骤，向模式添加以下附加混音：

* [!UICONTROL IdentityMap]
* [!UICONTROL 用于用户档案的数据捕获区域]
* [!UICONTROL 人口统计详细信息]
* [!UICONTROL 个人联系人详细信息]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-mixins.png)

如果您正在编辑已启用在[!DNL Real-time Customer Profile]中使用的现有模式，请选择&#x200B;**[!UICONTROL 保存]**&#x200B;以确认您的更改，然后跳到[上的“根据您的同意模式](#dataset)创建数据集”部分。 如果要创建新模式，请继续执行下面子部分中概述的步骤。

#### 启用模式以在[!DNL Real-time Customer Profile]中使用

为了使平台能够将其收到的同意数据与特定客户用户档案关联，必须启用同意模式才能在[!DNL Real-time Customer Profile]中使用。

>[!NOTE]
>
>本节中显示的示例模式使用其`identityMap`字段作为主标识。 如果您希望将另一个字段设置为主要标识，请确保您使用的是Cookie ID等间接标识符，而不是基于兴趣的广告（如电子邮件地址）中禁止使用的直接可识别字段。 如果您不确定哪些字段受限，请咨询您的法律顾问。
>
>有关如何为模式设置主标识字段的步骤，请参阅[模式创建教程](../../../../xdm/tutorials/create-schema-ui.md#identity-field)。

要启用[!DNL Profile]的模式，请在左边栏中选择模式的名称，以打开右边栏中的&#x200B;**[!UICONTROL 模式属性]**&#x200B;对话框。 从此处，选择&#x200B;**[!UICONTROL 用户档案]**&#x200B;切换按钮。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

将出现一个快显窗口，指示缺少主标识。 选中此复选框以使用替代主标识，因为主标识将包含在`identityMap`字段中。

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

最后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以确认更改。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 创建基于时间序列的同意模式{#event-schema}

在&#x200B;**[!UICONTROL 模式]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 创建模式]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL XDM ExperienceEvent]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

出现[!DNL Schema Editor]，显示画布中模式的结构。 使用右边栏为模式提供名称和说明，然后在画布左侧的&#x200B;**[!UICONTROL Mixins]**&#x200B;部分下选择&#x200B;**[!UICONTROL 添加]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-event.png)

将显示&#x200B;**[!UICONTROL 添加mixin]**&#x200B;对话框。 从此处，从列表中选择&#x200B;**[!UICONTROL 隐私详细信息]**。 您可以选择使用搜索栏缩小结果范围，以便更轻松地定位混音。 选择混音后，选择&#x200B;**[!UICONTROL 添加混音]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

画布将重新出现，显示`consentStrings`数组已添加到模式结构。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

在此处，重复上述步骤，向模式添加以下附加混音：

* [!UICONTROL IdentityMap]
* [!UICONTROL 环境详细信息]
* [!UICONTROL Web详细信息]
* [!UICONTROL 实施详细信息]

添加混音后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;即可完成。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-mixins.png)

## 根据您的同意模式{#datasets}创建数据集

对于上述每个必需模式，您必须创建一个数据集，以最终摄取客户同意数据。 必须为[!DNL Real-time Customer Profile]启用基于记录模式的模式集，而基于时间序列数据集&#x200B;**的数据集不应**&#x200B;启用[!DNL Profile]。

首先，在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**，然后选择右上角的&#x200B;**[!UICONTROL 创建数据集]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

在下一页，选择&#x200B;**[!UICONTROL 从模式]**&#x200B;创建数据集。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

将显示&#x200B;**[!UICONTROL 从模式]**&#x200B;创建模式集工作流，从&#x200B;**[!UICONTROL 选择数据集]**&#x200B;步骤开始。 在提供的列表中，找到您之前创建的同意模式之一。 您可以选择使用搜索栏缩小结果范围并更轻松地定位模式。 选择所需模式旁的单选按钮，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

出现&#x200B;**[!UICONTROL 配置数据集]**&#x200B;步骤。 在选择&#x200B;**[!UICONTROL 完成]**&#x200B;之前，为数据集提供唯一、易于识别的名称和说明。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

此时将显示新创建数据集的详细信息页面。 如果数据集基于您的时间序列模式，则该过程已完成。 如果数据集基于您的记录模式，则该过程的最后一步是启用数据集以在[!DNL Real-time Customer Profile]中使用。

在右侧边栏中，选择&#x200B;**[!UICONTROL 用户档案]**&#x200B;切换键，然后在确认窗口中选择&#x200B;**[!UICONTROL 启用]**&#x200B;以启用[!DNL Profile]模式。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

再次按照上述步骤创建符合TCF 2.0规范的其他必需数据集。

## 后续步骤

通过本教程，您创建了两个数据集，现在可用于收集客户同意数据：

* 支持在实时客户用户档案中使用的基于记录的数据集。
* 未为[!DNL Profile]启用的基于时间序列的数据集。

您现在可以返回[IAB TCF 2.0概述](./overview.md#merge-policies)以继续配置Platform以实现TCF 2.0规范的过程。