---
keywords: Experience Platform；熱門主題；XDM；XDM系統；XDM個人設定檔；XDM ExperienceEvent；XDM體驗事件；experienceEvent；experienceEvent；XDM體驗事件；XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述；疑難排解；FAQ；FAQ；聯合結構描述；聯合設定檔；聯合設定檔；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400；
solution: Experience Platform
title: XDM系統疑難排解指南
description: 尋找有關Experience Data Model (XDM)常見問題的解答，包括解決常見API錯誤的步驟。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---

# XDM系統疑難排解指南

本檔案提供以下專案的常見問題解答： [!DNL Experience Data Model] Adobe Experience Platform中的(XDM)和XDM系統，包括常見錯誤的疑難排解指南。 有關其他Platform服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 是開放原始碼規格，定義用於客戶體驗管理的標準化結構。 用於以下專案的方法： [!DNL Experience Platform] 已建置， **XDM系統**，可操作 [!DNL Experience Data Model] 供使用的結構描述 [!DNL Platform] 服務。 此 **[!DNL Schema Registry]** 提供使用者介面和RESTful API，以存取 **[!DNL Schema Library]** 範圍 [!DNL Experience Platform]. 請參閱 [XDM檔案](home.md) 以取得詳細資訊。

## 常见问题解答

以下是有關XDM系統和使用的常見問題解答清單 [!DNL Schema Registry] API。

### 如何將欄位新增至結構描述？

您可以使用結構描述欄位群組，將欄位新增到結構描述。 每個欄位群組都與一個或多個類別相容，允許欄位群組用於實作這些相容類別之一的任何結構描述中。 雖然Adobe Experience Platform為數個產業欄位群組提供他們自己的預先定義欄位，但您可以使用API或使用者介面建立自訂欄位群組，將自己的欄位新增到結構描述中。

