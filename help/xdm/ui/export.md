---
solution: Experience Platform
title: 在UI中匯出XDM結構描述
description: 瞭解如何在Adobe Experience Platform使用者介面中匯出現有結構描述至其他沙箱或組織。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 在UI中匯出XDM結構描述

Schema Library內的所有資源都包含在組織內的特定沙箱中。 在某些情況下，您可能會想要在沙箱和組織之間共用Experience Data Model (XDM)資源。

為了滿足此需求， [!UICONTROL 結構描述] Adobe Experience Platform UI中的工作區可讓您為架構資料庫中的任何架構產生匯出裝載。 然後，此裝載可用於對結構描述登入API的呼叫中，以將結構描述（以及所有相依資源）匯入目標沙箱和組織。

>[!NOTE]
>
>您也可以使用Schema Registry API匯出除了結構描述以外的其他資源，包括類別、結構描述欄位群組和資料型別。 請參閱 [匯出端點指南](../api/export.md) 以取得詳細資訊。

## 先决条件

雖然Platform UI可讓您匯出XDM資源，但您必須使用Schema Registry API將這些資源匯入其他沙箱或組織以完成工作流程。 請參閱指南，網址為 [開始使用結構描述登入API](../api/getting-started.md) 請參閱本指南，瞭解必要驗證標頭的重要資訊。

## 產生匯出裝載 {#generate-export-payload}

在Platform UI中選取 **[!UICONTROL 結構描述]** 左側導覽列中。 在內 [!UICONTROL 結構描述] 工作區中，選取您要匯出的結構描述列，以在右側邊欄中顯示結構描述詳細資訊。

>[!TIP]
>
>請參閱指南： [探索XDM資源](./explore.md) 有關如何尋找您所尋找XDM資源的詳細資訊。

接下來，選取 **[!UICONTROL 複製JSON]** 圖示(![復製圖示](../images/ui/export/icon.png))。

![具有結構描述列和的「結構描述」工作區 [!UICONTROL 複製到JSON] 反白顯示。](../images/ui/export/copy-json.png)

這會將JSON裝載複製到剪貼簿，並根據結構描述結構產生。 針對&quot;[!DNL Loyalty Members]」結構描述如上所示，會產生以下JSON：

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

裝載採用陣列的形式，每個陣列專案都是一個物件，代表要匯出的自訂XDM資源。 在上述範例中， 「[!DNL Loyalty details]「自訂欄位群組和」[!DNL Loyalty Members]「結構描述包含在內。 結構描述採用的任何核心資源都不會包含在匯出中，因為這些資源可用於所有沙箱和組織。

請注意，您組織的租使用者ID的每個例項都顯示為 `<XDM_TENANTID_PLACEHOLDER>` 在承載中。 這些預留位置會自動取代為適當的租使用者ID值，具體取決於您在下一個步驟中匯入結構描述的位置。

## 使用API匯入資源

複製結構描述的匯出JSON後，您可以將其用作POST請求的裝載 `/rpc/import` 結構描述登入API中的端點。 請參閱 [匯入端點指南](../api/import.md) 有關如何設定呼叫以將結構描述傳送至所需組織和沙箱的詳細資訊。

## 后续步骤

依照本指南，您已成功將XDM結構描述匯出至不同的組織或沙箱。 如需功能的詳細資訊， [!UICONTROL 結構描述] UI，請參閱 [[!UICONTROL 結構描述] UI總覽](./overview.md).
