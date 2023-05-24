---
solution: Experience Platform
title: 在UI中產生XDM結構描述的範例資料
description: 瞭解如何根據Adobe Experience Platform使用者介面中的現有結構描述產生範例JSON資料。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 在UI中產生XDM結構的範例資料

若要將資料內嵌至Adobe Experience Platform，資料的格式和結構必須符合現有的Experience Data Model (XDM)結構。 根據特定資料集的結構描述複雜性，可能很難判斷資料集在擷取時預期的資料確切形狀。

對於您在Experience PlatformUI中定義的任何結構描述，您可以產生符合結構描述結構的範例JSON物件。 此物件可當作任何資料匯入使用相關結構描述的資料集中的範本。

在Platform UI中選取 **[!UICONTROL 結構描述]** 左側導覽列中。 在 **[!UICONTROL 瀏覽]** 索引標籤中，找到您要為其產生範例資料的結構描述。 從清單中選取它，右邊欄會更新以顯示有關結構的詳細資訊。 從此處選取 **[!UICONTROL 下載範例檔案]**.

![](../images/ui/sample/sample-data.png)

瀏覽器會下載範例JSON檔案。 您現在可以使用此檔案作為參考，瞭解在擷取至採用此結構描述的資料集時，如何建構您的資料。

## 后续步骤

本指南說明如何從Platform UI中的XDM結構描述產生範例JSON檔案。 若要瞭解如何使用結構描述登入API產生範例資料，請參閱 [範例資料端點指南](../api/sample-data.md).

在您準備好開始內嵌資料後，請參閱教學課程： [將CSV檔案對應至XDM](../../ingestion/tutorials/map-csv/overview.md) 瞭解如何將平面資料檔案（例如CSV）對應到XDM結構描述，並將其擷取到Platform。 或者，您可以建立 [來源連線](../../sources/home.md) 從外部來源匯入資料，並將其對應至XDM。

如需功能的詳細資訊， [!UICONTROL 結構描述] 工作區在UI中，請參閱 [[!UICONTROL 結構描述] 工作區概觀](./overview.md).
