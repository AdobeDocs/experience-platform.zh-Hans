---
solution: Experience Platform
title: 如何取得並授予Experience Platform儀表板的存取許可權
type: Documentation
description: 授予使用者使用Adobe Admin Console檢視、編輯和更新Experience Platform儀表板的能力。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---

# 儀表板的存取許可權

若要授與使用者檢視、編輯和更新控制面板的能力，您必須先啟用許可權。 在Adobe Experience Platform中，存取控制是透過 [Adobe Admin Console](https://adminconsole.adobe.com/). 使用者透過中的產品設定檔連結許可權和沙箱 [!DNL Admin Console].

本檔案提供儀表板可用許可權的摘要，包括這些許可權授予的存取權功能以及這些許可權啟用的使用者功能。 如需取得和指派存取許可權的詳細資訊，請先閱讀 [存取控制總覽](../access-control/home.md).

## 先决条件

為了設定存取控制 [!DNL Experience Platform]，您必須擁有組織的管理員許可權， [!DNL Experience Platform] 產品整合。 請參閱以下文章中的Adobe Help Center： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得詳細資訊。

## 可用的儀表板許可權 {#available-permissions}

此 [!DNL Dashboards] 服務提供三種許可權，結合後可提供對的完整存取 [!UICONTROL 設定檔]， [!UICONTROL 區段]， [!UICONTROL 目的地]、和 [!UICONTROL 授權使用情況] Adobe Experience Platform中的儀表板。 這些許可權包括：

| 权限 | 描述 |
|---|---|
| **管理標準儀表板** | 此許可權是 **全域讀取和寫入許可權**. 它可讓您 [建立自訂Widget](./customize/custom-widgets.md) 和 [編輯Widget結構描述](./customize/edit-schema.md) 透過 [!UICONTROL Widget資料庫]. |
| **檢視標準儀表板** | 這可提供 **唯讀** 的功能 [!UICONTROL 設定檔]， [!UICONTROL 目的地]、和 [!UICONTROL 區段] 控制面板，並可透過Platform的左側導覽存取控制面板。 它也會新增 [!UICONTROL 儀表板] 左側導覽並存取 [!UICONTROL 儀表板] 詳細目錄與整合索引標籤。 |
| **檢視授權使用量儀表板** | 此許可權可讓使用者 **唯讀** 存取 [授權使用量儀表板](./guides/license-usage.md) 在Experience PlatformUI中。 |

有五個許可權未包含在 [!DNL Dashboard] 根據您的需求而可能需要的類別。 下表概述其在Admin Console中的類別位置：

>[!IMPORTANT]
>
>兩者皆有 **[!DNL Manage Standard Dashboards]** 和 **[!DNL View Standard Dashboards]** 許可權 **需要** 來自的「檢視」或「管理」許可權 [!DNL Profile Management] 或 [!DNL Destinations] Admin Console類別，以啟用Platform UI內的相關區段。

| 权限 | Admin Console類別位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 存取控制矩陣

下列存取控制矩陣提供需要哪些許可權，以及這些許可權提供的有關存取不同儀表板功能的功能劃分。 許可權會列在頂端水準列上，而Platform UI工作區則會列在左側欄。

|  | [!UICONTROL 檢視標準儀表板] 或 [!UICONTROL 管理標準儀表板] | [!UICONTROL 檢視設定檔]，<br/>[!UICONTROL 檢視區段]，<br/> [!UICONTROL 檢視目的地] | [!UICONTROL 管理查詢] 和 [!UICONTROL 管理沙箱] | [!UICONTROL 檢視授權使用量儀表板] |
|---|---|---|---|---|
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations] 左側導覽列中。 | 不适用 | **需要「檢視」或「管理」許可權** 每個個別控制面板的預設值。 | 不适用 | 不适用 |
| [!DNL Dashboards] 左側導覽列中。 | 已啟用 | **至少需要一個**. | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（瀏覽標籤） | 已啟用 | 不适用 | 不适用 | 不适用 |
| [!DNL Dashboards] [!DNL Integrations] 標籤 <br/>(用於安裝Power BI) | 已啟用 | **至少需要一個** | 不适用 | 不适用 |
| Power BI安裝按鈕和工作流程 | 已啟用 | 不适用 | **必填** | 不适用 |
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations] 儀表板。<br/>能夠編輯Widget結構描述並新增新屬性以進行Widget自訂 | **需要Manage-standard-dashboard** | **必填（適用於各個控制面板）** | 不适用 | 不适用 |
| [!DNL License Usage Dashboard] | 不适用 | 不适用 | 不适用 | 已啟用 |

{style="table-layout:auto"}

## 將許可權新增至您的產品設定檔

使用上方提供的資訊，將適當的許可權新增至您的產品設定檔。 如需下列專案的完整指示，請參閱檔案： [如何透過存取控制UI新增許可權](../access-control/ui/permissions.md).

如需許可權的描述，請參閱 [可用許可權](#available-permissions) 章節。

>[!NOTE]
>
>您不必為所有使用者啟用所有許可權。 根據您組織的結構，您可能想要為特定使用者建立單獨的產品設定檔，並授予有限存取權（例如唯讀）。 如需瞭解詳細資訊，請參閱有關管理產品設定檔的使用者檔案 [如何為特定使用者指派許可權](../access-control/ui/users.md).

新增必要的存取許可權後，組織內的使用者可以開始在Experience PlatformUI中檢視儀表板，並根據您指派的許可權執行其他動作。
