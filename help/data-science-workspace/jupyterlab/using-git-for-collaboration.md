---
keywords: Experience Platform；JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；Git；Github
solution: Experience Platform
title: 使用Git在JupyterLab中共同作業
type: Tutorial
description: Git是分散式版本控制系統，用於在軟體開發期間追蹤原始程式碼中的變更。 Git已預先安裝在Data Science Workspace JupyterLab環境中。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 共同作業位置 [!DNL JupyterLab] 使用 [!DNL Git]

[!DNL Git] 是分散式版本控制系統，用於在軟體開發期間追蹤原始程式碼中的變更。 Git已預先安裝在中 [!DNL Data Science Workspace JupyterLab] 環境。

## 先决条件

>[!NOTE]
>
> 您要使用的Git伺服器必須可透過網際網路存取。

此 [!DNL Data Science Workspace JupyterLab] 環境是託管環境，未部署在您的公司防火牆內，因此您連線的Git伺服器必須可從公用網際網路存取。 這可能是上的公開或私人存放庫 [GitHub](https://github.com/) 或另一個例項 [!DNL Git] 您已決定自行託管的伺服器。

## Connect [!DNL Git] 至 [!DNL Data Science Workspace JupyterLab Notebooks] 環境

從啟動開始 [!DNL Adobe Experience Platform] 並導覽至 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 環境。

範圍 [!DNL JupyterLab]，選取 **[!UICONTROL 檔案]** 然後暫留在 **[!UICONTROL 新增]**. 從出現的下拉式清單中選取 **[!UICONTROL 終端機]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

下一個，在內 *終端機* 使用以下命令導覽至您的工作區： `cd my-workspace`.

![cd工作區](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 若要檢視可用的Git命令清單，請發出命令： `git -help` 在您的「終端機」中。

接下來，使用複製您要使用的存放庫 `git clone` 命令。 使用「 」原地複製專案 `https://` URL而非 `ssh://`.

**示例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![原地複製](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 為了執行任何寫入操作(`git push` 例如，需要為每個新工作階段執行下列設定命令。 另請注意，任何推送命令都會提示輸入使用者名稱和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 后续步骤

完成複製存放庫後，您可以像在本機電腦上一樣使用Git與其他人在Notebook上共同作業。 如需您可以在內執行的操作的詳細資訊 [!DNL JupyterLab]，請參閱 [[!DNL JupyterLab user guide]](./overview.md).
