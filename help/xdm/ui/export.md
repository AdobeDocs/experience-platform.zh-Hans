---
solution: Experience Platform
title: 在UI中导出XDM模式
description: 了解如何将现有模式导出到Adobe Experience Platform用户界面中的其他沙箱或IMS组织。
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 2d6e833db7cd79135e6da4c68c9dca8cbed09ce4
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# 在UI中导出XDM模式

模式库中的所有资源都包含在IMS组织内的特定沙箱中。 在某些情况下，您可能希望在沙箱和IMS组织之间共享体验数据模型(XDM)资源。

为满足这一需求，Adobe Experience PlatformUI中的[!UICONTROL 模式]工作区允许您为模式库中的任何模式生成导出有效负荷。 然后，此有效负荷可用于对模式注册表API的调用，以将模式（和所有相关资源）导入目标沙箱和IMS组织。

>[!NOTE]
>
>除了模式(包括类、混合和模式类型)，您还可以使用注册表API导出其他资源。 有关详细信息，请参阅[导出／导入端点](../api/export-import.md)上的指南。

## 先决条件

平台UI允许您导出XDM资源，但必须使用模式注册表API将这些资源导入其他沙箱或IMS组织以完成工作流。 有关必需的身份验证头的重要信息，请参阅[模式注册表API](../api/getting-started.md)快速入门指南，然后按照本指南操作。

## 生成导出有效负荷

在平台UI中，在左侧导航中选择&#x200B;**[!UICONTROL 模式]**。 在[!UICONTROL 模式]工作区中，找到要导出的模式并在[!DNL Schema Editor]中打开它。

>[!TIP]
>
>有关如何查找要查找的XDM资源的详细信息，请参见[探索XDM资源](./explore.md)的指南。

打开模式后，请选择画布右上方的&#x200B;**[!UICONTROL 复制JSON]**&#x200B;图标（![复制图标](../images/ui/export/icon.png)）。

![](../images/ui/export/copy-json.png)

这会将JSON有效负荷复制到剪贴板，并根据模式结构生成。 对于上面显示的“[!DNL Loyalty Members]”模式，将生成以下JSON:

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

有效负荷采用数组的形式，每个数组项都是表示要导出的自定义XDM资源的对象。 在上面的示例中，包含“[!DNL Loyalty details]”自定义混音和“[!DNL Loyalty Members]”模式。 模式使用的任何核心资源都不包括在导出中，因为这些资源可在所有沙箱和IMS组织中使用。

请注意，贵组织的租户ID的每个实例在有效负荷中显示为`<XDM_TENANTID_PLACEHOLDER>`。 这些占位符将自动替换为相应的租户ID值，具体取决于您在下一步中导出模式的位置。

## 使用API导入资源

为模式复制导出JSON后，您可以将它用作POST请求到模式注册表API中的`/import`端点的有效负荷。 有关如何配置调用以将模式发送到正确的IMS组织和沙箱的详细信息，请参阅[在API](../api/export-import.md#import)中导入XDM资源一节。

## 后续步骤

通过遵循本指南，您已成功将XDM模式导出到其他IMS组织或沙箱。 有关[!UICONTROL 模式] UI功能的详细信息，请参阅[[!UICONTROL 模式] UI概述](./overview.md)。