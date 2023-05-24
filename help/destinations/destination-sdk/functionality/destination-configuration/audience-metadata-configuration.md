---
description: 瞭解如何為使用Destination SDK建立的目的地設定對象中繼資料設定。
title: 對象中繼資料設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# 對象中繼資料設定

將資料從Experience Platform匯出至目的地時，您可能需要在Experience Platform和目的地之間共用特定的對象中繼資料，例如區段名稱或區段ID。

Destination SDK提供的工具可讓您以程式設計方式在目的地平台中建立、更新或刪除對象。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或參閱操作說明指南 [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以透過以下方式設定對象中繼資料範本： `/authoring/audience-templates` 端點。 建立對象中繼資料設定後，您可以使用 `/authoring/destinations` 端點以設定 `audienceMetadataConfig` 區段。 本節說明目的地應將哪些區段中繼資料對應至您的對象範本。

請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [建立對象範本](../../metadata-api/create-audience-template.md)
* [更新對象範本](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

建立對象中繼資料設定時，您可以使用下表所述的引數來設定區段對應設定。

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布尔值 | 指示是否 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目的地啟用工作流程中的值應為Experience Platform區段名稱。 |
| `mapExperiencePlatformSegmentId` | 布尔值 | 指示是否 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目的地啟用工作流程中的值應為Experience Platform區段ID。 |
| `mapUserInput` | 布尔值 | 啟用或停用使用者輸入的 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標啟用工作流程中的值。 若設為 `true`， `audienceTemplateId` 不存在。 |
| `audienceTemplateId` | 布尔值 | 此 `instanceId` 的 [對象中繼資料範本](../../metadata-api/create-audience-template.md) 用於您的目的地。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

閱讀本文章後，您應該更瞭解如何為目的地設定對象中繼資料。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證設定](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)