---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 配置数据集以捕获同意和首选项数据
topic-legacy: getting started
description: 了解如何配置体验数据模型(XDM)架构和数据集，以在Adobe Experience Platform中捕获同意和首选项数据。
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 配置数据集以捕获同意和首选项数据

为了让Adobe Experience Platform处理您的客户同意/首选项数据，必须将该数据发送到架构中包含与同意和其他权限相关字段的数据集。 具体而言，此数据集必须基于 [!DNL XDM Individual Profile] 类，并启用以在中使用 [!DNL Real-Time Customer Profile].

本文档提供了配置数据集以处理Experience Platform中的同意数据的步骤。 有关在平台中处理同意/首选项数据的完整工作流程的概述，请参阅 [同意处理概述](./overview.md).

>[!IMPORTANT]
>
>本指南中的示例使用一组标准化字段来表示客户同意值，这些字段由 [[!UICONTROL 同意和首选项详细信息] 架构字段组](../../../../xdm/field-groups/profile/consents.md). 这些字段的结构旨在提供一个高效的数据模型，以涵盖许多常见的同意收集用例。
>
>但是，您也可以定义自己的字段组，以根据自己的数据模型表示同意。 根据以下选项，请咨询您的法律团队，以获得符合您业务需求的同意数据模型的批准：
>
>* 标准化的同意字段组
>* 由贵组织创建的自定义同意字段组
>* 自定义同意字段组提供的标准化同意字段组和其他字段的组合


## 先决条件

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块。
* [实时客户资料](../../../../profile/home.md):将来自不同来源的客户数据整合到一个完整、统一的视图中，同时为每个客户交互提供一个加盖时间戳的可操作帐户。

