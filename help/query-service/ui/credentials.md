---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務認證指南
description: Adobe Experience Platform查詢服務提供使用者介面，可用於寫入和執行查詢、檢視以前執行的查詢，以及存取由您組織內的使用者儲存的查詢。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# 認證指南

Adobe Experience Platform查詢服務可讓您與外部使用者端連線。 您可以使用即將到期的認證或不即將到期的認證來連線到這些外部使用者端。

## 即將到期的認證 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="客户端的 SSL 模式"
>abstract="必须在连接到查询服务的客户端中启用 SSL。确保 SSL 模式设置为“要求”。"

您可以使用即將到期的認證來快速設定與外部使用者端的連線。

![「查詢儀表板認證」索引標籤中會反白顯示「即將到期的認證」區段。](../images/ui/credentials/expiring-credentials.png)

此 **[!UICONTROL 即將到期的認證]** 一節提供下列資訊：

- **[!UICONTROL 主機]**：要將使用者端連線至的主機名稱。 這會合併您的組織名稱，如同在Platform UI的頂端功能區中所見。
- **[!UICONTROL 連線埠]**：要連線之主機的連線埠號碼。
- **[!UICONTROL 資料庫]**：要連線使用者端的資料庫名稱。
- **[!UICONTROL 使用者名稱]**：用來連線至查詢服務的使用者名稱。
- **[!UICONTROL 密碼]**：用來連線至查詢服務的密碼。 UI中的密碼已進行雜湊處理，以提供安全性。 選取復製圖示(![復製圖示。](../images/ui/credentials/copy-icon.png))，將完整、未雜湊的認證複製到剪貼簿。
- **[!UICONTROL PSQL命令]**：自動插入所有相關資訊的命令，讓您在命令列上使用PSQL連線至Query Service。
- **[!UICONTROL 過期]**：即將到期的認證的到期日期和時間。 權杖的預設有效期間為24小時，但可在Admin Console的進階設定中變更。

