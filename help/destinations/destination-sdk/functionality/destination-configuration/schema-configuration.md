---
description: 瞭解如何為使用Destination SDK建立的目的地設定合作夥伴結構。
title: 合作夥伴結構描述設定
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# 合作夥伴結構描述設定

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。將資料內嵌至Platform時，會根據XDM結構描述來建構。 如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱 [結構描述組合基本概念](../../../../xdm/schema/composition.md).

使用Destination SDK建立目的地時，您可以定義自己的合作夥伴結構描述，以供目的地平台使用。 這可讓使用者將設定檔屬性從Platform對應到目的地平台可辨識的特定欄位，而且全都在Platform UI中。

為您的目的地設定合作夥伴結構描述時，您可以微調目的地平台支援的欄位對應，例如：

* 允許使用者對應 `phoneNumber` XDM屬性至 `phone` 目的地平台支援的屬性。
* 建立Experience Platform可動態呼叫的動態合作夥伴結構描述，以擷取目的地內所有支援屬性的清單。
* 定義目的地平台所需的必要欄位對應。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或參閱操作說明指南 [使用Destination SDK設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過以下方式設定結構描述： `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援結構描述設定選項，並顯示客戶在Platform UI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的結構描述設定 {#supported-schema-types}

Destination SDK支援多個結構描述設定：

* 靜態結構描述是透過 `profileFields` 中的陣列 `schemaConfig` 區段。 在靜態結構描述中，您會定義應顯示在Experience PlatformUI中的每個目標屬性 `profileFields` 陣列。 如果您需要更新結構描述，必須 [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md).
* 動態結構描述會使用其他目的地伺服器型別，稱為 [動態結構描述伺服器](../../authoring-api/destination-server/create-destination-server.md)，以根據您自己的API動態產生結構描述。 動態結構描述不會使用 `profileFields` 陣列。 如果您需要更新結構描述，則無需 [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md). 而是由動態結構描述伺服器從您的API擷取更新的結構描述。
* 在架構設定中，您可以選擇新增必要（或預先定義）的對應。 這些是使用者可以在Platform UI中檢視的對應，但在設定與目的地的連線時無法加以修改。 例如，您可以強制電子郵件位址列位一律傳送至目的地。

此 `schemaConfig` 區段會根據您需要的結構描述型別，使用多個設定引數，如下節所示。

## 建立靜態結構描述 {#attributes-schema}

若要使用設定檔屬性建立靜態結構描述，請在 `profileFields` 陣列，如下所示。

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|------|---|
| `profileFields` | 陣列 | 可选 | 定義目的地平台接受的目標屬性陣列，客戶可將其設定檔屬性對應至該陣列。 使用時 `profileFields` 陣列，您可以省略 `useCustomerSchemaForAttributeMapping` 引數完整。 |
| `useCustomerSchemaForAttributeMapping` | 布尔值 | 可选 | 啟用或停用從客戶結構描述到您在 `profileFields` 陣列。 <ul><li>若設為 `true`，使用者只會在對應欄位中看到來源欄。 `profileFields` 不適用於此情況。</li><li>若設為 `false`，使用者可以將來源屬性從他們的結構描述對應到您在 `profileFields` 陣列。</li></ul> 默认值为 `false`。 |
| `profileRequired` | 布尔值 | 可选 | 使用 `true` 使用者是否應該能夠將Experience Platform中的設定檔屬性對應至目的地平台上的自訂屬性。 |
| `segmentRequired` | 布尔值 | 必需 | Destination SDK需要此引數，且此引數應一律設為 `true`. |
| `identityRequired` | 布尔值 | 必需 | 設定為 `true` 如果使用者應該能夠 [身分型別](identity-namespace-configuration.md) 從Experience Platform到您在 `profileFields` 陣列。 |

{style="table-layout:auto"}

產生的UI體驗如下圖所示。

當使用者選擇目標對應時，他們可以看到中定義的欄位 `profileFields` 陣列。

![顯示目標屬性畫面的UI影像。](../../assets/functionality/destination-configuration/select-attributes.png)

選取屬性後，他們便可在目標欄位欄中看到屬性。

![顯示具有屬性的靜態目標結構描述的使用者介面影像](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 建立動態結構描述 {#dynamic-schema-configuration}

Destination SDK支援建立動態合作夥伴結構描述。 相對於靜態結構描述，動態結構描述不會使用 `profileFields` 陣列。 動態結構描述會改用動態結構描述伺服器，該伺服器會從其中擷取結構描述設定，連線到您自己的API。

>[!IMPORTANT]
>
>在建立動態結構描述之前，您必須 [建立動態結構描述伺服器](../../authoring-api/destination-server/create-destination-server.md).

在動態結構描述設定中， `profileFields` 陣列由 `dynamicSchemaConfig` 區段，如下所示。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 字符串 | 必需 | 指示如何進行 [!DNL Platform] 客戶連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`， `PLATFORM_AUTHENTICATION`， `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過上述任何驗證方法登入您的系統 [此處](customer-authentication.md). </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe和您的目的地之間存在全域驗證系統，並且 [!DNL Platform] 客戶不需要提供任何驗證認證即可連線至您的目的地。 在此情況下，您必須 [建立認證物件](../../credentials-api/create-credential-configuration.md) 使用認證API。 </li><li>使用 `NONE` 如果不需要驗證即可將資料傳送至您的目的地平台。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字符串 | 必需 | 此 `instanceId` （屬於您的動態結構描述伺服器）。 此目的地伺服器包含API端點，Experience Platform會呼叫該API端點來擷取動態結構描述。 |
| `dynamicEnum.value` | 字符串 | 必需 | 動態結構描述的名稱，如動態結構描述伺服器設定中所定義。 |
| `dynamicEnum.responseFormat` | 字符串 | 必需 | 一律設為 `SCHEMA` 定義動態結構描述時。 |
| `profileRequired` | 布尔值 | 可选 | 使用 `true` 使用者是否應該能夠將Experience Platform中的設定檔屬性對應至目的地平台上的自訂屬性。 |
| `segmentRequired` | 布尔值 | 必需 | Destination SDK需要此引數，且此引數應一律設為 `true`. |
| `identityRequired` | 布尔值 | 必需 | 設定為 `true` 如果使用者應該能夠 [身分型別](identity-namespace-configuration.md) 從Experience Platform到您在 `profileFields` 陣列。 |

{style="table-layout:auto"}

## 必要的對應 {#required-mappings}

在結構描述設定中，除了您的靜態或動態結構描述外，您還可以選擇新增必要（或預先定義）的對應。 這些是使用者可以在Platform UI中檢視的對應，但在設定與目的地的連線時無法加以修改。

例如，您可以強制電子郵件位址列位一律傳送至目的地。

>[!NOTE]
>
>目前支援下列必要對應組合：
>* 您可以設定必要來源欄位和必要目的地欄位。 在此情況下，使用者無法編輯或選取這兩個欄位中的任何一個，且只能檢視選取專案。
>* 您只能設定必要的目的地欄位。 在此情況下，使用者可選取來源欄位，以對應至目的地。
>
> 目前僅設定必要來源欄位 *not* 支援。

請參閱以下兩個具有必要對應的結構描述設定範例，以及這些範例在 [啟用批次目的地工作流程的資料](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB 必要的來源和目的地對應]

以下範例顯示必要的來源和目的地對應。 當來源欄位和目的地欄位都指定為必要對應時，使用者無法選取或編輯這兩個欄位中的任何一個，而且只能檢視預先定義的選取專案。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 當此設定為true時，除了您在中定義的必要對應外，使用者無法對應啟動流程中的其他屬性和身分 `requiredMappings` 陣列。 |
| `requiredMappings.sourceType` | 字符串 | 必需 | 指示 `source` 欄位。 支援的值： <ul><li>`text/x.schema-path`：此值用於 `source` 欄位是XDM結構描述中的設定檔屬性。</li><li>`text/x.aep-xl`：此值用於： `source` 欄位是由規則運算式定義。 示例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`：此值用於： `source` 欄位由巨集範本定義。 目前唯一支援的巨集範本是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | 字符串 | 必需 | 表示來源欄位的值。 支援的值型別： <ul><li>xdm設定檔屬性。 示例: `personalEmail.address`. 當來源屬性為XDM設定檔屬性時，設定 `sourceType` 引數至 `text/x.schema-path`.</li><li>正则表达式. 示例: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. 當來源屬性為規則運算式時，設定 `sourceType` 引數至 `text/x.aep-xl`.</li><li>巨集範本。 示例:`metadata.segment.alias`. 當來源屬性是巨集範本時，請設定 `sourceType` 引數至 `text/plain`. 目前唯一支援的巨集範本是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | 字符串 | 必需 | 表示目標欄位的值。 當來源欄位和目的地欄位都指定為必要對應時，使用者無法選取或編輯這兩個欄位中的任何一個，且只能檢視選取專案。 |

{style="table-layout:auto"}

因此，兩個 **[!UICONTROL 來源欄位]** 和 **[!UICONTROL 目標欄位]** Platform UI中的區段會呈現灰色。

![UI啟動流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 必要的目的地對應]

以下範例顯示必要的目的地對應。 如果僅將目的地欄位指定為必要欄位，則使用者可以選取要與其對應的來源欄位。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 當此設定為true時，除了您在中定義的必要對應外，使用者無法對應啟動流程中的其他屬性和身分 `requiredMappings` 陣列。 |
| `requiredMappings.destination` | 字符串 | 必需 | 表示目標欄位的值。 僅指定目的地欄位時，使用者可以選取來源欄位以對應至目的地。 |
| `mandatoryRequired` | 布尔值 | 可选 | 指示對應是否應標示為 [強制屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | 布尔值 | 可选 | 指示對應是否應標示為 [重複資料刪除索引鍵](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

因此， **[!UICONTROL 目標欄位]** Platform UI中的區段會呈現灰色，而 **[!UICONTROL 來源欄位]** 區段處於作用中狀態，使用者可以與其互動。 此 **[!UICONTROL 必要索引鍵]** 和 **[!UICONTROL 重複資料刪除索引鍵]** 選項為作用中，使用者無法變更它們。

![UI啟動流程中所需對應的影像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 后续步骤 {#next-steps}

閱讀本文章後，您應該更瞭解Destination SDK支援的結構描述型別，以及如何設定您的結構描述。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)