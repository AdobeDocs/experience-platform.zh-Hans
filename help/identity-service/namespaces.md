---
keywords: Experience Platform；首頁；熱門主題；名稱空間；名稱空間；名稱空間；名稱空間；身分名稱空間；身分名稱空間；身分名稱空間；身分；身分；身分服務；身分服務
solution: Experience Platform
title: 身分名稱空間概觀
description: 身份命名空间是“身份服务”的组件，充当与身份相关的上下文指示器。例如，他們會將「name@email.com」的值視為電子郵件地址，或將「443522」的值視為數值CRM ID。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 482de6a50d14b9de095014b070ce400a2fd273cc
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 8%

---

# 身分名稱空間總覽

身分名稱空間是的元件 [[!DNL Identity Service]](./home.md) 做為身分識別相關內容的指示器。 例如，它們區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。

## 快速入门

使用身份命名空间需要了解所涉及的多个 Adobe Experience Platform 服务。开始使用命名空间之前，请参阅以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
- [[!DNL Identity Service]](./home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
- [[!DNL Privacy Service]](../privacy-service/home.md)：身分名稱空間用於一般資料保護規範(GDPR)等法律隱私權法規的合規性請求中。 每個隱私權請求都是相對於名稱空間提出，以識別哪些消費者的資料應該受到影響。

## 瞭解身分名稱空間

完整身分包含ID值和名稱空間。 跨設定檔片段比對記錄資料時，例如 [!DNL Real-Time Customer Profile] 會合併設定檔資料，身分值和名稱空間必須相符。

例如，兩個設定檔片段可能包含不同的主要ID，但兩者的「電子郵件」名稱空間值相同，因此 [!DNL Platform] 能夠看到這些片段實際上是同一個人，並為該個人將資料彙整在身分圖表中。

![](images/identity-service-stitching.png)

### 身分型別 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="指定标识类型"
>abstract="标识类型控制数据是否存储到标识图形中。非人员标识符不会被存储，所有其他标识类型都会被存储。"
>text="Learn more in documentation"

資料可由數種不同的身分型別識別。 身分型別是在建立身分名稱空間時指定的，並控制資料是否持續存在身分圖表中，以及應該如何處理該資料的任何特殊指示。 除外的所有身分型別 **非人員識別碼** 請遵循相同的行為，將名稱空間及其對應的ID值拼接至身分圖表叢集。 使用時，資料不會彙整在一起 **非人員識別碼**.

下列身分型別可在以下位置使用： [!DNL Platform]：

| 身分型別 | 描述 |
| --- | --- |
| Cookie ID | Cookie ID可識別網頁瀏覽器。 這些身分對於擴充至關重要，並構成身分圖表的大多數。 然而，它們自然會迅速衰落，並隨著時間而失去價值。 |
| 跨裝置ID | 跨裝置ID會識別個人，通常會將其他ID連結在一起。 範例包括登入ID、CRM ID和熟客ID。 此表示會 [!DNL Identity Service] 以敏感地處理值。 |
| 裝置ID | 裝置ID會識別硬體裝置，例如IDFA (iPhone和iPad)、GAID (Android)和RIDA (Roku)，而且可由家中的多個人共用。 |
| 电子邮件地址 | 電子郵件地址通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 此型別的身分包含個人識別資訊(PII)。 此表示會 [!DNL Identity Service] 以敏感地處理值。 |
| 非人员标识符 | 非人員ID是用來儲存需要名稱空間但未連線至人員叢集的識別碼。 例如，產品SKU、與產品、組織或商店相關的資料。 |
| 电话号码 | 電話號碼通常與單一人員相關聯，因此可用於跨不同頻道識別該人員。 此型別的身分識別包括PII。 此表示以下情況： [!DNL Identity Service] 以敏感地處理值。 |

### 標準名稱空間 {#standard}

Experience Platform提供數個適用於所有組織的身分名稱空間。 這些稱為標準名稱空間，可透過以下方式檢視： [!DNL Identity Service] API或透過Platform UI。

提供下列標準名稱空間，供Platform內的所有組織使用：

| 显示名称 | 描述 |
| ------------ | ----------- |
| AdCloud | 代表AdobeAdCloud的名稱空間。 |
| Adobe Analytics （舊版ID） | 代表Adobe Analytics的名稱空間。 請參閱以下檔案： [Adobe Analytics名稱空間](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 以取得詳細資訊。 |
| Apple IDFA （廣告商的ID） | 代表廣告商Apple ID的名稱空間。 請參閱以下檔案： [興趣型廣告](https://support.apple.com/en-us/HT202074) 以取得詳細資訊。 |
| Apple推播通知服務 | 代表使用Apple推播通知服務所收集之身分的名稱空間。 請參閱以下檔案： [Apple推播通知服務](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 以取得詳細資訊。 |
| CORE | 代表Adobe Audience Manager的名稱空間。 此名稱空間也可以透過其舊版名稱來參照：「Adobe AudienceManager」。 請參閱以下檔案： [AUDIENCE MANAGERID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 以取得詳細資訊。 |
| ECID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](./ecid.md) 以取得詳細資訊。 |
| 电子邮件 | 代表電子郵件地址的名稱空間。 這類名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的名稱空間。 使用SHA256雜湊之前，此名稱空間中提供的值會轉換為小寫。 在電子郵件地址標準化之前，需要修剪開頭和結尾的空格。 此設定無法回溯變更。 請參閱以下檔案： [sha256雜湊支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 以取得詳細資訊。 |
| Firebase雲端通訊 | 代表使用Google Firebase Cloud Messaging收集以進行推播通知的身分識別的名稱空間。 請參閱以下檔案： [Google Firebase雲端通訊](https://firebase.google.com/docs/cloud-messaging) 以取得詳細資訊。 |
| Google Ad ID (GAID) | 代表Google Advertising ID的名稱空間。 請參閱以下檔案： [Google廣告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以取得詳細資訊。 |
| Google點按ID | 代表Google點選ID的名稱空間。 請參閱以下檔案： [Google Ads中的點選追蹤](https://developers.google.com/adwords/api/docs/guides/click-tracking) 以取得詳細資訊。 |
| Phone | 代表電話號碼的名稱空間。 這類名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電話(E.164) | 代表需要以E.164格式雜湊的原始電話號碼的名稱空間。 E.164格式包含加號(`+`)、國際國家/地區的電話代碼、區域代碼和電話號碼。 例如：`(+)(country code)(area code)(phone number)`。 |
| 電話(SHA256) | 代表需要使用SHA256雜湊之電話號碼的名稱空間。 您必須移除符號、字母及任何前導零。 您也必須新增國家/地區呼叫代碼作為前置詞。 |
| 電話(SHA256_E.164) | 代表需要使用SHA256和E.164格式雜湊的原始電話號碼的名稱空間。 |
| TNTID | 代表Adobe Target的名稱空間。 請參閱以下檔案： [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 瞭解更多資訊。 |
| Windows AID | 代表Windows Advertising ID的名稱空間。 請參閱以下檔案： [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 以取得詳細資訊。 |

### 檢視身分名稱空間 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="查看集成标识"
>abstract="集成身份是用于连接其他系统的命名空间，不用于标识解析或拼接标识。<br>默认情况下，这些标识是隐藏的。使用切换功能来查看集成命名空间。"

若要在UI中檢視身分識別名稱空間，請選取 **[!UICONTROL 身分]** 在左側導覽中，然後選取 **[!UICONTROL 瀏覽]**.

![浏览器](./images/browse.png)

身分名稱空間清單會顯示在頁面的主要介面中，顯示有關其名稱、身分符號、上次更新日期以及是否為標準或自訂名稱空間的資訊。 右側欄包含的相關資訊 [!UICONTROL 身分圖表強度].

![身分](./images/identities.png)

Platform也提供名稱空間以進行整合。 預設會隱藏這些名稱空間，因為它們是用來連線其他系統，而不是用來拼接身分。 若要檢視整合名稱空間，請選取 **[!UICONTROL 檢視整合身分]**.

![view-integration-identities](./images/view-integration-identities.png)

從清單中選取身分名稱空間，以檢視特定名稱空間的資訊。 選取身分名稱空間會更新右側邊欄上的顯示，以顯示與您選取的身分名稱空間有關的中繼資料，包括擷取的身分數量以及失敗和略過的記錄數量。

![select-namespace](./images/select-namespace.png)

## 管理自訂名稱空間 {#manage-namespaces}

根據您的組織資料和使用案例，您可能需要自訂名稱空間。 自訂名稱空間可透過以下方式建立： [[!DNL Identity Service]](./api/create-custom-namespace.md) API或透過UI。

若要使用UI建立自訂名稱空間，請導覽至 **[!UICONTROL 身分]** 工作區，選取 **[!UICONTROL 瀏覽]**，然後選取 **[!UICONTROL 建立身分名稱空間]**.

![select-create](./images/select-create.png)

此 **[!UICONTROL 建立身分名稱空間]** 對話方塊隨即顯示。 提供唯一 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 身分符號]** 然後選取您要建立的身分型別。 您也可以新增選擇性說明，以新增有關名稱空間的進一步資訊。 所有身分型別，但不包括 **非人員識別碼** 會遵循相同的拼接行為。 如果您選取 **非人員識別碼** 作為身分型別，在建立名稱空間時不會進行拼接。 如需有關每種身分型別的特定資訊，請參閱以下表格： [身分型別](#identity-types).

完成後，選取 **[!UICONTROL 建立]**.

>[!IMPORTANT]
>
>您定義的名稱空間屬於貴組織專用，而且需要唯一的身分符號才能成功建立。

![create-identity-namespace](./images/create-identity-namespace.png)

與標準名稱空間類似，您可以從 **[!UICONTROL 瀏覽]** 標籤以檢視其詳細資訊。 不過，有了自訂名稱空間，您還可以從詳細資訊區域編輯其顯示名稱和說明。

>[!NOTE]
>
>建立名稱空間後，便無法刪除該名稱空間，也無法變更其身分符號和型別。

## 身分資料中的名稱空間

提供身分的名稱空間取決於您用來提供身分資料的方法。 如需有關提供資料身分資料的詳細資訊，請參閱以下章節： [提供身分資料](./home.md#supplying-identity-data-to-identity-service) 在 [!DNL Identity Service] 概述。

## 后续步骤

現在您已瞭解身分識別名稱空間的主要概念，可以開始瞭解如何使用身分識別圖表 [身分圖表檢視器](./ui/identity-graph-viewer.md).
