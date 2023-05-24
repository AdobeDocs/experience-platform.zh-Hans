---
keywords: Experience Platform；JupyterLab；筆記型電腦；資料科學工作區；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的網頁式使用者介面，並緊密整合至Adobe Experience Platform。 它提供互動式開發環境，讓資料科學家能夠使用Jupyter Notebooks、程式碼和資料。 本檔案概述JupyterLab及其功能，以及執行常見動作的指示。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI總覽

[!DNL JupyterLab] 是Web型使用者介面，用於 [Jupyter專案](https://jupyter.org/) 並緊密整合至Adobe Experience Platform。 它提供互動式開發環境，讓資料科學家能夠使用Jupyter Notebooks、程式碼和資料。

本檔案提供下列專案的概觀： [!DNL JupyterLab] 及其功能，以及執行常見動作的指示。

## [!DNL JupyterLab] 於 [!DNL Experience Platform]

Experience Platform的JupyterLab整合可搭配架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫，以及Adobe主題的介面。

下列清單概述JupyterLab on Platform的獨特功能：

| 功能 | 描述 |
| --- | --- |
| **核心** | 核心，提供筆記型電腦及其他 [!DNL JupyterLab] 前端能以不同的程式設計語言執行及內嵌程式碼。 [!DNL Experience Platform] 提供其他核心以支援中的開發 [!DNL Python]、R、PySpark和 [!DNL Spark]. 請參閱 [核心](#kernels) 區段以取得更多詳細資料。 |
| **資料存取** | 直接從存取現有的資料集 [!DNL JupyterLab] 全面支援讀寫功能。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您利用其他 [!DNL Platform] 直接從中取得服務 [!DNL JupyterLab]. 支援整合的完整清單可在以下連結的區段中取得： [與其他Platform服務整合](#service-integration). |
| **身份验证** | 除了 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab的內建安全性模型</a>，應用程式和Experience Platform之間的每次互動（包括平台服務對服務通訊）都會透過進行加密和驗證 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **开发库** | 在 [!DNL Experience Platform]， [!DNL JupyterLab] 提供預先安裝的程式庫，用於 [!DNL Python]、 R和PySpark。 請參閱 [附錄](#supported-libraries) 以取得支援程式庫的完整清單。 |
| **程式庫控制器** | 當您的需求缺乏預先安裝的程式庫時，可以為Python和R安裝其他程式庫，並暫時儲存在隔離的容器中，以保持 [!DNL Platform] 並確保資料安全。 請參閱 [核心](#kernels) 區段以取得更多詳細資料。 |

>[!NOTE]
>
>其他程式庫僅適用於已安裝程式庫的工作階段。 您必須重新安裝啟動新工作階段時所需的任何其他程式庫。

## 與其他整合 [!DNL Platform] 服務 {#service-integration}

標準化和互用性是背後的重要概念 [!DNL Experience Platform]. 整合 [!DNL JupyterLab] 於 [!DNL Platform] 作為內嵌IDE，可以與其他 [!DNL Platform] 服務，讓您能夠利用 [!DNL Platform] 充分發揮其潛力。 下列專案 [!DNL Platform] 以下位置提供服務： [!DNL JupyterLab]：

* **[!DNL Catalog Service]：** 使用讀取和寫入功能存取及探索資料集。
* **[!DNL Query Service]：** 使用SQL存取及探索資料集，可在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]：** 模型開發，能夠訓練及評分資料，以及按一下即可建立配方。
* **[!DNL Experience Data Model (XDM)]：** 標準化和互用性是Adobe Experience Platform背後的重要概念。 [體驗資料模型(XDM)](https://www.adobe.com/go/xdm-home-en)由Adobe推動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

>[!NOTE]
>
>部分 [!DNL Platform] 上的服務整合 [!DNL JupyterLab] 僅限特定核心。 請參閱以下章節： [核心](#kernels) 以取得更多詳細資料。

## 主要功能與常見操作

關於主要功能的資訊 [!DNL JupyterLab] 以下各節提供執行常見操作的說明：

* [存取JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [核心](#kernels)
* [核心階段作業](#kernel-sessions)
* [啟動器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)，選取 **[!UICONTROL Notebooks]** 左側導覽欄中的。 允許一些時間 [!DNL JupyterLab] 以完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

此 [!DNL JupyterLab] 介麵包含功能表列、可摺疊的左側邊欄，以及包含檔案和活動索引標籤的主要工作區域。

**菜单栏**

介面頂端的功能表列有頂層功能表，這些功能表會顯示 [!DNL JupyterLab] 使用鍵盤快速鍵：

* **檔案：** 與檔案和目錄相關的動作
* **編輯：** 與編輯檔案和其他活動相關的動作
* **檢視：** 變更外觀的動作 [!DNL JupyterLab]
* **執行：** 在不同活動（例如筆記型電腦和程式碼主控台）中執行程式碼的動作
* **核心：** 管理核心的動作
* **標籤：** 開啟的檔案和活動清單
* **設定：** 通用設定和進階設定編輯器
* **說明：** 清單 [!DNL JupyterLab] 與核心說明連結

**左側欄**

左側邊欄包含可點按的標籤，可讓您存取以下功能：

* **檔案瀏覽器：** 已儲存的筆記本檔案和目錄清單
* **資料總管：** 瀏覽、存取及探索資料集和結構描述
* **執行核心與終端機：** 具有終止能力的作用中核心與終端機階段作業清單
* **命令：** 有用的命令清單
* **儲存格檢測器：** 提供工具和中繼資料的存取的儲存格編輯器，可用於設定筆記本以進行簡報
* **索引標籤：** 開啟的標籤清單

選取標籤以公開其功能，或在展開的標籤上選取以摺疊左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區域**

中的主要工作區域 [!DNL JupyterLab] 可讓您將檔案和其他活動安排到標籤面板中，這些標籤面板可以調整大小或進行細分。 將索引標籤拖曳至索引標籤面板的中心以移轉索引標籤。 將標籤拖曳至面板的左側、右側、上方或底部，以分割面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 中的GPU和記憶體伺服器組態 [!DNL Python]/R

在 [!DNL JupyterLab] 選取右上角的齒輪圖示以開啟 *Notebook伺服器設定*. 您可以開啟GPU，並使用滑桿來分配所需的記憶體容量。 您可以配置的記憶體數量取決於您的組織已布建的記憶體數量。 選取 **[!UICONTROL 更新設定]** 以儲存。

>[!NOTE]
>
>每個組織只能布建一個GPU來使用Notebooks。 如果GPU正在使用中，您需要等待目前已保留GPU的使用者將其釋出。 登出或讓GPU處於閒置狀態四個小時以上，即可完成這項作業。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止和重新啟動 [!DNL JupyterLab]

在 [!DNL JupyterLab]，您可以終止工作階段以防止其他資源被使用。 從選取 **電源圖示** ![電源圖示](../images/jupyterlab/user-guide/power_button.png)，然後選取 **[!UICONTROL 關閉]** 從顯示終止工作階段的彈出視窗。 Notebook工作階段會在12小時沒有活動後自動終止。

若要重新啟動 [!DNL JupyterLab]，選取 **重新啟動圖示** ![重新啟動圖示](../images/jupyterlab/user-guide/restart_button.png) 位於電源圖示左側，然後選取 **[!UICONTROL 重新啟動]** 從出現的彈出視窗。

![終止jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 程式碼儲存格 {#code-cells}

程式碼儲存格是Notebooks的主要內容。 它們包含筆記型電腦相關核心語言的原始程式碼，以及執行程式碼儲存格後的輸出。 每個程式碼儲存格的右側會顯示執行計數，代表其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見的儲存格動作說明如下：

* **新增儲存格：** 按一下加號(**+**)，以新增空白儲存格。 新儲存格會放置在目前互動的儲存格下方，如果沒有特定儲存格成為焦點，則位於筆記本的結尾。

* **移動儲存格：** 將游標放在您要移動的儲存格右側，然後按一下並將儲存格拖曳到新位置。 此外，將儲存格從一個筆記本移至另一個筆記本，會複製儲存格及其內容。

* **執行儲存格：** 按一下要執行的儲存格內文，然後按一下 **play** 圖示(**▶**)。 星號(**\***)會在核心處理執行時顯示在儲存格的執行計數器中，並在完成後以整數取代。

* **刪除儲存格：** 按一下要刪除的儲存格內文，然後按一下 **剪刀** 圖示。

### 核心 {#kernels}

筆記型電腦核心是處理筆記型電腦儲存格的語言專屬運算引擎。 除了 [!DNL Python]， [!DNL JupyterLab] 在R、PySpark和 [!DNL Spark] (Scala)。 當您開啟筆記本檔案時，會啟動相關聯的核心。 執行notebook儲存格時，核心會執行計算並產生可能耗用大量CPU和記憶體資源的結果。 請注意，在關閉核心之前，不會釋放配置的記憶體。

某些特色和功能僅限於特定核心，如下表所述：

| 核心 | 程式庫安裝支援 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 核心階段作業 {#kernel-sessions}

上的每個使用中筆記本或活動 [!DNL JupyterLab] 會使用核心工作階段。 展開「 」，即可找到所有作用中的工作階段 **執行終端機與核心** tab鍵（從左側邊欄）。 您可以透過觀察筆記型電腦介面的右上角來識別筆記型電腦核心的型別和狀態。 在下圖中，筆記本的相關核心為 **[!DNL Python]3** 其目前狀態由右側的灰色圓圈表示。 空心圓表示閒置核心，實心圓表示忙碌核心。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果核心關機或長時間未啟用，則 **無核心！** 會顯示實心圓。 按一下核心狀態並選取適當的核心型別，以啟動核心，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自訂的 *啟動器* 提供支援的筆記型電腦核心的實用範本，協助您開始工作，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預先填入的筆記型電腦，示範使用範例資料進行資料探索。 |
| 零售業 | 預先填滿的筆記型電腦，具備 [零售指導方針](../pre-built-recipes/retail-sales.md) 使用範例資料。 |
| 配方產生器 | 用於建立配方的筆記本範本 [!DNL JupyterLab]. 它預先填入了示範和說明配方建立流程的程式碼和註解。 請參閱 [筆記本至配方教學課程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 以取得詳細逐步解說。 |
| [!DNL Query Service] | 預先填入的筆記型電腦，展示 [!DNL Query Service] 直接在 [!DNL JupyterLab] 提供大規模分析資料的工作流程範例。 |
| XDM事件 | 預先填寫的筆記型電腦，示範有關後值體驗事件資料的資料探索，著重於整個資料結構的共同功能。 |
| XDM查詢 | 預先填寫的筆記本，示範有關體驗事件資料的範例業務查詢。 |
| 聚合 | 預先填入的筆記型電腦，展示將大量資料彙總成可管理之較小區塊的範例工作流程。 |
| 聚类 | 預先填寫的筆記型電腦，示範使用叢集演演算法的端對端機器學習模型化程式。 |

有些筆記型電腦範本僅限於某些核心。 每個核心的範本可用性如下表所示：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入門者</strong></th>
        <th><strong>零售業</strong></th>
        <th><strong>配方產生器</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM查詢</strong></th>
        <th><strong>聚合</strong></th>
        <th><strong>聚类</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >否</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >是</td>
    </tr>
</table>

若要開啟新的 *啟動器*，按一下 **檔案>新增啟動器**. 或者，展開 **檔案瀏覽器** 然後按一下加號(**+**)：

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 后续步骤

若要進一步瞭解每部支援的筆記型電腦及其使用方法，請造訪 [Jupyterlab notebooks資料存取](./access-notebook-data.md) 開發人員指南。 本指南著重於如何使用JupyterLab Notebooks存取您的資料，包括讀取、寫入和查詢資料。 資料存取指南也包含每個支援筆記型電腦可讀取的最大資料量資訊。

## 支援的程式庫 {#supported-libraries}

如需Python、R和PySpark支援的套件清單，請複製並貼上 `!conda list` 然後，在新儲存格中執行儲存格。 支援的套件清單會依字母順序填入。

![範例](../images/jupyterlab/user-guide/libraries.PNG)

此外，下列相依性已使用但未列出：
* CUDA 11.2
* CUDNN 8.1