有關在中建立欄位群組的詳細資訊 [!DNL Schema Registry] API，請參閱 [欄位群組端點指南](api/field-groups.md#create). 如果您有使用UI，請參閱 [結構描述編輯器教學課程](./tutorials/create-schema-ui.md).

### 欄位群組與資料型別的最佳用途為何？

[欄位群組](./schema/composition.md#field-group) 是定義結構描述中一或多個欄位的元件。 欄位群組會強制實施其欄位在結構描述階層中的顯示方式，因此會在其包含的每個結構描述中顯示相同的結構。 欄位群組僅與特定類別相容，由識別專案群組 `meta:intendedToExtend` 屬性。

[資料型別](./schema/composition.md#data-type) 也可以為結構描述提供一個或多個欄位。 不過，與欄位群組不同，資料型別不受限於特定類別。 這讓資料型別成為描述通用資料結構的更具彈性的選項，這些資料結構可重複用於具有不同類別的多個結構描述。

### 結構描述的唯一ID為何？

全部 [!DNL Schema Registry] 資源（結構描述、欄位群組、資料型別、類別）的URI會作為唯一ID用於參考和查詢。 在API中檢視結構描述時，您可以在頂層找到它 `$id` 和 `meta:altId` 屬性。

如需詳細資訊，請參閱 [資源識別](api/getting-started.md#resource-identification) 中的區段 [!DNL Schema Registry] API指南。

### 結構描述何時開始防止重大變更？

只要結構描述從未用於建立資料集或啟用，即可進行重大變更 [[!DNL Real-Time Customer Profile]](../profile/home.md). 結構描述用於資料集建立或啟用以搭配使用後 [!DNL Real-Time Customer Profile]，的規則 [結構描述演變](schema/composition.md#evolution) 會由系統嚴格執行。

### 長欄位型別的大小上限是多少？

長欄位型別是整數，大小上限為53(+1)位元，可能的範圍介於 — 9007199254740992到9007199254740992之間。 這是由於JSON的JavaScript實作呈現長整數的方式存在限制。

如需欄位型別的詳細資訊，請參閱以下檔案： [XDM欄位型別限制](./schema/field-constraints.md).

### 如何為我的結構描述定義身分？

在 [!DNL Experience Platform]，無論資料來源為何，身分都會用來識別主旨（通常是個人）。 藉由將關鍵欄位標示為「身分」，可在結構描述中定義身分。 身分識別的常用欄位包括電子郵件地址、電話號碼、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)、CRM ID和其他唯一ID欄位。

可使用API或使用者介面將欄位標示為身分。

#### 在API中定義身分

在API中，身分識別是透過建立身分描述項來建立。 身分描述項會指出結構描述的特定屬性是唯一識別碼。

身分描述項是由POST對/descriptors端點的要求所建立。 如果成功，您將會收到HTTP Status 201 （已建立）和包含新描述項詳細資訊的回應物件。

如需在API中建立身分描述項的詳細資訊，請參閱以下檔案： [描述項](api/descriptors.md) 中的區段 [!DNL Schema Registry] 開發人員指南。

#### 在UI中定義身分

在架構編輯器中開啟您的架構後，選取 **[!UICONTROL 結構]** 要標籤為身分的編輯器區段。 下 **[!UICONTROL 欄位屬性]** 在右側，選取 **[!UICONTROL 身分]** 核取方塊。

如需在UI中管理身分的詳細資訊，請參閱以下章節： [定義身分欄位](./tutorials/create-schema-ui.md#identity-field) 區段（在架構編輯器教學課程中）。

### 我的結構描述需要主要身分嗎？

主要身分是選用的，因為結構描述可能沒有或只有一個。 但是，結構描述必須具有主要身分，才能啟用結構描述以便用於 [!DNL Real-Time Customer Profile]. 請參閱 [身分](./tutorials/create-schema-ui.md#identity-field) 結構描述編輯器教學課程的區段以取得詳細資訊。

### 如何啟用結構描述以用於 [!DNL Real-Time Customer Profile]？

結構描述已啟用以用於中 [[!DNL Real-Time Customer Profile]](../profile/home.md) 在中新增「union」標籤 `meta:immutableTags` 結構描述的屬性。 啟用結構描述以用於 [!DNL Profile] 可使用API或使用者介面完成。

#### 啟用現有結構描述 [!DNL Profile] 使用API

發出PATCH請求以更新結構並新增 `meta:immutableTags` 屬性，作為包含「union」值的陣列。 如果更新成功，回應將顯示更新的結構描述，其中現在包含聯合標籤。

如需使用API啟用結構描述以用於中的詳細資訊 [!DNL Real-Time Customer Profile]，請參閱 [聯合](./api/unions.md) 檔案 [!DNL Schema Registry] 開發人員指南。

#### 啟用現有結構描述 [!DNL Profile] 使用UI

在 [!DNL Experience Platform]，選取 **[!UICONTROL 結構描述]** 在左側導覽列中，從結構描述清單中選取您要啟用的結構描述名稱。 然後，在編輯器的右側下 **[!UICONTROL 結構描述屬性]**，選取 **[!UICONTROL 設定檔]** 以將其開啟。


如需詳細資訊，請參閱以下章節： [用於即時客戶個人檔案](./tutorials/create-schema-ui.md#profile) 在 [!UICONTROL 結構描述編輯器] 教學課程。

### 我可以直接編輯聯合結構描述嗎？

聯合結構描述是唯讀的，並由系統自動產生。 無法直接編輯它們。 在實作該類別的結構描述中新增「聯合」標籤時，會為特定類別建立聯合結構描述。

如需XDM中聯合的詳細資訊，請參閱 [聯合](./api/unions.md) 中的區段 [!DNL Schema Registry] API指南。

### 如何格式化資料檔以擷取資料到我的結構描述中？

[!DNL Experience Platform] 接受以下任一專案中的資料檔： [!DNL Parquet] 或JSON格式。 這些檔案的內容必須符合資料集參照的結構描述。 如需資料檔擷取最佳實務的詳細資訊，請參閱 [批次擷取概觀](../ingestion/home.md).

## 錯誤與疑難排解

以下為使用時可能會遇到的錯誤訊息清單 [!DNL Schema Registry] API。

### 找不到資源

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

當系統找不到特定資源時，會顯示此錯誤。 資源可能已被刪除，或API呼叫中的路徑無效。 在重試之前，請確定您已輸入API呼叫的有效路徑。 您可能需要檢查您是否為資源輸入了正確的ID，並且路徑已使用適當的容器（全域或租使用者）正確命名。

>[!NOTE]
>
>根據正在擷取的資源型別，此錯誤可能會使用以下任何一項 `type` URI：
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


如需在API中建構查閱路徑的詳細資訊，請參閱 [容器](./api/getting-started.md#container) 和 [資源識別](api/getting-started.md#resource-identification) 中的區段 [!DNL Schema Registry] 開發人員指南。

### 標題不是唯一的

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

當您嘗試建立標題已被其他資源使用的資源時，會顯示此錯誤訊息。 標題在所有資源型別中必須是唯一的。 例如，如果您嘗試建立的欄位群組標題已被結構描述使用，您將收到此錯誤。

### 名稱空間驗證錯誤

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

當您嘗試使用不正確的名稱空間欄位建立資源，或將不正確的名稱空間欄位新增到現有資源時，會顯示此錯誤訊息。

貴組織定義的資源必須將租使用者ID下的欄位命名為名稱空間，以避免與其他產業和廠商資源衝突。 使用標準欄位群組建立結構描述時，您在這些欄位群組的結構中新增的任何自訂欄位也必須以租使用者ID命名。

>[!NOTE]
>
>根據名稱空間錯誤的特定性質，此錯誤可能會使用以下任一項 `type` URI以及不同的訊息詳細資料：
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


如需XDM資源的正確資料結構的詳細範例，請參閱結構描述登入API指南：

* [建立自訂類別](./api/classes.md#create)
* [建立自訂欄位群組](./api/field-groups.md#create)
* [建立自訂資料型別](./api/data-types.md#create)

### 接受標頭無效

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

中的GET請求 [!DNL Schema Registry] API需要 `Accept` 標頭，讓系統決定如何格式化回應。 當需要時，會發生此錯誤 `Accept` 標頭無效或遺失。

根據您使用的端點， `detailed-message` 屬性指出何為有效的 `Accept` 標題看起來應該像成功回應的樣子。 確定您已正確輸入 `Accept` 在重試之前，嘗試建立的API請求相容的標頭。

>[!NOTE]
>
>根據使用的端點，此錯誤可能使用以下任一項 `type` URI：
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


如需不同API請求的相容Accept標頭清單，請參閱其在 [Schema Registry開發人員指南](./api/overview.md).

### [!DNL Real-Time Customer Profile] 錯誤

以下錯誤訊息與啟用結構描述的相關操作 [!DNL Real-Time Customer Profile]. 請參閱 [聯合](./api/unions.md) 中的區段 [!DNL Schema Registry] API指南，以瞭解詳細資訊。

#### 必須有參考身分描述項

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

當您嘗試為以下專案啟用結構描述時，此錯誤訊息便會顯示： [!DNL Profile] 而且其中一個屬性包含沒有參考身分描述項的關係描述項。 將參考身分描述項新增到有問題的結構描述欄位以解決此錯誤。

#### 參考身分描述項欄位和目的地結構描述的名稱空間必須相符

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>對於此錯誤，「目的地結構描述」是指關係中的參考結構描述。

為了啟用包含關係描述項的結構描述，以便用於 [!DNL Profile]，來源欄位的名稱空間和參考欄位的主要名稱空間必須相同。 當您嘗試啟用包含不匹配名稱空間的結構描述以做為參考身分描述項時，會顯示此錯誤訊息。

確保 `xdm:namespace` 參考結構描述身分欄位的值與 `xdm:identityNamespace` 來源欄位參考身分描述項中的屬性以解決此問題。

如需標準身分名稱空間程式碼的清單，請參閱以下小節： [標準名稱空間](../identity-service/namespaces.md) 身分名稱空間概觀中的。

#### 結構描述必須包含identityMap或主要身分

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

在為「設定檔」啟用結構描述之前，您必須先 [建立主要身分描述項](./api/descriptors.md#create) 或包含身分對應欄位，以取代主要身分身分。

#### 無法合併不相容的資料型別

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

屬於相同類別的所有已啟用設定檔的結構描述必須能夠合併在一起，才能為該類別建構聯合結構描述。 當您嘗試將欄位新增到結構描述時，會出現此錯誤，此結構描述的路徑由另一個已啟用設定檔的結構描述共用，且資料型別與原始結構描述不同。 由於結構描述已啟用設定檔並包含相同的欄位路徑，在建構聯合結構描述時，設定檔會嘗試將這兩個欄位合併為一個。 由於無法將不同的資料型別合併在一起，因此會將此視為合併衝突，因此是不允許的。

若要解決此問題，請為欄位選擇不同的名稱，或是在唯一名稱空間物件下巢狀內嵌欄位，以避免與相同類別下其他具有類似欄位的設定檔啟用結構描述發生合併衝突。