>[!IMPORTANT]
>
>本教程假定您知道 [!DNL Profile] 平台中用于捕获客户属性信息的架构。 无论您使用何种方法收集同意数据，此模式都必须 [为实时客户用户档案启用](../../../../xdm/ui/resources/schemas.md#profile). 此外，架构的主标识不能是禁止在基于兴趣的广告（如电子邮件地址）中使用的直接可识别字段。 如果您不确定哪些字段受到限制，请咨询您的法律顾问。

## [!UICONTROL 同意和首选项详细信息] 字段组结构 {#structure}

的 [!UICONTROL 同意和首选项详细信息] 字段组为架构提供标准化的同意字段。 目前，此字段组仅与基于 [!DNL XDM Individual Profile] 类。

字段组提供单个对象类型字段， `consents`，其子属性将捕获一组标准化同意字段。 以下JSON是数据类型的示例 `consents` 在摄取数据时预期：

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
>有关 `consents`，请参阅 [[!UICONTROL 同意和首选项详细信息] 字段组](../../../../xdm/field-groups/profile/consents.md).

## 将必填字段组添加到 [!DNL Profile] 模式 {#add-field-group}

要使用Adobe标准收集同意数据，您必须具有启用了用户档案的架构，该架构包含以下两个字段组：

* [!UICONTROL 同意和首选项详细信息]
* [!UICONTROL IdentityMap] （使用Platform Web或Mobile SDK发送同意信号时需要使用此参数）

在平台UI中，选择 **[!UICONTROL 模式]** 在左侧导航中，选择 **[!UICONTROL 浏览]** 选项卡，以显示现有架构的列表。 从此处，选择 [!DNL Profile] — 启用了要向其添加同意字段的架构。 此部分中的屏幕截图使用 [模式创建教程](../../../../xdm/tutorials/create-schema-ui.md) 例如。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>您可以使用工作区的搜索和筛选功能来帮助更轻松地查找架构。 请参阅 [浏览XDM资源](../../../../xdm/ui/explore.md) 以了解更多信息。

的 [!DNL Schema Editor] ，显示画布中架构的结构。 在画布的左侧，选择 **[!UICONTROL 添加]** 下 **[!UICONTROL 字段组]** 中。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

的 **[!UICONTROL 添加字段组]** 对话框。 从此处选择 **[!UICONTROL 同意和首选项详细信息]** 列表。 您可以选择使用搜索栏来缩小结果范围，以便更轻松地找到字段组。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

接下来，查找 **[!UICONTROL IdentityMap]** 字段组，并将其选中。 在右边栏中列出两个字段组后，选择 **[!UICONTROL 添加字段组]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

画布将重新出现，显示 `consents` 和 `identityMap` 字段已添加到架构结构中。 如果您需要标准字段组未捕获的其他同意和首选项字段，请参阅 [向架构添加自定义同意和首选项字段](#custom-consent). 否则，请选择 **[!UICONTROL 保存]** 完成对架构的更改。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>如果要创建新架构，或编辑尚未为配置文件启用的现有架构，则必须 [为配置文件启用架构](../../../../xdm/ui/resources/schemas.md#profile) 保存之前。

如果您编辑的架构由 [!UICONTROL 配置文件数据集] 在您的Platform Web SDK数据流中指定，该数据集现在将包含新的同意字段。 您现在可以返回到 [同意处理指南](./overview.md#merge-policies) 继续配置Experience Platform以处理同意数据的过程。 如果您尚未为此架构创建数据集，请按照下一部分中的步骤操作。

## 根据您的同意架构创建数据集 {#dataset}

在创建包含同意字段的架构后，您必须创建一个数据集，以最终摄取客户的同意数据。 必须为 [!DNL Real-Time Customer Profile].

要开始，请选择 **[!UICONTROL 数据集]** 在左侧导航中，选择 **[!UICONTROL 创建数据集]** 中。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一页，选择 **[!UICONTROL 从架构创建数据集]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

的 **[!UICONTROL 从架构创建数据集]** 此时会显示工作流，从 **[!UICONTROL 选择架构]** 中。 在提供的列表中，找到您之前创建的同意架构之一。 您可以选择使用搜索栏来缩小结果范围并更轻松地查找架构。 选择所需架构旁边的单选按钮，然后选择 **[!UICONTROL 下一个]** 继续。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

的 **[!UICONTROL 配置数据集]** 中。 在选择之前，为数据集提供唯一且易于识别的名称和描述 **[!UICONTROL 完成]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

此时会显示新创建数据集的详细信息页面。 如果数据集基于您的时间系列架构，则该过程会完成。 如果数据集基于您的记录架构，则此过程的最后一步是启用该数据集以在中使用 [!DNL Real-Time Customer Profile].

在右边栏中，选择 **[!UICONTROL 用户档案]** 切换。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最后，选择 **[!UICONTROL 启用]** 在确认弹出窗口中，为 [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

数据集现已保存并启用，可在中使用 [!DNL Profile]. 如果您计划使用Platform Web SDK将同意数据发送到用户档案，则必须选择此数据集作为 [!UICONTROL 配置文件数据集] 设置 [数据流](../../../../edge/datastreams/overview.md).

## 后续步骤

通过阅读本教程，您已将同意字段添加到 [!DNL Profile] — 已启用架构，其数据集将用于使用Platform Web SDK或直接摄取XDM来摄取同意数据。

您现在可以返回到 [同意处理概述](./overview.md#merge-policies) 继续配置Experience Platform以处理同意数据。

## 附录

以下部分包含有关创建数据集以摄取客户同意和首选项数据的其他信息。

### 在架构中添加自定义同意和首选项字段 {#custom-consent}

如果您需要捕获标准所表示的同意信号以外的其他同意信号 [!UICONTROL 同意和首选项详细信息] 字段组中，您可以使用自定义XDM组件来增强您的同意架构，以满足您的特定业务需求。 本节概述了如何自定义同意模式以将这些信号摄取到用户档案的基本原则。

>[!IMPORTANT]
>
>平台Web SDK和移动SDK不支持在其同意更改命令中使用自定义字段。 目前，将自定义同意字段摄取到用户档案的唯一方法是 [批量摄取](../../../../ingestion/batch-ingestion/overview.md) 或 [源连接](../../../../sources/home.md).

强烈建议您使用 [!UICONTROL 同意和首选项详细信息] 字段组作为同意数据结构的基线，并根据需要添加其他字段，而不是尝试从头开始创建整个结构。

要向标准字段组的结构添加自定义字段，您必须首先创建自定义字段组。 添加 [!UICONTROL 同意和首选项详细信息] 字段组，选择 **加号(+)** 图标 **[!UICONTROL 字段组]** ，然后选择 **[!UICONTROL 创建新字段组]**. 为字段组提供名称和可选描述，然后选择 **[!UICONTROL 添加字段组]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

的 [!DNL Schema Editor] 在左边栏中选中新的自定义字段组后，将重新显示。 在画布中，将显示用于向架构结构添加自定义字段的控件。 要添加新的同意或首选项字段，请选择 **加号(+)** 图标 `consents` 对象。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

在 `consents` 对象。 由于您将自定义字段添加到标准XDM对象，因此新字段会在与租户ID命名的对象下创建。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在右边栏的 **[!UICONTROL 字段属性]**，提供字段的名称和描述。 选择字段的 **[!UICONTROL 类型]**，则必须在自定义同意或首选项字段中使用相应的标准数据类型：

* [[!UICONTROL 一般同意字段]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 一般营销首选项字段]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 包含订阅的通用营销首选项字段]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 一般个性化首选项字段]](../../../../xdm/data-types/personalization-field.md)

完成后，选择 **[!UICONTROL 应用]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或首选项字段将添加到架构结构中。 请注意， [!UICONTROL 路径] 显示在右边栏中的包含 `_tenantId` 命名空间。 每当您在数据操作中引用此字段的路径时，都必须包含此命名空间。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

按照上述步骤继续添加您需要的同意和首选项字段。 完成后，选择 **[!UICONTROL 保存]** 确认更改。

如果尚未为此架构创建数据集，请继续 [创建数据集](#dataset).
