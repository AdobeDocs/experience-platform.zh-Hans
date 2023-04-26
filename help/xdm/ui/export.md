---
solution: Experience Platform
title: 在UI中导出XDM模式
description: 了解如何在Adobe Experience Platform用户界面中将现有架构导出到其他沙箱或组织。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 在UI中导出XDM模式

架构库中的所有资源都包含在组织内的特定沙箱中。 在某些情况下，您可能希望在沙箱和组织之间共享体验数据模型(XDM)资源。

为满足此需求， [!UICONTROL 模式] 使用Adobe Experience Platform UI中的工作区，可为架构库中的任何架构生成导出有效负载。 然后，可以在对架构注册API的调用中使用此有效负载将架构（以及所有相关资源）导入目标沙箱和组织。

>[!NOTE]
>
>除了架构之外，您还可以使用架构注册表API导出其他资源，包括类、架构字段组和数据类型。 请参阅 [导出端点指南](../api/export.md) 以了解更多信息。

## 先决条件

虽然Platform UI允许导出XDM资源，但您必须使用架构注册表API将这些资源导入其他沙箱或组织，以完成工作流。 请参阅 [架构注册API快速入门](../api/getting-started.md) 有关在遵循本指南之前所需的身份验证标头的重要信息。

## 生成导出有效负载 {#generate-export-payload}

在平台UI中，选择 **[!UICONTROL 模式]** 中。 在 [!UICONTROL 模式] 工作区中，选择要导出的架构的行，以在右侧侧栏中显示架构详细信息。

>[!TIP]
>
>请参阅 [浏览XDM资源](./explore.md) 有关如何查找要查找的XDM资源的详细信息。

接下来，选择 **[!UICONTROL 复制JSON]** 图标(![复制图标](../images/ui/export/icon.png))。

![具有模式行和 [!UICONTROL 复制到JSON] 突出显示。](../images/ui/export/copy-json.png)

这会将JSON有效负载复制到剪贴板，这些负载是根据架构结构生成的。 对于“[!DNL Loyalty Members]“架构”中，将生成以下JSON:

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

有效负载采用数组的形式，每个数组项目都是一个对象，表示要导出的自定义XDM资源。 在上例中，“[!DNL Loyalty details]“自定义字段组”和“[!DNL Loyalty Members]“架构”。 导出中不包含该架构使用的任何核心资源，因为这些资源可在所有沙箱和组织中使用。

请注意，贵组织的租户ID的每个实例都显示为 `<XDM_TENANTID_PLACEHOLDER>` 中。 这些占位符将自动替换为相应的租户ID值，具体取决于您在下一步中将架构导入的位置。

## 使用API导入资源

在复制了架构的导出JSON后，您便可以将其用作向POST请求的有效负载 `/rpc/import` 架构注册表API中的端点。 请参阅 [导入端点指南](../api/import.md) 有关如何配置调用以将架构发送到所需组织和沙盒的详细信息。

## 后续步骤

按照本指南，您已成功将XDM架构导出到其他组织或沙盒。 有关 [!UICONTROL 模式] UI，请参阅 [[!UICONTROL 模式] UI概述](./overview.md).
