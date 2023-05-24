---
keywords: Experience Platform；疑難排解；資料科學工作區；熱門主題
solution: Experience Platform
title: Data Science Workspace疑難排解指南
description: 本檔案提供有關Adobe Experience Platform資料科學工作區的常見問題解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑難排解指南

本檔案提供有關Adobe Experience Platform常見問題的解答 [!DNL Data Science Workspace]. 有關下列專案的問題和疑難排解： [!DNL Platform] API一般而言，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

## JupyterLab Notebook查詢狀態卡在執行狀態

JupyterLab Notebook可能表示儲存格在某些記憶體不足的情況下無限期處於執行狀態。 例如，在查詢大型資料集或執行多個後續查詢時，JupyterLab Notebook的可用記憶體可能會用盡以儲存產生的資料流物件。 在此情況下可以看到一些指標。 首先，即使儲存格顯示為executing，核心也會進入閒置狀態。 [`*`] 圖示加以儲存。 此外，底部列會指出已使用/可用的RAM數量。

![可用的ram](./images/jupyterlab/user-guide/allocate-ram.png)

在讀取資料期間，記憶體可能會增加，直到達到您配置的最大記憶體數量。 當達到最大記憶體且核心重新啟動時，就會釋放記憶體。 這表示在此情況下使用的記憶體可能會因為核心重新啟動而顯示為非常低，而在重新啟動之前，記憶體會非常接近配置的最大RAM。

若要解決此問題，請選取JupyterLab右上方的齒輪圖示，並將滑桿滑至右側，然後選取 **[!UICONTROL 更新設定]** 以配置更多RAM。 此外，如果您正在執行多個查詢，而RAM值接近配置的最大量，除非您需要先前查詢的結果，請重新啟動核心以重設可用的RAM量。 這可確保您擁有可用於目前查詢的最大RAM量。

