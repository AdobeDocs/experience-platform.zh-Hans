---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 配置数据集以捕获同意和偏好设置数据
description: 了解如何在Adobe Experience Platform中配置体验数据模型(XDM)架构和数据集以捕获同意和偏好设置数据。
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 配置数据集以捕获同意和偏好设置数据

为了让Adobe Experience Platform处理您的客户同意/偏好设置数据，必须将该数据发送到数据集，其架构包含与同意和其他权限相关的字段。 具体而言，此数据集必须基于 [!DNL XDM Individual Profile] 类，并启用以用于 [!DNL Real-Time Customer Profile].

本文档提供了配置数据集以处理Experience Platform中的同意数据的步骤。 有关Platform中处理同意/偏好设置数据的完整工作流的概述，请参阅 [同意处理概述](./overview.md).

>[!IMPORTANT]
>
>本指南中的示例使用一组标准化的字段来表示客户同意值，具体值由 [[!UICONTROL 同意和偏好设置详细信息] 架构字段组](../../../../xdm/field-groups/profile/consents.md). 这些字段的结构旨在提供一个高效的数据模型，以涵盖许多常见的同意收集用例。
>
>但是，您也可以根据自己的数据模型定义自己的字段组来表示同意。 请咨询您的法律团队，以根据以下选项获得批准符合您业务需求的同意数据模型：
>
>* 标准同意字段组
>* 您的组织创建的自定义同意字段组
>* 标准化同意字段组和自定义同意字段组提供的其他字段的组合


## 先决条件

本教程需要深入了解Adobe Experience Platform的以下组件：

