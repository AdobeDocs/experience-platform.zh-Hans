---
solution: Experience Platform
title: 在UI中导出XDM架构
description: 了解如何在Adobe Experience Platform用户界面中将现有架构导出到其他沙盒或组织。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 0f0842c1d14ce42453b09bf97e1f3690448f6e9a
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 在UI中导出XDM架构 {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="复制 JSON 结构"
>abstract="通过将JSON结构复制到剪贴板，为您选择的架构生成导出有效负载。 使用此功能可导出架构库中任何架构的详细信息。 然后，可使用此导出的JSON将架构和任何相关资源导入其他沙盒或组织。 这使得在不同环境之间共享和重用架构变得简单而高效。"

架构库中的所有资源都包含在组织内的特定沙盒中。 在某些情况下，您可能希望在沙盒和组织之间共享Experience Data Model (XDM)资源。

为了满足此需求， [!UICONTROL 架构] Adobe Experience Platform UI中的工作区允许您为架构库中的任何架构生成导出有效负载。 然后，可以在调用架构注册表API中使用此有效负载，将架构（以及所有依赖的资源）导入目标沙盒和组织。

>[!NOTE]
>
>您还可以使用架构注册表API导出架构以外的其他资源，包括类、架构字段组和数据类型。 请参阅 [导出端点指南](../api/export.md) 以了解更多信息。

## 先决条件

虽然Platform UI允许您导出XDM资源，但必须使用架构注册表API将这些资源导入其他沙盒或组织以完成工作流。 请参阅指南，网址为 [架构注册表API快速入门](../api/getting-started.md) 有关所需身份验证标头的重要信息，请参阅本指南。

## 生成导出有效负载 {#generate-export-payload}

可以在Platform UI中从的详细信息面板生成导出负载 [!UICONTROL 浏览] 选项卡，或直接从架构编辑器的架构画布进行访问。

要生成导出有效负载，请选择 **[!UICONTROL 架构]** 在左侧导航中。 在 [!UICONTROL 架构] 在工作区中，选择要导出的架构的行以便在右侧边栏中显示架构详细信息。

>[!TIP]
>
>请参阅指南，网址为 [探索XDM资源](./explore.md) ，以了解有关如何查找您所寻找的XDM资源的详细信息。

接下来，选择 **[!UICONTROL 复制JSON]** 图标(![复制图标](../images/ui/export/icon.png))。

![包含架构行和架构的架构工作区 [!UICONTROL 复制到JSON] 突出显示。](../images/ui/export/copy-json.png)

这会将JSON有效负载复制到剪贴板，该剪贴板是基于架构结构生成的。 对于&quot;[!DNL Loyalty Members]”架构如上所示，会生成以下JSON：

+++选择以展开示例JSON有效负载

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

+++

通过选择还可以复制有效负载 [!UICONTROL 更多] 架构编辑器的右上角。 下拉菜单提供两个选项： [!UICONTROL 复制JSON结构] 和 [!UICONTROL 删除架构].

>[!NOTE]
>
>为配置文件启用某个架构或具有关联的数据集时，无法删除该架构。

![架构编辑器，带有 [!UICONTROL 更多] 和 [!UICONTROL 复制到JSON] 突出显示。](../images/ui/export/schema-editor-copy-json.png)

有效负载采用数组的形式，每个数组项都是一个对象，表示要导出的自定义XDM资源。 在上述示例中， ”[!DNL Loyalty details]“自定义字段组和”[!DNL Loyalty Members]已包含&#39;&#39;架构。 架构使用的任何核心资源都不会包含在导出中，因为这些资源在所有沙盒和组织中都可用。

请注意，您组织的租户ID的每个实例均显示为 `<XDM_TENANTID_PLACEHOLDER>` 在有效负荷中。 这些占位符将自动替换为相应的租户ID值，具体取决于您在下一步中导入架构的位置。

## 使用API导入资源 {#import-resource-with-api}

在复制了架构的导出JSON后，您可以将其用作POST请求的有效负载到 `/rpc/import` 架构注册表API中的端点。 请参阅 [导入端点指南](../api/import.md) 有关如何配置调用以将架构发送到所需组织和沙盒的详细信息。

## 后续步骤

按照本指南，您已成功将XDM架构导出到其他组织或沙盒。 欲知关于 [!UICONTROL 架构] UI，请参阅 [[!UICONTROL 架构] UI概述](./overview.md).
