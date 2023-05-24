---
title: 錯誤處理
description: 瞭解如何在Reactor API中處理錯誤。
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 錯誤處理

呼叫Reactor API時發生問題時，可能會以下列其中一種方式傳回錯誤：

* **立即錯誤**：執行導致立即錯誤的請求時，API會傳回錯誤回應，且HTTP狀態會反映所發生的一般錯誤型別。
* **延遲的錯誤**：執行導致延遲錯誤（例如非同步活動）的API請求時，API可能會在 `meta.status_details` 相關資源的。

## 錯誤格式

錯誤回應旨在符合 [JSON：API錯誤規格](http://jsonapi.org/format/#errors)，且通常會遵循下列結構：

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 此特定問題發生次數的唯一識別碼。 |
| `status` | 適用於此問題的HTTP狀態代碼，以字串值表示。 |
| `code` | 應用程式專屬的錯誤代碼，以字串值表示。 |
| `title` | 簡短、易懂的問題摘要，其中 **不應變更** 從一次事件到一次事件，但本地化目的除外。 |
| `detail` | 此問題發生的特定說明，可供使用者讀取。 按讚 `title`，此欄位的值可翻譯。 |
| `source` | 一個物件，其中包含對錯誤來源的參照，可選擇性地包括下列任何成員：<ul><li>`pointer`：a [JSON指標(RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) 在請求檔案中參考關聯實體的字串(例如 `/data` 主要資料物件的，或 `/data/attributes/title` 特定屬性)。</li></ul> |
| `meta` | 包含有關錯誤的非標準中繼資料的物件。 |

{style="table-layout:auto"}

## 錯誤參考

下表列出API可傳回的不同錯誤。

| 錯誤標題 | 描述 |
| --- | --- |
| `authentication-failure` | 您的IMS存取權杖無效。 您可以再次登入以取得新的存取Token。 或針對技術帳戶，產生新的JWT並交換IMS存取權杖。 |
| `connection-refused` | 無法建立伺服器連線。 |
| `decrypt-bad-passphrase` | 無法使用提供的密碼解密。 |
| `decrypt-failed` | 無法使用提供的私密金鑰解密資料。 確保金鑰在本機運作，且空白字元已修剪。 |
| `decrypt-no-data` | 沒有私密金鑰無法解密資料。 請提供加密的私密金鑰。 |
| `delegate-descriptor-unresolved` | 擴充功能未提供此委派描述項的預期定義。 擴充功能可能需要更新。 |
| `deleted-resources` | 您嘗試新增至程式庫的資源已刪除。 |
| `environment-in-use` | 一個環境一次只能指派給一個程式庫。 選項1是選擇不同的環境。 選項2是將程式庫移至其他環境或刪除程式庫，以釋放此環境。 |
| `environment-required` | 在建立組建之前，您的程式庫必須已指派環境。 |
| `extension-not-found` | 定義資料元素或規則元件的擴充功能不會包含在程式庫中。 確認已將所有必要的擴充功能新增至程式庫。 |
| `extension-package-path-error` | extension.json中定義的路徑建構不正確。 |
| `extension-package-transform-definition-error` | 您已經為物件屬性定義了無效的轉換。 每個物件屬性都可以定義一個轉換，而且它必須是檔案轉換或函式轉換。 |
| `extension-package-zip-error` | 解壓縮ExtensionPackage或壓縮檔案以進行發佈時發生錯誤。 |
| `host-in-use` | 如果一個或多個環境正在使用主機，則無法刪除主機。 |
| `host-required` | 指派給此程式庫的環境沒有有效主機。 檢查指派給程式庫的環境。 然後將有效的主機指派給該環境。 |
| `host-type-error` | 只有SFTP主機需要先驗證認證才能使用，因此預先測試僅適用於該主機型別。 |
| `illegal-custom-code-transform` | 您不得使用customCode轉換。 請指定函式或檔案轉換。 |
| `ims-not-authorized` | 授權您的帳戶時發生未知錯誤。 請稍後再試。 |
| `ims-session-error` | 登入工作階段發生問題。 請登出並重新登入。 |
| `internal-error` | 發生內部錯誤。 請稍候幾分鐘，然後再試一次。 如果問題仍然存在，請聯絡客戶服務。 |
| `invalid-data_element` | 無法將無效的資料元素新增至程式庫。 |
| `invalid-embed_code` | 這不是有效的內嵌程式碼，或是您嘗試將其連結至開發或中繼環境。 Dynamic Tag Management (DTM)內嵌程式碼只能連結至生產環境。 |
| `invalid-extension` | 無法將無效的擴充功能新增至程式庫。 |
| `invalid-extension_package_id` | 您只能修改擴充功能套件的部分物件屬性。 您嘗試修改其中一個不允許的專案。 |
| `invalid-new-owner-org-id` | 您嘗試指派的組織ID不是有效的組織ID。 |
| `invalid-org` | 您的作用中組織無權存取API。 檢查您使用的組織是否正確。 |
| `invalid-rule` | 無法將無效的規則新增至程式庫。 |
| `invalid-settings-syntax` | 剖析設定JSON時遇到語法錯誤。 |
| `library-file-not-found` | 在zip套件中找不到extension.json中定義的必要檔案。 |
| `minification-error` | 由於程式碼無效，無法編譯程式碼。 |
| `multiple-revisions` | 程式庫中只能包含每個資源的一個修訂版本。 |
| `no-available-orgs` | 此使用者帳戶不屬於可存取標籤的產品設定檔。 使用Admin Console將此使用者新增至具有標籤許可權的產品設定檔。 |
| `not-authorized` | 此使用者帳戶沒有執行此動作的必要許可權。 |
| `not-found` | 找不到記錄。 驗證您嘗試擷取的物件ID。 |
| `not-unique` | 您嘗試使用的名稱已在使用中。 對於此資源，「name」屬性必須是唯一的。 |
| `public-release-not-authorized` | 擴充功能的公開發行協調方： `launch-ext-dev@adobe.com`. 檢視檔案： [發行擴充功能](../../extension-dev/submit/release.md) 以取得詳細資訊。 |
| `read-only` | 此資源為唯讀資源，無法修改。 |
| `session-timeout` | 使用者工作階段已過期。 請登出並重新登入。 |
| `sftp-authentication-failed` | SFTP連線的驗證失敗。 |
| `sftp-connection-timeout` | SFTP連線已逾時。 |
| `sftp-exception` | 使用SFTP連線至伺服器時發生例外狀況。 |
| `sftp-status-exception` | 嘗試與伺服器通訊時發生SFTP例外狀況。 |
| `socket-error` | 嘗試與伺服器通訊時發生通訊端錯誤。 |
| `ssh-disconnect` | SSH工作階段已中斷。 |
| `timeout-error` | 與伺服器的連線逾時。 |
| `unknown-error` | 發生非預期的錯誤。 您可以稍後再試一次，或打電話給客戶服務，說明您剛才在做什麼。 |
| `unsupported-custom-code-language` | 提供的自訂程式碼語言不受支援。 |
| `upgraded-extension-required` | 安裝擴充功能升級後，您必須將其納入所有程式庫，直到升級至生產環境為止。 唯一的例外是擴充功能尚未發佈。 |
| `upstream-build-required` | 您必須先成功建置上遊程式庫，才能建置此程式庫。 |

{style="table-layout:auto"}
