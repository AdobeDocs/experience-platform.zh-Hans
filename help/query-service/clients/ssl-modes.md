---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連線；連線到查詢服務；SSL；ssl；sslmode；
title: 查詢服務SSL選項
description: 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用驗證完整SSL模式連線。
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL選項

為了提高安全性，Adobe Experience Platform [!DNL Query Service] 為SSL連線提供原生支援，以加密使用者端/伺服器通訊。 本文介紹的協力廠商使用者端連線可用的SSL選項如下： [!DNL Query Service] 以及如何使用 `verify-full` SSL引數值。

## 先决条件

本檔案假設您已下載協力廠商案頭使用者端應用程式，以便與您的平台資料搭配使用。 在各自的連線指南檔案中可找到有關如何在與協力廠商使用者端連線時合併SSL安全性的特定指示。 用於所有清單 [!DNL Query Service] 支援的使用者端，請參閱 [使用者端連線概觀](./overview.md).

## 可用的SSL選項 {#available-ssl-options}

Platform支援各種SSL選項，以符合您的資料安全性需求，並平衡加密和金鑰交換的處理開銷。

不同的 `sslmode` 引數值可提供不同等級的保護。 使用SSL憑證加密您的資料，有助於防止「中間人」(MITM)攻擊、偷聽和模擬。 下表提供可用不同SSL模式的劃分及其提供的保護等級。

>[!NOTE]
>
> SSL值 `disable` 由於符合必要的資料保護規範，Adobe Experience Platform不支援此功能。

| sslmode | 竊聽保護 | MITM保護 | 描述 |
|---|---|---|---|
| `allow` | 部分 | 否 | 安全性不是優先考量，速度與低處理開銷更為重要。 只有在伺服器堅持使用加密時，這個模式才會選擇加密。 |
| `prefer` | 部分 | 否 | 不需要加密，但如果伺服器支援的話，通訊將會加密。 |
| `require` | 是 | 否 | 所有通訊都需要加密。 信任網路可連線到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `verify-ca` | 是 | 取決於CA原則 | 所有通訊都需要加密。 必須先進行伺服器驗證，才能共用資料。 這要求您設定根憑證於 [!DNL PostgreSQL] 主目錄。 [詳情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通訊都需要加密。 必須先進行伺服器驗證，才能共用資料。 這要求您設定根憑證於 [!DNL PostgreSQL] 主目錄。 [詳情如下](#instructions). |

>[!NOTE]
>
>兩者之間的差異 `verify-ca` 和 `verify-full` 取決於根憑證授權單位(CA)的原則。 如果您已建立自己的本機CA來核發應用程式的私人憑證，請使用 `verify-ca` 通常提供足夠的保護。 如果使用公用CA， `verify-ca` 允許連線到其他人可能已向CA註冊的伺服器。 `verify-full` 應一律搭配公用根CA使用。

在建立與平台資料庫的協力廠商連線時，建議您使用 `sslmode=require` 至少要確保傳輸中資料的安全連線。 此 `verify-full` 建議將SSL模式用於大多數安全性敏感型環境。

## 設定伺服器驗證的根憑證 {#root-certificate}

為了確保安全連線，在建立連線之前，必須在使用者端和伺服器上設定SSL使用方式。 如果只在伺服器上設定SSL，則使用者端可能會在確定伺服器需要高度安全性之前傳送機密資訊，例如密碼。

依預設， [!DNL PostgreSQL] 不執行伺服器憑證的任何驗證。 驗證伺服器的身分並確保在任何敏感資料傳送之前有安全連線（作為SSL的一部分） `verify-full` 模式)，則您必須在本機電腦上放置根（自我簽署）憑證(`root.crt`)和伺服器上根憑證簽署的分葉憑證。

如果 `sslmode` 引數已設為 `verify-full`，libpq會透過檢查憑證鏈結一直到儲存在使用者端上的根憑證來驗證伺服器是否值得信任。 然後它會驗證主機名稱是否符合伺服器憑證中儲存的名稱。

若要允許伺服器憑證驗證，您必須放置一個或多個根憑證(`root.crt`)中 [!DNL PostgreSQL] 檔案時。 檔案路徑會類似於 `~/.postgresql/root.crt`.

## 啟用驗證完整SSL模式以供第三方使用 [!DNL Query Service] 連線 {#instructions}

如果您需要更嚴格的安全性控制 `sslmode=require`，您可以依照醒目提示的步驟，將協力廠商使用者端連線至 [!DNL Query Service] 使用 `verify-full` SSL模式。

>[!NOTE]
>
>取得SSL憑證有許多選項。 由於流氓憑證的趨勢日益發展，本指南中使用DigiCert，因為他們是高保證TLS/SSL、PKI、IoT和簽署解決方案的可信全球提供者。

1. 導覽至 [可用的DigiCert根憑證清單](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 搜尋&quot;[!DNL DigiCert Global Root CA]」從可用憑證清單。
1. 選取 [!DNL **下載PEM**] 將檔案下載至本機電腦。
   ![反白顯示「下載PEM」的可用DigiCert根憑證清單。](../images/clients/ssl-modes/digicert.png)
1. 將安全性憑證檔案重新命名為 `root.crt`.
1. 將檔案複製到 [!DNL PostgreSQL] 資料夾。 必要的檔案路徑會因您的作業系統而異。 如果該資料夾尚不存在，請建立該資料夾。
   - 如果您使用macOS，路徑為 `/Users/<username>/.postgresql`
   - 如果您使用的是Windows，則路徑為 `%appdata%\postgresql`

>[!TIP]
>
>尋找您的 `%appdata%` 檔案在Windows作業系統上的位置，按⊞ **Win + R** 和輸入 `%appdata%` 至搜尋欄位。

晚於 [!DNL DigiCert Global Root CA] CRT檔案可在 [!DNL PostgreSQL] 資料夾，您可以連線至 [!DNL Query Service] 使用 `sslmode=verify-full` 或 `sslmode=verify-ca` 選項。

## 后续步骤

閱讀本檔案後，您對連線協力廠商使用者端的可用SSL選項有了更深入的瞭解 [!DNL Query Service]，以及如何啟用 `verify-full` SSL選項，可動態加密您的資料。

如果您尚未這麼做，請遵循以下指南： [連線協力廠商使用者端至 [!DNL Query Service]](./overview.md).
