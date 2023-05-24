---
keywords: 串流； HTTP目的地
title: HTTP API連線
description: 在Adobe Experience Platform中使用HTTP API目的地，將設定檔資料傳送至第三方HTTP端點，以執行您自己的Experience Platform，或針對從Analytics匯出的設定檔資料執行您可能需要的任何其他操作。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 8%

---

# HTTP API連線

## 概述 {#overview}

>[!IMPORTANT]
>
> 此目的地僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

HTTP API目的地是 [!DNL Adobe Experience Platform] 可協助您將設定檔資料傳送至第三方HTTP端點的串流目的地。

若要將設定檔資料傳送至HTTP端點，您必須先 [連線到目的地](#connect-destination) 在 [!DNL Adobe Experience Platform].

## 用例 {#use-cases}

HTTP API目的地可讓您將XDM設定檔資料和受眾區段匯出至一般HTTP端點。 在那裡，您可以對從Experience Platform匯出的設定檔資料執行自己的分析或執行任何其他您可能需要的操作。

HTTP端點可以是客戶自己的系統或協力廠商解決方案。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如在對應畫面中所選擇。 [目的地啟用工作流程](../../ui/activate-segment-streaming-destinations.md#mapping). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

若要使用HTTP API目的地將資料匯出為Experience Platform，您必須符合下列先決條件：

* 您必須有支援REST API的HTTP端點。
* 您的HTTP端點必須支援Experience Platform設定檔結構描述。 HTTP API目的地不支援轉換至第三方裝載結構描述。 請參閱 [匯出的資料](#exported-data) 區段以取得Experience Platform輸出結構描述的範例。
* 您的HTTP端點必須支援標頭。

>[!TIP]
>
> 您也可以使用 [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 以設定整合併將Experience Platform設定檔資料傳送至HTTP端點。

## IP位址允許清單 {#ip-address-allowlist}

為了滿足客戶的安全性和合規性要求，Experience Platform提供您可以允許列出HTTP API目的地的靜態IP清單。 請參閱 [串流目的地的IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以取得允許清單的IP完整清單。

## 支援的驗證型別 {#supported-authentication-types}

HTTP API目的地支援對您的HTTP端點使用幾種驗證型別：

* 沒有驗證的HTTP端點；
* 持有人權杖驗證；
* [OAuth 2.0使用者端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 使用主體表單進行驗證，使用 [!DNL client ID]， [!DNL client secret] 和 [!DNL grant type] HTTP要求內文中，如下列範例所示。

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [OAuth 2.0使用者端認證](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 具有基本授權，並具有包含URL編碼的授權標頭 [!DNL client ID] 和 [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [OAuth 2.0密碼授予](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## 連線到目的地 {#connect-destination}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 連線至此目的地時，您必須提供下列資訊：

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="客户端凭据类型"
>abstract="选择&#x200B;**编码的正文形式**&#x200B;以在请求正文中包含客户端 ID 和客户端密码，或选择&#x200B;**基本授权**&#x200B;以在授权标头中包含客户端 ID 和客户端密码。查看文档中的示例。"

#### 持有人權杖驗證 {#bearer-token-authentication}

如果您選取 **[!UICONTROL 持有人權杖]** 驗證型別以連線至您的HTTP端點，輸入以下欄位並選取 **[!UICONTROL 連線到目的地]**：

![您可以使用持有人權杖驗證來連線至HTTP API目的地的UI畫面影像](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL 持有人權杖]**：插入持有人權杖以驗證您的HTTP位置。

#### 無驗證 {#no-authentication}

如果您選取 **[!UICONTROL 無]** 要連線至您的HTTP端點的驗證型別：

![UI畫面影像，您可在其中使用無驗證連線至HTTP API目的地](../../assets/catalog/http/http-api-authentication-none.png)

當您選取此驗證開啟時，您只需要選取 **[!UICONTROL 連線到目的地]** 且已建立與端點的連線。

#### OAuth 2密碼驗證 {#oauth-2-password-authentication}

如果您選取 **[!UICONTROL OAuth 2密碼]** 驗證型別以連線至您的HTTP端點，輸入以下欄位並選取 **[!UICONTROL 連線到目的地]**：

![UI畫面影像，您可在其中使用OAuth 2搭配密碼驗證連線至HTTP API目的地](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL 存取權杖URL]**：您那邊發出存取權杖的URL，以及（可選）重新整理權杖。
* **[!UICONTROL 使用者端ID]**：此 [!DNL client ID] 您的系統指派給Adobe Experience Platform的許可權。
* **[!UICONTROL 使用者端密碼]**：此 [!DNL client secret] 您的系統指派給Adobe Experience Platform的許可權。
* **[!UICONTROL 使用者名稱]**：存取您HTTP端點的使用者名稱。
* **[!UICONTROL 密碼]**：存取您的HTTP端點的密碼。

#### OAuth 2使用者端憑證驗證 {#oauth-2-client-credentials-authentication}

如果您選取 **[!UICONTROL OAuth 2使用者端認證]** 驗證型別以連線至您的HTTP端點，輸入以下欄位並選取 **[!UICONTROL 連線到目的地]**：

![UI畫面影像，您可在其中使用OAuth 2搭配使用者端憑證驗證連線至HTTP API目的地](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL 存取權杖URL]**：您那邊發出存取權杖的URL，以及（可選）重新整理權杖。
* **[!UICONTROL 使用者端ID]**：此 [!DNL client ID] 您的系統指派給Adobe Experience Platform的許可權。
* **[!UICONTROL 使用者端密碼]**：此 [!DNL client secret] 您的系統指派給Adobe Experience Platform的許可權。
* **[!UICONTROL 使用者端認證型別]**：選取您的端點支援的OAuth2使用者端憑證授權型別：
   * **[!UICONTROL 內文表單已編碼]**：在此案例中， [!DNL client ID] 和 [!DNL client secret] 包含 *在要求內文中* 已傳送至您的目的地。 如需範例，請參閱 [支援的驗證型別](#supported-authentication-types) 區段。
   * **[!UICONTROL 基本授權]**：在此案例中， [!DNL client ID] 和 [!DNL client secret] 包含 *在 `Authorization` 頁首* 在base64編碼並傳送至您的目的地之後。 如需範例，請參閱 [支援的驗證型別](#supported-authentication-types) 區段。

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="标头"
>abstract="按照以下格式输入要包含在目标调用中的任何自定义标头：`header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="HTTP 端点"
>abstract="要将配置文件数据发送到的 HTTP 端点的 URL。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="包括区段名称"
>abstract="如果您希望数据导出包括正在导出的区段的名称，请进行切换。在选中此选项后查看数据导出示例的文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="包括区段时间戳"
>abstract="如果您希望数据导出包括区段创建时间和更新时间的 Unix 时间戳，以及区段映射到用于激活的目标时的 Unix 时间戳，请进行切换。在选中此选项后查看数据导出示例的文档。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="查询参数"
>abstract="（可选）您可以将查询参数添加到 HTTP 端点 URL。格式化您使用的查询参数，如下所示：`parameter1=value&parameter2=value`。"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

![顯示HTTP目的地詳細資訊的已完成欄位的UI畫面影像](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL 名稱]**：輸入您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：輸入有助於您日後識別此目的地的說明。
* **[!UICONTROL 標頭]**：依照此格式，輸入您要包含在目的地呼叫中的任何自訂標頭： `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP端點]**：要將設定檔資料傳送至的HTTP端點URL。
* **[!UICONTROL 查詢引數]**：您可以選擇將查詢引數新增至HTTP端點URL。 格式化您使用的查询参数，如下所示：`parameter1=value&parameter2=value`。
* **[!UICONTROL 包含區段名稱]**：如果您希望資料匯出包含要匯出的區段名稱，請切換按鈕。 如需選取此選項後匯出資料的範例，請參閱 [匯出的資料](#exported-data) 區段下方。
* **[!UICONTROL 包含區段時間戳記]**：如果您希望資料匯出包含建立和更新區段時的UNIX時間戳記，以及區段對應至要啟用的目的地時的UNIX時間戳記，請切換此設定。 如需選取此選項後匯出資料的範例，請參閱 [匯出的資料](#exported-data) 區段下方。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [將受眾資料啟用至串流設定檔匯出目的地](../../ui/activate-streaming-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 目的地屬性 {#attributes}

在 [[!UICONTROL 選取屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化您HTTP API目的地的設定檔匯出行為，以便僅在符合區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至您的API端點。 設定檔會在下列情況下匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個區段的區段成員資格變更所決定。 例如，設定檔已符合其中一個對應至目的地的區段的資格，或已退出其中一個對應至目的地的區段。
* 設定檔更新是由 [身分對應](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合對應至目的地其中一個區段資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由至少一個對應至目的地的屬性變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。

在上述所有情況下，只會將已發生相關更新的設定檔匯出至您的目的地。 例如，如果對應至目的地流程的一個區段有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的程式為遞增式，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，即使屬性本身並未變更，也將匯出這五個新設定檔的所有對應屬性。

### 決定資料匯出的因素，以及匯出中包括的因素 {#what-determines-export-what-is-included}

針對指定設定檔匯出的資料，請務必瞭解以下兩個不同的概念 *決定匯出至HTTP API目的地的資料內容* 和 *匯出中包含哪些資料*.

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示如果任何對應的區段變更狀態(從 `null` 至 `realized` 或從 `realized` 至 `exiting`)或更新任何對應的屬性，就會開始匯出目的地。</li><li>由於身分目前無法對應至HTTP API目的地，因此特定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會被視為變更。</li></ul> | <ul><li>此 `segmentMembership` 物件包含啟動資料流中對應的區段，在資格或區段退出事件後，設定檔的狀態已針對該區段變更。 請注意，如果設定檔符合資格的其他未對應區段屬於相同區段，則這些區段可以屬於目標匯出的一部分 [合併原則](/help/profile/merge-policies/overview.md) 區段在啟動資料流中對應時相同。 </li><li>中的所有身分 `identityMap` 也包括物件(Experience Platform目前不支援在HTTP API目的地中識別對應)。</li><li>目的地匯出只會包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為HTTP目的地，其中在資料流中選取了三個區段，且四個屬性對應至目的地。

![HTTP API目的地資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

個人資料匯出至目的地可由符合或退出其中一個的個人資料決定。 *三個對應的區段*. 不過，在資料匯出中，在 `segmentMembership` 物件(請參閱 [匯出的資料](#exported-data) 區段)，如果該特定設定檔為其他未對應區段的成員，且這些區段與觸發匯出的區段共用相同的合併原則，則可能會顯示其他未對應區段。 如果設定檔符合 **擁有DeLorean Cars的客戶** 區段，但同時也是 **觀看「回到未來」** 影片和 **科幻愛好者** 區段，則其他這兩個區段也會出現在 `segmentMembership` 資料匯出的物件，即使這些物件未在資料流中對映，只要它們與共用相同的合併原則 **擁有DeLorean Cars的客戶** 區段。

從設定檔屬性的角度來看，對上述四個對應屬性所做的任何變更都將決定目的地匯出，而且設定檔上存在的四個對應屬性中的任何一個都會出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

當您新增區段至現有目的地，或當您建立新目的地並將區段對應至該目的地時，Experience Platform會將歷史區段資格資料匯出至該目的地。 符合區段資格的設定檔 *早於* 新增至目的地的區段會在約一小時內匯出至目的地。

## 匯出的資料 {#exported-data}

您的匯出 [!DNL Experience Platform] 資料進入您的 [!DNL HTTP] JSON格式的目標。 例如，下列匯出包含符合特定區段資格的設定檔、是另一個兩個區段的成員，且已退出另一個區段。 匯出也包含設定檔屬性的名字、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分識別為ECID和電子郵件。

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

以下為更多匯出資料範例，具體取決於您在連線目的地流程中選取的UI設定 **[!UICONTROL 包含區段名稱]** 和 **[!UICONTROL 包含區段時間戳記]** 選項：

+++ 以下資料匯出範例包含 `segmentMembership` 區段

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 以下資料匯出範例包含 `segmentMembership` 區段

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 限制和重試原則 {#limits-retry-policy}

在95%的時間中，Experience Platform會嘗試為成功傳送的訊息提供少於10分鐘的輸送量延遲，每個資料流向HTTP目的地的每秒請求率少於10,000個。

如果對您的HTTP API目的地的請求失敗，Experience Platform會儲存失敗的請求，並重試兩次以將請求傳送至您的端點。