---
title: Experience Platform中資料收集的許可權管理
description: 有關如何在Adobe Experience Platform中管理許可權和控制資料收集功能存取的高級概觀。
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 876339019b324d4483152ed6f24bd6ad749ea7ba
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 5%

---

# Experience Platform中資料收集的許可權管理

[Adobe Experience Platform中的資料彙集](./home.md) 由數種不同的技術組成，可共同合作收集及傳輸您的資料。 這些技術的存取權可透過Adobe Admin Console中精細的角色型許可權來控制。

本指南說明如何管理資料收集功能的許可權。

## 快速入门

若要設定資料收集的存取控制，您必須擁有與Adobe Experience Platform Data Collection產品整合之組織的管理員許可權。 可授予或撤銷許可權的最小角色為 **產品設定檔管理員**. 可以管理許可權的其他管理員角色包括 **產品管理員** （可以管理產品內的所有設定檔）和 **系統管理員** （無限制）。 請參閱以下文章： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 如需詳細資訊，請參閱Adobe企業管理指南。

本指南假設您熟悉基本的Admin Console概念，例如產品設定檔，以及產品設定檔如何授予個別使用者和群組的產品許可權。 如需詳細資訊，請參閱 [Admin Console使用手冊](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 可用許可權

透過Admin Console中的兩個產品指定來提供資料收集的相關許可權： **Adobe Experience Platform** 和 **Adobe Experience Platform資料彙集**. 以下各節概述每個產品下提供的許可權，以及這些許可權授予存取權的特定功能的說明。

### Adobe Experience Platform許可權

Adobe Experience Platform下的許可權包括存取資料串流、身分、結構描述和沙箱。 如需設定Adobe Experience Platform許可權的相關步驟，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 沙盒 | (不适用) | 根據 [沙箱](../sandboxes/home.md) 如果您已在組織下建立，則可以透過Admin Console中的此許可權類別控制對每一個的存取。 |
| 数据建模 | 管理架构 | 授予檢視、建立和編輯的能力 [體驗資料模型(XDM)結構描述](../xdm/home.md). |
| 数据建模 | 查看架构 | 授予結構描述的唯讀存取權。 |
| Identity Management | 管理身份命名空间 | 授予檢視、建立和編輯的能力 [身分名稱空間](../identity-service/namespaces.md). |
| Identity Management | 查看标识命名空间 | 授予識別名稱空間的唯讀存取權。 |
| 数据收集 | 管理資料串流 | 授予檢視、建立和編輯的能力 [資料串流](../edge/datastreams/overview.md). |
| 数据收集 | 檢視資料串流 | 授予資料串流的唯讀存取權。 |

{style="table-layout:auto"}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Adobe Experience Platform資料收集許可權

Adobe Experience Platform資料收集下的許可權可控制對標籤和事件轉送功能（包括屬性、擴充功能和環境）的存取。 如需設定Adobe Experience Platform資料收集許可權的相關步驟，請參閱 [以下區段](#manage).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| 平台 | Web | 授予存取權 [Web屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 平台 | 移动设备 | 授予存取權 [行動屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 平台 | Edge | 授予存取權 [事件轉送邊緣屬性](../tags/ui/event-forwarding/getting-started.md) 與其他屬性權利結合時。 |
| 属性 | (不适用) | 根據已在您的組織下建立的屬性，您可以透過Admin Console中的此許可權類別控制對每一個屬性的存取。<br><br>使用者的指派屬性許可權僅適用於他們透過此許可權類別被授予存取權的屬性。 |
| 资产权限 | 批准 | 授予核准程式庫組建的能力，使其成為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 资产权限 | 开发 | 授予開發程式庫組建作為一部分的能力 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 资产权限 | 編輯屬性 | 授予編輯使用者有權存取之屬性的基本設定的能力。 |
| 资产权限 | 管理環境 | 授予管理 [環境](../tags/ui/publishing/environments.md) 使用者有權存取的屬性。 |
| 资产权限 | 管理擴充功能 | 授予管理 [擴充功能](../tags/ui/managing-resources/extensions/overview.md) 使用者有權存取的屬性。 |
| 资产权限 | 发布 | 授予將程式庫組建發佈為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 公司权限 | 開發擴充功能 | 授予建立及修改組織擁有的擴充功能套件的能力，包括私人發行和公開發行請求。 |
| 公司权限 | 管理擴充功能 | 此許可權僅適用於您擁有Adobe Journey Optimizer或其他解決方案的授權，可授予行動應用程式內及推送訊息存取權時。 這可讓您管理Adobe Experience Cloud知道的應用程式，以及與Firebase Cloud Messaging服務和Apple推播通知服務通訊所需的推播認證。 |

{style="table-layout:auto"}

>[!NOTE]
>
>如需這些許可權如何影響標籤中功能的詳細資訊，包括常見情境的管理策略，請參閱標籤檔案： [使用者許可權](../tags/ui/administration/user-permissions.md).

## 管理权限 {#manage}

如上一節所述，資料收集的許可權是透過Admin Console中的兩個產品名稱來管理： **Adobe Experience Platform** 和 **Adobe Experience Platform資料彙集**.

若要管理這些許可權，請登入 [Admin Console](https://adminconsole.adobe.com/) 並選取 **[!UICONTROL 產品]** 從頂端導覽列中。 從這裡，選取您要設定之許可權的產品卡。 如需如何管理Admin Console中每個產品下相關許可權的步驟，請參閱以下小節：

* [Adobe Experience Platform許可權](#manage-platform)
* [Adobe Experience Platform資料收集許可權](#manage-collection)

### 在Adobe Experience Platform下管理許可權 {#manage-platform}

從 **[!UICONTROL 產品]** 在Admin Console中檢視，選取 **[!UICONTROL Adobe Experience Platform資料彙集]**. 選取您要編輯許可權的產品設定檔，然後導覽至 **[!UICONTROL 許可權]** 標籤。

若要存取資料收集功能，您必須啟用 **[!UICONTROL 沙箱]**， **[!UICONTROL 資料模型]**， **[!UICONTROL Identity Management]**、和 **[!UICONTROL 資料彙集]** 類別。

![以Admin Console顯示資料收集產品卡的影像](./images/permissions/platform-permission-card.png)

請參閱 [存取控制UI指南](../access-control/ui/overview.md) 以取得管理Platform許可權的詳細說明。

>[!NOTE]
>
>根據您的組織有權存取的產品SKU，您可能沒有每個可用的平台許可權。

### 在Adobe Experience Platform資料收集下管理許可權 {#manage-collection}

從 **[!UICONTROL 產品]** 在Admin Console中檢視，選取 **[!UICONTROL Adobe Experience Platform資料彙集]**.

![以Admin Console顯示資料收集產品卡的影像](./images/permissions/data-collection-card.png)

#### 選取或建立產品設定檔

下一個畫面顯示貴組織下資料收集的可用產品設定檔清單，預設設定檔為 **[!DNL Default Data Collection All Access]**. 您可以視需要選擇編輯預設的產品設定檔，也可以選擇 **[!UICONTROL 新設定檔]** 以建立一個。 如果您的組織中有多個角色或使用者群組需要不同的存取層級，您應該為每個角色或使用者群組建立個別的產品設定檔。

![顯示Admin Console中資料收集的產品設定檔的影像](./images/permissions/new-profile.png)

選取或建立產品設定檔後，您可以使用 **[!UICONTROL 編輯]** 要開始的圖示 [編輯許可權](#edit-permissions) ，或選取 **[!UICONTROL 使用者]** 索引標籤以開始 [指派使用者](#assign-users) 至設定檔。

![顯示產品設定檔Admin Console的許可權索引標籤的影像](./images/permissions/edit-permission-categories.png)

#### 編輯產品設定檔的許可權 {#edit-permissions}

編輯設定檔的許可權時，可用許可權會列在左欄，而包含在設定檔中的許可權則會列在右欄。 選取列出的許可權，以便在任一欄之間移動。

![此影像顯示新增至包含欄下的許可權](./images/permissions/added-permissions.png)

許可權會整理到不同類別中。 若要在類別之間切換，請從左側導覽中選取所需的類別。

![此影像顯示許可權底下的公司許可權區段](./images/permissions/switch-category.png)

選取 **[!UICONTROL 儲存]** 完成許可權設定後。

![此影像顯示正在為產品設定檔儲存的許可權設定](./images/permissions/save-permissions.png)

產品設定檔檢視會重新出現，並反映新增的許可權。

![顯示產品設定檔新增許可權的影像](./images/permissions/permissions-added.png)

#### 將使用者指派至產品設定檔 {#assign-users}

若要將使用者指派給產品設定檔（並授予他們設定檔設定的許可權），請選取 **[!UICONTROL 使用者]** 索引標籤，後面接著 **[!UICONTROL 新增使用者]**.

![顯示Admin Console中產品設定檔的使用者索引標籤的影像](./images/permissions/manage-users.png)

如需管理產品設定檔使用者的詳細資訊，請參閱 [Admin Console檔案](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## 后续步骤

本指南說明資料收集的可用許可權，以及如何透過Admin Console管理這些許可權。 如需管理其他Adobe Experience Platform功能許可權的詳細資訊，請參閱 [存取控制檔案](../access-control/home.md).
