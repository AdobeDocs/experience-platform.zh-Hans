---
keywords: Experience Platform；首頁；熱門主題；沙箱疑難排解
solution: Experience Platform
title: 沙箱疑難排解指南
description: 本檔案提供有關Adobe Experience Platform中沙箱的常見問題解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 9%

---

# 沙箱疑難排解指南

本檔案提供有關Adobe Experience Platform中沙箱的常見問題解答。 有關其他Platform服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

沙箱會將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。 有关更多信息，请参阅[沙盒概述](home.md)。

## 什麼是Sandbox？

沙箱是單一Experience Platform執行個體中的虛擬分割區。 每個沙箱都維護其自身的Platform資源資料庫（包括結構描述、資料集、設定檔等）。 在沙箱內執行的所有內容和動作都僅限於該沙箱，不會影響任何其他沙箱。 有关更多信息，请参阅[沙盒概述](home.md)。

## 可以使用哪些型別的沙箱，以及它們之間有何差異？ {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙盒类型"
>abstract="沙盒类型指示这是生产沙盒还是开发沙盒。生产沙盒包括实时数据，开发沙盒用于测试和开发。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="在 UI 中创建沙盒"

Experience Platform中有兩種沙箱型別：

* **生產沙箱**：生產沙箱旨在用於生產環境中的設定檔。 Platform可讓您建立多個生產沙箱，以便在為資料提供正確功能的同時仍保持操作隔離。 此功能可讓您指定特定的生產沙箱給不同的業務線、品牌、專案或區域。 生產沙箱支援大量生產設定檔，最多可達您的授權 [!DNL Profile] 承諾（在所有授權的生產沙箱中累積測量）。 您有權根據授權使用授權平均設定檔 [!DNL Profile] （在所有授權的生產沙箱中累積測量）。
* **開發沙箱**：開發沙箱是一種沙箱，專門可用於使用非生產設定檔進行開發和測試。 開發沙箱支援最多10%授權的非生產設定檔數量 [!DNL Profile] 承諾（在所有授權開發沙箱中累積測量）。 您有權享有：
   * 每個授權的非生產設定檔的平均非生產設定檔豐富度為75 KB （在所有授權開發沙箱中累加測量）；
   * 每個開發沙箱每天一個批次分段工作；
   * 平均120 [!DNL Profile] API呼叫，按 [!DNL Profile]，每年（在所有已授權的開發沙箱中累積測量）。

有关更多信息，请参阅[沙盒概述](./home.md)。

## 我可以從多個沙箱存取資源嗎？

沙箱是單一Platform執行個體的獨立分割區，每個沙箱都維護自己的獨立資源庫。 不論沙箱型別（生產或非生產）為何，都無法從任何其他沙箱存取存在於一個沙箱中的資源。

## 什麼是預設的生產沙箱？

預設的生產沙箱是第一次布建組織時建立的第一個生產沙箱。 預設的生產沙箱可讓您從Platform擷取或使用資料，以及接受不包含沙箱名稱或沙箱ID值的請求。 預設的生產沙箱可以重設，但不能刪除。

## 我可以擁有多少個生產沙箱？

Experience Platform執行個體支援多個生產及開發沙箱，每個沙箱都維護其獨立的Platform資源庫（包括結構描述、資料集和設定檔）。

預設Experience Platform授權總共會授予您5個沙箱，您可將其分類為生產或開發。 您可以授權其他10個沙箱的套件，最多總共75個沙箱。

生產沙箱可重設或刪除，但Adobe Analytics也用於的生產沙箱除外 [跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或其中代管的身分圖表是否也被Adobe Audience Manager用於此功能 [以人物為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 功能。

您可以更新生產沙箱的標題。 但是，無法重新命名生產沙箱。

>[!NOTE]
>
>沙箱名稱用於API呼叫中的查詢目的，而沙箱標題則用作顯示名稱。

## 我可以擁有多少個開發沙箱？

Experience Platform目前最多可在單一組織中啟用75個沙箱（生產及開發）。

開發沙箱支援重設和刪除功能。

## 我剛才已建立沙箱。 如何為將使用此沙箱的使用者設定許可權？

Adobe Admin Console透過使用產品設定檔將使用者連結至沙箱和許可權。 建立新沙箱後，瀏覽至 **許可權** 您想要授與存取權的產品設定檔標籤，然後按一下 **沙箱**. 從這裡，您可以用與其他許可權相同的方式新增或移除新沙箱的存取權。

如果您想要將唯一許可權新增到特定沙箱的使用者，您可能需要建立新的產品設定檔，並套用適當的沙箱和許可權，然後將這些使用者指派到該設定檔。

請參閱 [存取控制使用手冊](../access-control/ui/overview.md) 有關在Admin Console中管理沙箱和許可權的詳細資訊。