>[!TIP]
>
>若要變更「查詢服務」之到期認證連線的工作階段期限，請瀏覽至 [Admin Console](https://adminconsole.adobe.com/) 並選取下列熒幕選項： **設定** > **隱私權與安全性** > **驗證設定** > **進階設定** > **最長工作階段期限**.
>
>![反白顯示「隱私權與安全性」、「驗證設定」和「最長工作階段期限」的「Admin Console設定」索引標籤。](../images/ui/credentials/max-session-life.png)
>
>請參閱Adobe說明檔案，以瞭解有關 [進階設定](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) 由Admin Console提供。

## 不會到期的認證 {#non-expiring-credentials}

您可以使用不會到期的認證來設定與外部使用者端更永久的連線。

### 先决条件

您必須先在Adobe Admin Console中完成下列步驟，才能產生不會到期的認證：

1. 登入 [Adobe Admin Console](https://adminconsole.adobe.com/) 並從上方導覽列中選取相關組織。
2. [選取產品設定檔。](../../access-control/ui/browse.md)
3. [設定兩者 **沙箱** 和 **管理查詢服務整合** 許可權](../../access-control/ui/permissions.md) 用於產品設定檔。
4. [將新使用者新增至產品設定檔](../../access-control/ui/users.md) 因此會授予他們已設定的許可權。
5. [將使用者新增為產品設定檔管理員](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 允許為任何使用中產品設定檔建立帳戶。
6. [將使用者新增為產品設定檔開發人員](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html) 以便建立整合。

若要進一步瞭解如何指派許可權，請閱讀以下檔案： [存取控制](../../access-control/home.md).

現在，所有必要的許可權都已在Adobe Developer Console中設定，以便使用者使用即將到期的認證功能。

### 產生認證

若要建立一組不會到期的認證，請返回Platform UI並選擇 **[!UICONTROL 查詢]** 從左側導覽存取 [!UICONTROL 查詢] 工作區。 接下來，選取 **[!UICONTROL 認證]** 索引標籤後接 **[!UICONTROL 產生認證]**.

![「查詢」控制面板中反白了「認證」標籤和「產生認證」。](../images/ui/credentials/generate-credentials.png)

會出現一個對話方塊，讓您產生認證。 若要建立不會到期的證明資料，您必須提供下列詳細資訊：

- **[!UICONTROL 名稱]**：您產生的認證名稱。
- **[!UICONTROL 說明]**：（選用）您產生之認證的說明。
- **[!UICONTROL 指派給]**：將指派認證的使用者。 此值應為建立認證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （選用）憑證的選用密碼。 如果未設定密碼，Adobe會自動為您產生密碼。

提供所有必要的詳細資訊後，請選取 **[!UICONTROL 產生認證]** 以產生您的認證。

![[Generate credentials]對話方塊會反白顯示。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>時間 **[!UICONTROL 產生認證]** ，則會將設定JSON檔案下載至您的本機電腦。 因為Adobe會 **not** 記錄產生的認證，您必須安全地儲存下載的檔案，並保留認證的記錄。
>
>此外，如果認證已有90天未使用，則會將認證清除。

設定JSON檔案包含技術帳戶名稱、技術帳戶ID和認證等資訊。 其提供格式如下。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

儲存產生的認證後，選取 **[!UICONTROL 關閉]**. 您現在可以看到所有不會到期的認證清單。

![「查詢儀表板認證」索引標籤中反白了「不會到期的認證」區段。](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除不會到期的認證。 若要編輯不會到期的認證，請選取鉛筆圖示(![鉛筆圖示。](../images/ui/credentials/edit-icon.png))。若要刪除不會到期的認證，請選取刪除圖示(![垃圾桶圖示。](../images/ui/credentials/delete-icon.png))。

編輯不會到期的認證時，強制回應視窗會出現。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**：您產生的認證名稱。
- **[!UICONTROL 說明]**：（選用）您產生之認證的說明。
- **[!UICONTROL 指派給]**：將指派認證的使用者。 此值應為建立認證之使用者的電子郵件地址。

![更新帳戶對話方塊。](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資訊後，請選取 **[!UICONTROL 更新帳戶]** 以完成認證的更新。

## 使用認證來連線到外部使用者端 {#use-credential-to-connect}

您可以使用到期或不到期的認證來連線到外部使用者端，例如Aqua Data Studio、Looker或Power BI。 這些憑證的輸入方法會因外部使用者端而異。 請參閱外部使用者端檔案，取得使用這些憑證的特定指示。

此影像會指出在UI中找到的每個引數的位置，但不包括不會到期的認證的密碼。 雖然不會到期的認證是由其JSON設定檔案所提供，但您可以在底下檢視即將到期的認證 **認證** UI中的Tab鍵。

![「查詢」工作區的「認證」索引標籤中反白了「即將到期的認證」區段。](../images/ui/credentials/expiring-credentials.png)

下表概述連線至外部使用者端通常所需的引數。

>[!NOTE]
>
>使用不會到期的證明資料連線到主機時，仍需使用 [!UICONTROL 即將到期的認證] 區段，但密碼和使用者名稱除外。
>輸入使用者名稱和密碼的格式使用冒號分隔值，如本範例所示 `username:{your_username}` 和 `password:{password_string}`.

| 参数 | 描述 | 示例 |
|---|---|---|
| **伺服器/主機** | 您要連線的伺服器/主機名稱。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，其形式為 `server.adobe.io`. 值位於 **[!UICONTROL 主機]** 在 [!UICONTROL 即將到期的認證] 區段。</ul></li> | `acme.platform.adobe.io` |
| **端口** | 您要連線的伺服器/主機連線埠。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，並位於下方 **[!UICONTROL 連線埠]** 在 [!UICONTROL 即將到期的認證] 區段。</ul></li> | `80` |
| **数据库** | 您正在連線的資料庫。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，並會發現於 **[!UICONTROL 資料庫]** 在 [!UICONTROL 即將到期的認證] 區段。 </ul></li> | `prod:all` |
| **用户名** | 連線至外部使用者端的使用者使用者名稱。 <ul><li>此值會用於即將到期的認證和不即將到期的認證。 它以前採用英數字串的形式 `@AdobeOrg`. 此值位於 **[!UICONTROL 使用者名稱]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **密码** | 連線到外部使用者端的使用者密碼。 <ul><li>如果您使用即將到期的認證，您可在下列位置找到： **[!UICONTROL 密碼]** 在 [!UICONTROL 即將到期的認證] 區段。</li><li>如果您使用不會到期的認證，此值是從technicalAccountID串連的引數，以及從設定JSON檔案取得的認證。 密碼值採用以下形式： `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>即將到期的認證密碼超過一千個字元的英數字串。 將不會提供範例。</li><li>不會到期的認證密碼如下：<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 后续步骤

現在您已瞭解即將到期和未到期的認證如何運作，您可以使用這些認證連線到外部使用者端。 如需有關外部使用者端的詳細資訊，請參閱 [連線使用者端至查詢服務指南](../clients/overview.md).