![配置更多ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

如果您正在配置最大記憶體(RAM)量且仍然遇到此問題，您可以透過減少資料行或資料範圍，修改查詢以在較小的資料集大小上操作。 若要使用完整的資料量，建議您使用Spark筆記本。

## [!DNL JupyterLab] 環境未載入 [!DNL Google Chrome]

>[!IMPORTANT]
>
>此問題已解決，但可能仍存在於Google Chrome 80.x瀏覽器中。 請確定您的Chrome瀏覽器為最新狀態。

使用 [!DNL Google Chrome] 瀏覽器80.x版預設會封鎖所有第三方Cookie。 此原則可防止 [!DNL JupyterLab] ，以免在Adobe Experience Platform中載入。

若要修正此問題，請使用下列步驟：

在您的 [!DNL Chrome] 瀏覽器，導覽至右上角並選取 **設定** (您也可以複製並貼上位址列中的「chrome://settings/」)。 接下來，捲動至頁面底部，然後按一下 **進階** 下拉式清單。

![chrome advanced](./images/faq/chrome-advanced.png)

此 **隱私權與安全性** 區段隨即顯示。 接下來，按一下 **網站設定** 後面接著 **Cookie和網站資料**.

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

最後，將「封鎖第三方Cookie」切換為「關閉」。

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您可以停用第三方Cookie並新增 [*.]ds.adobe.net加入允許清單。

導覽至網址列中的「chrome://flags/」。 搜尋和停用標示為的標幟 *&quot;預設SameSite Cookie&quot;* 使用右側的下拉式功能表。

![停用samesite標幟](./images/faq/samesite-flag.png)

在步驟2之後，系統會提示您重新啟動瀏覽器。 你重新啟動後， [!DNL Jupyterlab] 應為可存取。

## 為什麼我無法存取 [!DNL JupyterLab] 使用Safari嗎？

Safari預設會在Safari &lt; 12中停用第三方Cookie。 因為您的 [!DNL Jupyter] 虛擬機器器執行個體位在與上層框架不同的網域上，Adobe Experience Platform目前要求啟用協力廠商Cookie。 請啟用第三方Cookie或切換至其他瀏覽器，例如 [!DNL Google Chrome].

若使用Safari 12，您必須將使用者代理程式切換為&#39;[!DNL Chrome]&#39;或&#39;[!DNL Firefox]&#39;. 若要切換使用者代理程式，請開啟 *Safari* 功能表並選取 **偏好設定**. 偏好設定視窗隨即出現。

![Safari偏好設定](./images/faq/preferences.png)

在Safari偏好設定視窗中，選取 **進階**. 然後檢視 *在功能表列中顯示[開發]功能表* 方塊。 完成此步驟後，您可以關閉偏好設定視窗。

![Safari進階](./images/faq/advanced.png)

接下來，從頂端導覽列中選取 **開發** 功能表。 從 **開發** 下拉式清單，暫留在 **使用者代理**. 您可以選取 **[!DNL Chrome]** 或 **[!DNL Firefox]** 您要使用的使用者代理字串。

![開發功能表](./images/faq/user-agent.png)

## 為什麼我嘗試上傳或刪除中的檔案時會看到「403禁止」訊息 [!DNL JupyterLab]？

如果您的瀏覽器已啟用廣告封鎖軟體，例如 [!DNL Ghostery] 或 [!DNL AdBlock] 此外，每個廣告封鎖軟體都必須允許網域「\*.adobe.net」 [!DNL JupyterLab] 以正常運作。 這是因為 [!DNL JupyterLab] 虛擬機器器在與「 」不同的網域上執行 [!DNL Experience Platform] 網域。

## 為什麼我的某些部分 [!DNL Jupyter Notebook] 看起來很混亂或不演算為程式碼？

如果意外地將相關儲存格從「代碼」變更為「Markdown」，就可能發生這種情況。 聚焦程式碼儲存格時，按下按鍵組合 **ESC+M** 將儲存格型別變更為Markdown。 儲存格的型別可以透過所選儲存格之筆記本頂端的下拉式指示器來變更。 若要將儲存格型別變更為程式碼，請從選取您要變更的指定儲存格開始。 接下來，按一下指出儲存格目前型別的下拉式清單，然後選取「代碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂 [!DNL Python] 資料庫？

此 [!DNL Python] kernel已預先安裝許多常用的機器學習程式庫。 不過，您可以在程式碼儲存格中執行以下命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

如需預先安裝的完整清單 [!DNL Python] 程式庫，請參閱 [JupyterLab使用手冊的附錄區段](./jupyterlab/overview.md#supported-libraries).

## 我可以安裝自訂PySpark程式庫嗎？

很遺憾，您無法為PySpark核心安裝其他程式庫。 不過，您可以聯絡Adobe客戶服務代表，為您安裝自訂PySpark程式庫。

如需預先安裝的PySpark程式庫的清單，請參閱 [JupyterLab使用手冊的附錄區段](./jupyterlab/overview.md#supported-libraries).

## 是否可以設定 [!DNL Spark] 的叢集資源 [!DNL JupyterLab] [!DNL Spark] 或PySpark核心？

您可以將下列區塊新增至筆記本的第一個儲存格來設定資源：

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

如需詳細資訊，請參閱 [!DNL Spark] 叢集資源設定，包括可設定屬性的完整清單，請參閱 [JupyterLab使用手冊](./jupyterlab/overview.md#kernels).

## 嘗試執行較大資料集的某些任務時，為什麼會收到錯誤？

如果您收到錯誤的原因，例如 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 這通常表示驅動程式或執行器的記憶體不足。 請參閱JupyterLab Notebooks [資料存取](./jupyterlab/access-notebook-data.md) 檔案，以取得資料限制及如何在大型資料集上執行任務的詳細資訊。 通常此錯誤可透過變更 `mode` 從 `interactive` 至 `batch`.

此外，在撰寫大型Spark/PySpark資料集時，請快取您的資料(`df.cache()`)，然後執行寫入程式碼可以大幅改善效能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在讀取資料時遇到問題，並且正在將轉換套用至資料，請嘗試在轉換之前快取您的資料。 快取您的資料可防止跨網路多次讀取。 從讀取資料開始。 接下來，快取(`df.cache()`)資料。 最後，執行轉換。

## 我的Spark/PySpark筆記型電腦為何要花這麼長時間來讀取和寫入資料？

如果您要對資料執行轉換，例如使用 `fit()`，轉換可能會執行多次。 若要提高效能，請使用 `df.cache()` 執行 `fit()`. 這樣可確保只執行一次轉換，並防止跨網路多次讀取。

**建議的順序：** 從讀取資料開始。 接下來，執行轉換，然後進行快取(`df.cache()`)資料。 最後，執行 `fit()`.

## 為什麼我的Spark/PySpark筆記型電腦無法執行？

如果您收到下列任何錯誤：

- 工作已中止，因為中繼失敗……只能壓縮每個磁碟分割中具有相同元素數量的RDD。
- 遠端RPC使用者端已解除關聯和其他記憶體錯誤。
- 讀取和寫入資料集時效能不佳。

檢查以確定您正在快取資料(`df.cache()`)，然後再寫入資料。 在Notebooks中執行程式碼時，使用 `df.cache()` 在動作(例如 `fit()` 可大幅提升筆記型電腦效能。 使用 `df.cache()` 在寫入資料集之前，請確定轉換只會執行一次，而非多次。

## [!DNL Docker Hub] 限制資料科學工作區中的限制

自2020年11月20日起，匿名和免費驗證使用Docker Hub的費率限制已生效。 匿名且免費 [!DNL Docker Hub] 每六小時，使用者最多只能收到100個容器影像提取請求。 如果您受這些變更影響，您將會收到此錯誤訊息： `ERROR: toomanyrequests: Too Many Requests.` 或 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

目前，此限制只會在您嘗試在六小時內建立100部配方筆記型電腦，或是您在資料科學工作區中使用經常擴充和縮減的Spark筆記型電腦時，才會影響您的組織。 不過，這不太可能，因為這些執行所在的叢集在閒置之前會維持作用中兩個小時。 這減少了叢集處於作用中狀態時所需的提取次數。 如果您收到上述任何錯誤，則需要等到您的 [!DNL Docker] 限制已重設。

如需有關的詳細資訊 [!DNL Docker Hub] 速率限制，請造訪 [DockerHub檔案](https://www.docker.com/increase-rate-limits). 我們正在研究此問題的解決方案，預計會在後續版本中推出。