* [体验数据模型(XDM)](../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块。
* [Real-time Customer Profile](../../../../profile/home.md)：将来自不同来源的客户数据整合到一个完整、统一的视图中，同时为每个客户交互提供一个带有时间戳的可操作帐户。

>[!IMPORTANT]
>
>本教程假设您知道 [!DNL Profile] Platform中要用于捕获客户属性信息的架构。 无论您使用何种方法来收集同意数据，此架构必须 [已为实时客户配置文件启用](../../../../xdm/ui/resources/schemas.md#profile). 此外，架构的主要身份不能是禁止在基于兴趣的广告（如电子邮件地址）中使用的直接可识别的字段。 如果您不确定哪些字段受限，请咨询您的法律顾问。

## [!UICONTROL 同意和偏好设置详细信息] 字段组结构 {#structure}

此 [!UICONTROL 同意和偏好设置详细信息] 字段组为架构提供标准化的同意字段。 目前，此字段组仅与基于 [!DNL XDM Individual Profile] 类。

字段组提供单个对象类型字段， `consents`，其子属性捕获一组标准化的同意字段。 以下JSON是此类数据的示例 `consents` 数据引入时预期：

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>有关中子属性的结构和含义的更多信息 `consents`，请参阅 [[!UICONTROL 同意和偏好设置详细信息] 字段组](../../../../xdm/field-groups/profile/consents.md).

## 将必填字段组添加到您的 [!DNL Profile] 架构 {#add-field-group}

要使用Adobe标准收集同意数据，您必须具有启用配置文件的架构，该架构包含以下两个字段组：

* [!UICONTROL 同意和偏好设置详细信息]
* [!UICONTROL Identitymap] （如果使用Platform Web或Mobile SDK发送同意信号，则此为必填字段）

在Platform UI中，选择 **[!UICONTROL 架构]** 在左侧导航中，然后选择 **[!UICONTROL 浏览]** 选项卡以显示现有架构的列表。 从此处，选择 [!DNL Profile] — 启用的要向其添加同意字段的架构。 此部分中的屏幕截图使用中内置的“忠诚会员”模式 [模式创建教程](../../../../xdm/tutorials/create-schema-ui.md) 例如。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找架构。 请参阅指南，网址为 [探索XDM资源](../../../../xdm/ui/explore.md) 了解更多信息。

此 [!DNL Schema Editor] 显示，显示画布中的架构结构。 在画布的左侧，选择 **[!UICONTROL 添加]** 在 **[!UICONTROL 字段组]** 部分。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

此 **[!UICONTROL 添加字段组]** 对话框。 从此处选择 **[!UICONTROL 同意和偏好设置详细信息]** 从名单上。 您可以选择使用搜索栏缩小结果范围，以便更轻松地找到字段组。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

接下来，查找 **[!UICONTROL Identitymap]** 字段组并选择它。 一旦两个字段组都列在右边栏中，请选择 **[!UICONTROL 添加字段组]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

画布会重新出现，显示 `consents` 和 `identityMap` 字段已添加到架构结构。 如果您需要标准字段组未捕获的其他同意和偏好设置字段，请参阅 [将自定义同意和偏好设置字段添加到架构](#custom-consent). 否则，选择 **[!UICONTROL 保存]** 以完成对架构的更改。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>如果要创建新架构，或编辑尚未为配置文件启用的现有架构，您必须 [为配置文件启用架构](../../../../xdm/ui/resources/schemas.md#profile) 保存之前。

如果您编辑的架构由 [!UICONTROL 配置文件数据集] 在Platform Web SDK数据流中指定，该数据集现在将包括新的同意字段。 您现在可以返回到 [同意处理指南](./overview.md#merge-policies) 继续配置Experience Platform以处理同意数据的过程。 如果尚未为此架构创建数据集，请按照下一节中的步骤操作。

## 根据您的同意模式创建数据集 {#dataset}

创建包含同意字段的架构后，您必须创建一个最终摄取客户同意数据的数据集。 必须为以下项启用此数据集 [!DNL Real-Time Customer Profile].

要开始，请选择 **[!UICONTROL 数据集]** 在左侧导航中，然后选择 **[!UICONTROL 创建数据集]** 在右上角。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一页上，选择 **[!UICONTROL 从架构创建数据集]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

此 **[!UICONTROL 从架构创建数据集]** 此时将显示工作流，从 **[!UICONTROL 选择架构]** 步骤。 在提供的列表中，找到您之前创建的同意架构之一。 您可以选择使用搜索栏缩小结果范围并更轻松地找到架构。 选择所需模式旁边的单选按钮，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

此 **[!UICONTROL 配置数据集]** 步骤。 在选择之前，为数据集提供唯一、易于识别的名称和描述 **[!UICONTROL 完成]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

此时将显示新创建的数据集的详细信息页面。 如果数据集基于您的时间序列架构，则流程已完成。 如果数据集基于您的记录架构，则该过程的最后一步是启用数据集以便用于 [!DNL Real-Time Customer Profile].

在右边栏中，选择 **[!UICONTROL 个人资料]** 切换。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最后，选择 **[!UICONTROL 启用]** 在确认弹出框中启用架构 [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

数据集现已保存并启用，以供使用 [!DNL Profile]. 如果您计划使用Platform Web SDK将同意数据发送到用户档案，则必须选择此数据集作为 [!UICONTROL 配置文件数据集] 设置时 [数据流](../../../../edge/datastreams/overview.md).

## 后续步骤

按照本教程，您已向添加同意字段 [!DNL Profile] — 支持的架构，其数据集将用于通过Platform Web SDK或直接XDM摄取来摄取同意数据。

您现在可以返回到 [同意处理概述](./overview.md#merge-policies) 以继续配置Experience Platform以处理同意数据。

## 附录

以下部分包含有关创建数据集以摄取客户同意和偏好设置数据的其他信息。

### 将自定义同意和偏好设置字段添加到架构 {#custom-consent}

如果您需要捕获标准所表示同意信号以外的其他同意信号 [!UICONTROL 同意和偏好设置详细信息] 字段组，则可以使用自定义XDM组件来增强同意模式，以满足您的特定业务需求。 此部分概述如何自定义同意模式的基本原则，以便将这些信号摄取到配置文件中。

>[!IMPORTANT]
>
>Platform Web和Mobile SDK在其consent-change命令中不支持自定义字段。 目前，将自定义同意字段摄取到用户档案的唯一方法是通过 [批量摄取](../../../../ingestion/batch-ingestion/overview.md) 或 [源连接](../../../../sources/home.md).

强烈建议您使用 [!UICONTROL 同意和偏好设置详细信息] 字段组作为同意数据结构的基线，并根据需要添加其他字段，而不是尝试从头开始创建整个结构。

要将自定义字段添加到标准字段组的结构，您必须首先创建自定义字段组。 添加 [!UICONTROL 同意和偏好设置详细信息] 字段组，选择 **加(+)** 中的图标 **[!UICONTROL 字段组]** 部分，然后选择 **[!UICONTROL 创建新字段组]**. 为字段组提供名称和可选描述，然后选择 **[!UICONTROL 添加字段组]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

此 [!DNL Schema Editor] 重新显示，并在左边栏中选择新的自定义字段组。 在画布中显示允许您向架构结构添加自定义字段的控件。 要添加新的同意或偏好设置字段，请选择 **加(+)** 图标 `consents` 对象。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

新字段随即会显示在 `consents` 对象。 由于您将自定义字段添加到标准XDM对象，因此会在命名为租户ID的对象下创建新字段。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在右边栏中，位于 **[!UICONTROL 字段属性]**，提供字段的名称和描述。 选择字段的 **[!UICONTROL 类型]**，则必须对自定义同意或首选项字段使用相应的标准数据类型：

* [[!UICONTROL 通用同意字段]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 通用营销偏好设置字段]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 具有订阅的通用营销偏好设置字段]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 通用个性化偏好设置字段]](../../../../xdm/data-types/personalization-field.md)

完成后，选择 **[!UICONTROL 应用]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或偏好设置字段会添加到架构结构中。 请注意 [!UICONTROL 路径] 右侧边栏中显示的 `_tenantId` 命名空间。 每当您在数据操作中引用此字段的路径时，都必须包含此命名空间。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

按照上述步骤继续添加您需要的同意和偏好设置字段。 完成后，选择 **[!UICONTROL 保存]** 以确认更改。

如果尚未为此架构创建数据集，请继续上的部分 [创建数据集](#dataset).
