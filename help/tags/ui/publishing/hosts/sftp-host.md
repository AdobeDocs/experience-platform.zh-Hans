---
title: SFTP 主机
description: 瞭解如何在Adobe Experience Platform中設定標籤，以將程式庫組建傳送至安全的自行託管SFTP伺服器。
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 19%

---

# SFTP主機

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

Adobe Experience Platform可讓您將標籤程式庫組建傳送至您自行託管的安全SFTP伺服器，讓您更能掌控組建的儲存和管理方式。 本指南說明如何在Experience PlatformUI或資料收集UI中為標籤屬性設定SFTP主機。

>[!NOTE]
>
>您也可以選擇改用Adobe管理的主機。 請參閱指南： [Adobe管理主機](./managed-by-adobe-host.md) 以取得詳細資訊。
>
>如需自行託管程式庫的優點與限制的詳細資訊，請參閱 [自行託管指南](./self-hosting-libraries.md).

## 設定伺服器的存取金鑰 {#access-key}

Platform 会使用加密密钥连接到 SFTP 站点。可以通过以下几步来正确设置此操作：

### 建立公開/私密金鑰組

您必须在 SFTP 服务器上安装公钥/私钥对。您可以在伺服器上產生這些金鑰，也可以在其他地方產生金鑰並安裝在伺服器上。 請參閱GitHub檔案，瞭解 [如何產生SSH金鑰](https://help.github.com/cn/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) 以取得詳細資訊。

### 加密您的金鑰

私密金鑰是用來加密公開金鑰。 在SFTP主機建立過程中，您需要提供私密金鑰。 請參閱以下小節： [加密值](../../../api/guides/encrypting-values.md) Reactor API指南中取得加密公開金鑰的指示。 使用生產環境的GPG金鑰，除非您知道您需要特定金鑰。 最后，您可以从任何计算机加密私钥，您无需在服务器上安装 GPG 即可完成此步骤。

### 允許清單平台IP位址

您可能需要核准一組IP位址，以便在公司防火牆內使用，以允許Platform連線您的SFTP伺服器並進行連線。 這些IP位址包括：

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>標籤組建的結構已隨著時間而改變。 它们在内部使用符号链接来保持向后兼容性，以便之前嵌入的代码可以继续与最新的内部版本结构配合使用。您的SFTP伺服器必須支援使用symlink，才能當做標籤組建的有效目的地。

如需更多詳細資訊，請參閱以下媒體文章： [如何設定SFTP伺服器以傳遞組建](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## 创建 SFTP 主机 {#create}

選取 **[!UICONTROL 主機]** 在左側導覽列中，後面接著 **[!UICONTROL 新增主機]**.

![此影像顯示正在UI中選取新增主機按鈕](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

主機建立對話方塊隨即顯示。 提供主機的名稱，並在 **[!UICONTROL 型別]**，選取 **[!UICONTROL SFTP]**.

![顯示正在選取SFTP託管選項的影像](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### 設定SFTP主機 {#configure}

此對話方塊會展開，包含SFTP主機的其他設定選項。 下文將說明這些內容。

![顯示SFTP主機連線所需詳細資料的影像](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 設定欄位 | 描述 |
| --- | --- |
| [!UICONTROL 不要使用符號連結] | 依預設，所有SFTP主機都會使用符號連結（符號連結）來參考程式庫 [組建](../builds.md) 已儲存至伺服器的虛擬報表套裝。 不過，並非所有伺服器都支援使用symlink。 選取此選項時，主機會使用複製操作直接更新組建資產，而非使用符號連結。 |
| [!UICONTROL SFTP伺服器URL] | 伺服器的URL基底路徑。 |
| [!UICONTROL 路径] | 要附加至此主機之基本伺服器URL的路徑。 |
| [!UICONTROL 端口] | 端口必须是以下端口之一：<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>作为最佳安全做法，Adobe 会限制用于传出流量的端口数量。通常允許選取的連線埠通過公司防火牆，並包含一些彈性範圍。 |
| [!UICONTROL 用户名] | 存取伺服器時要使用的使用者名稱。 |
| [!UICONTROL 加密的私密金鑰] | 您在中建立的加密私密金鑰 [上一步](#access-key). |

選取 **[!UICONTROL 儲存]** 以使用選取的組態建立主機。

![顯示正在儲存的SFTP主機的影像](../../../images/ui/publishing/sftp-hosts/save-host.png)

當您選取 **[!UICONTROL 儲存]**，則會測試連線以及將檔案傳送至SFTP伺服器的能力。 Platform會建立資料夾、在該資料夾中寫入檔案、檢查檔案是否確實存在，然後自行清除。 若您SFTP伺服器上的使用者帳戶（與您提供給Platform的安全憑證連結的帳戶）沒有執行此動作的必要許可權，則主機會進入「失敗」狀態。

## 后续步骤

本指南說明如何設定自家託管的SFTP伺服器，以用於標籤。 建立主機後，您就可以將其與您的一個或多個建立關聯。 [環境](../environments.md) 用於發佈標籤庫。 如需在網頁或行動屬性上啟用標籤功能高層級流程的詳細資訊，請參閱 [發佈概觀](../overview.md).
