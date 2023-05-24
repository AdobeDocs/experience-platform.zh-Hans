---
keywords: Experience Platform；套件來源檔案；Data Science Workspace；熱門主題；Docker；Docker影像
solution: Experience Platform
title: 將來源檔案封裝到配方中
type: Tutorial
description: 本教學課程提供有關如何將提供的零售銷售範例來源檔案封裝到封存檔案中的指示，透過在UI中或使用API遵循配方匯入工作流程，可用於在Adobe Experience Platform Data Science Workspace中建立配方。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 將來源檔案封裝到配方中

本教學課程說明如何將提供的零售業範例來源檔案封裝到封存檔案中，以便在Adobe Experience Platform中建立配方 [!DNL Data Science Workspace] 在UI中或使用API遵循配方匯入工作流程。

要瞭解的概念：

- **配方**：配方是模型規格的Adobe術語，是頂層容器，代表特定機器學習、人工智慧演演算法或演演算法組合、處理邏輯和設定，需要這些來建立和執行經過訓練的模型，從而幫助解決特定業務問題。
- **來源檔案**：您的專案中包含配方邏輯的個別檔案。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 配方建立

配方建立從封裝來源檔案開始，以建置封存檔案。 來源檔案會定義用來解決手頭特定問題的機器學習邏輯和演演算法，且會以其中一種方式撰寫 [!DNL Python]、R、PySpark或Scala。 構建的封存檔案採取Docker映像的形式。 建置後，封裝的封存檔案會匯入 [!DNL Data Science Workspace] 建立配方 [在UI中](./import-packaged-recipe-ui.md) 或 [使用API](./import-packaged-recipe-api.md).

### 基於Docker的模型編寫 {#docker-based-model-authoring}

Docker映像可讓開發人員將應用程式與其所需的所有元件（例如程式庫和其他相依性）一起封裝，然後以一個封裝形式送出。

使用配方建立工作流程期間提供給您的憑證將內建的Docker映像推送到Azure容器登入。

若要取得您的Azure容器登入認證，請登入 [Adobe Experience Platform](https://platform.adobe.com). 在左側導覽欄中，導覽至 **[!UICONTROL 工作流程]**. 選取 **[!UICONTROL 匯入配方]** 接著選取 **[!UICONTROL Launch]**. 如需參考資訊，請參閱下面的熒幕擷圖。

![](../images/models-recipes/package-source-files/import.png)

此 **[!UICONTROL 設定]** 頁面隨即開啟。 提供適當的 **[!UICONTROL 配方名稱]**，例如「零售配方」，並可選擇提供說明或檔案URL。 完成後，按一下 **[!UICONTROL 下一個]**.

![](../images/models-recipes/package-source-files/configure.png)

選取適當的 *執行階段*，然後選擇 **[!UICONTROL 分類]** 的 *型別*. 您的Azure Container Registry認證會在完成後產生。

>[!NOTE]
>
>*型別* 是設計配方所針對的機器學習問題類別，並在訓練後用來協助量身打造評估訓練回合。

>[!TIP]
>
>- 對象 [!DNL Python] 配方選取 **[!UICONTROL Python]** 執行階段。
>- 針對R配方，選取 **[!UICONTROL R]** 執行階段。
>- 對於PySpark配方，請選取 **[!UICONTROL PySpark]** 執行階段。 成品型別會自動填入。
>- 對於Scala配方，請選取 **[!UICONTROL Spark]** 執行階段。 成品型別會自動填入。


![](../images/models-recipes/package-source-files/docker-creds.png)

記下Docker主機、使用者名稱和密碼的值。 這些用來建置和推送 [!DNL Docker] 影像的工作流程概述如下。

>[!NOTE]
>
>完成下列步驟後，系統就會提供來源URL。 在後續的教學課程中會說明此設定檔案 [後續步驟](#next-steps).

### 封裝來源檔案

首先，取得 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform資料科學工作區參考資料</a> 存放庫。

- [建置Python Docker映像](#python-docker)
- [建置R Docker映像](#r-docker)
- [建置PySpark Docker影像](#pyspark-docker)
- [建立Scala (Spark) Docker影像](#scala-docker)

### 建置 [!DNL Python] Docker影像 {#python-docker}

如果您尚未這樣做，請原地複製 [!DNL GitHub] 使用下列命令將存放庫放到您的本機系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/python/retail`. 在這裡，您可以找到指令碼 `login.sh` 和 `build.sh` 用於登入Docker和構建 [!DNL Python Docker] 影像。 如果您的 [Docker憑證](#docker-based-model-authoring) ready，依序輸入下列指令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker源檔案URL。 在此特定範例中，它看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建置R [!DNL Docker] 影像 {#r-docker}

如果您尚未這樣做，請原地複製 [!DNL GitHub] 使用下列命令將存放庫放到您的本機系統上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 位於複製的存放庫內。 您可以在這裡找到檔案 `login.sh` 和 `build.sh` ，用於登入Docker和構建R Docker映像。 如果您的 [Docker憑證](#docker-based-model-authoring) ready，依序輸入下列指令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker源檔案URL。 在此特定範例中，它看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建置PySpark Docker影像 {#pyspark-docker}

從複製開始 [!DNL GitHub] 使用下列命令將存放庫放到您的本機系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/pyspark/retail`. 指令碼 `login.sh` 和 `build.sh` 位於此處，用於登入Docker和構建Docker映像。 如果您的 [Docker憑證](#docker-based-model-authoring) ready，依序輸入下列指令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker源檔案URL。 在此特定範例中，它看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建立Scala Docker映像 {#scala-docker}

從複製開始 [!DNL GitHub] 在「終端機」中使用以下命令將存放庫放到您的本機系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下來，導覽至目錄 `experience-platform-dsw-reference/recipes/scala` 您可以在其中找到指令碼 `login.sh` 和 `build.sh`. 這些指令碼用於登入Docker和構建Docker映像。 如果您的 [Docker憑證](#docker-based-model-authoring) 就緒，請依序輸入下列命令至終端機：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您嘗試使用登入Docker時遇到許可權錯誤 `login.sh` 指令碼，嘗試使用命令 `bash login.sh`.

執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker源檔案URL。 在此特定範例中，它看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

## 后续步骤 {#next-steps}

本教學課程說明如何將來源檔案封裝到配方中，這是將配方匯入的先決條件步驟 [!DNL Data Science Workspace]. 您現在應該在Azure容器登入中擁有Docker映像以及對應的映像URL。 您現在已準備好開始有關將封裝配方匯入的教學課程 [!DNL Data Science Workspace]. 選取下列其中一個教學課程連結以開始：

- [在UI中匯入封裝的配方](./import-packaged-recipe-ui.md)
- [使用API匯入封裝的配方](./import-packaged-recipe-api.md)
