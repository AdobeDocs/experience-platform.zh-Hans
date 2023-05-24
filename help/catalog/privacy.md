---
keywords: Experience Platform；首頁；熱門主題；資料湖隱私權；身分名稱空間；隱私權；資料湖
solution: Experience Platform
title: Data Lake中的隱私權請求處理
description: Adobe Experience Platform Privacy Service會根據法律和組織隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 本檔案說明與處理儲存在Data Lake之客戶資料的隱私權請求相關的重要概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# Data Lake中的隱私權請求處理

Adobe Experience Platform [!DNL Privacy Service] 根據法律和組織隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。

本檔案說明與處理儲存在Data Lake之客戶資料的隱私權請求相關的重要概念。

>[!NOTE]
>
>本指南僅涵蓋如何在Experience Platform中提出Data Lake的隱私權請求。 如果您也計畫向即時客戶個人檔案資料存放區提出隱私權請求，請參閱以下指南： [設定檔的隱私權請求處理](../profile/privacy.md) 除了本教學課程外。
>
>如需針對其他Adobe Experience Cloud應用程式提出隱私權請求的步驟，請參閱 [Privacy Service檔案](../privacy-service/experience-cloud-apps.md).

## 快速入门

建議您實際瞭解下列事項 [!DNL Experience Platform] 閱讀本指南之前的服務：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Catalog Service]](home.md)：資料位置與譜系內的記錄系統 [!DNL Experience Platform]. 提供可用於更新資料集中繼資料的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service] 使用身分識別名稱空間，透過將身分識別值與來源系統建立關聯來提供身分識別值的內容。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

[!DNL Identity Service] 維護全域定義（標準）和使用者定義（自訂）的身分名稱空間存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需中識別名稱空間的詳細資訊 [!DNL Experience Platform]，請參閱 [身分名稱空間總覽](../identity-service/namespaces.md).

## 將身分資料新增至資料集

為Data Lake建立隱私權請求時，必須為每位客戶提供有效的身分值（及其關聯的名稱空間），以便找到其資料並據以處理。 因此，受隱私權請求約束的所有資料集都必須在其相關聯的XDM結構描述中包含身分描述項。

>[!NOTE]
>
>任何以不支援身分描述項中繼資料的結構描述為基礎的資料集（例如臨時資料集），目前都無法在隱私權請求中處理。

本節逐步說明將身分描述項新增至現有資料集的XDM結構描述的步驟。 如果您已有具有身分描述項的資料集，您可以向前跳至 [下一節](#nested-maps).

>[!IMPORTANT]
>
>在決定要將哪些結構描述欄位設定為身分時，請記住 [使用巢狀對應型別欄位的限制](#nested-maps).

有兩種方法可以將身分描述項新增到資料集結構描述：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在 [!DNL Experience Platform ]使用者介面， **[!UICONTROL 結構描述]** 工作區可讓您編輯現有的XDM結構描述。 若要將身分描述項新增至結構描述，請從清單中選取結構描述，然後遵循以下步驟： [將結構描述欄位設定為身分欄位](../xdm/tutorials/create-schema-ui.md#identity-field) 在 [!DNL Schema Editor] 教學課程。

一旦您將結構描述中的適當欄位設定為身分欄位，您可以繼續下一節： [提交隱私權請求](#submit).

### 使用 API {#identity-api}

>[!NOTE]
>
>本節假設您知道資料集XDM結構描述的唯一URI ID值。 如果您不知道此值，可以使用 [!DNL Catalog Service] API。 閱讀 [快速入門](./api/getting-started.md) 開發人員指南的區段，遵循中概述的步驟 [清單](./api/list-objects.md) 或 [查詢](./api/look-up-object.md) [!DNL Catalog] 物件以尋找您的資料集。 此結構描述ID位於 `schemaRef.id`
>
>本節也假設您知道如何呼叫Schema Registry API。 如需與使用API相關的重要資訊，包括瞭解 `{TENANT_ID}` 以及容器的概念，請參閱 [快速入門](../xdm/api/getting-started.md) API指南的部分。

您可以透過向以下專案發出POST請求，將身分描述項新增到資料集的XDM結構描述中： `/descriptors` 中的端點 [!DNL Schema Registry] API。

**API格式**

```http
POST /descriptors
```

**请求**

以下請求在範例結構描述中的「電子郵件地址」欄位上定義身分描述項。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在建立的描述項型別。 對於身分描述項，值必須是&quot;xdm：descriptorIdentity&quot;。 |
| `xdm:sourceSchema` | 資料集XDM結構描述的唯一URI ID。 |
| `xdm:sourceVersion` | 在中指定的XDM結構描述的版本 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 描述項套用到的結構描述欄位路徑。 |
| `xdm:namespace` | 其中一項 [標準身分名稱空間](../privacy-service/api/appendix.md#standard-namespaces) 識別者 [!DNL Privacy Service]，或由您的組織定義的自訂名稱空間。 |
| `xdm:property` | 「xdm：id」或「xdm：code」，視下使用的名稱空間而定 `xdm:namespace`. |
| `xdm:isPrimary` | 選用的布林值。 為true時，表示欄位是主要身分。 結構描述只能包含一個主要身分。 若不包含，則預設為false。 |

**响应**

成功的回應會傳回HTTP狀態201 （已建立）和新建立之描述項的詳細資訊。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 提交請求 {#submit}

>[!NOTE]
>
>本節說明如何格式化Data Lake的隱私權請求。 強烈建議您檢閱 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 或 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 有關如何提交隱私權工作的完整步驟的檔案，包括如何在請求裝載中正確格式化提交的使用者身分資料。

以下章節概述如何使用向Data Lake提出隱私權請求 [!DNL Privacy Service] UI或API。

>[!IMPORTANT]
>
>無法保證完成隱私權請求所需的時間。 如果在請求仍在處理時資料湖內發生變更，也無法保證這些記錄是否也受到處理。

### 使用UI

在UI中建立工作請求時，請務必選取 **[!UICONTROL AEP資料湖]** 在 **[!UICONTROL 產品]** 以便處理儲存在data lake中之資料的工作。

![此影像顯示隱私權請求建立對話方塊中選取的Data Lake產品](./images/privacy/product-value.png)

### 使用 API

在API中建立工作請求時， `userIDs` 提供的必須使用特定 `namespace` 和 `type` 視其套用的資料存放區而定。 資料湖的ID必須使用 `unregistered` 的 `type` 值和 `namespace` 值符合以下其中一項： [隱私權標籤](#privacy-labels) 已新增至適用資料集的URL名稱。

此外， `include` 請求承載的陣列必須包含請求所針對的不同資料存放區的產品值。 向Data Lake提出請求時，陣列必須包含值 `aepDataLake`.

以下請求會使用未註冊的，為Data Lake建立新的隱私權工作 `email_label` 名稱空間。 此外，還包含中資料湖的產品值 `include` 陣列：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform會處理所有隱私權請求 [沙箱](../sandboxes/home.md) 屬於您的組織。 因此，任何 `x-sandbox-name` 請求中包含的標頭會被系統忽略。

## 正在處理刪除請求

時間 [!DNL Experience Platform] 接收來自的刪除請求 [!DNL Privacy Service]， [!DNL Platform] 傳送確認至 [!DNL Privacy Service] 已收到請求，且受影響的資料已標示為刪除。 接著會在七天內從資料湖中移除記錄。 在這七天期間，資料會軟刪除，因此任何人都無法存取 [!DNL Platform] 服務。

如果您也包含 `ProfileService` 或 `identity` 在隱私權請求中，會分別處理其關聯資料。 請參閱以下小節： [設定檔的刪除請求處理](../profile/privacy.md#delete) 以取得詳細資訊。

## 后续步骤

閱讀本檔案後，您將會瞭解處理Data Lake隱私權請求相關的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

檢視檔案： [即時客戶個人檔案的隱私權請求處理](../profile/privacy.md) ，以瞭解處理隱私權請求的步驟。 [!DNL Profile] 商店。

## 附录

以下小節包含在Data Lake中處理隱私權請求的其他資訊。

### 標籤巢狀對應型別欄位 {#nested-maps}

請務必注意，有兩種巢狀對應型別欄位不支援隱私權標籤：

* 陣列型別欄位中的對應型別欄位
* 另一個對應型別欄位中的對應型別欄位

上述兩個範例的隱私權工作處理最終都將失敗。 因此，建議您避免使用巢狀對應型別欄位來儲存私人客戶資料。 相關消費者ID應該以非對應資料型別儲存在 `identityMap` 記錄型資料集的欄位（本身是對應型別欄位），或 `endUserID` 時間序列資料集的欄位。
