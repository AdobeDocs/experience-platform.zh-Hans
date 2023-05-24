---
keywords: Experience Platform；零售配方；資料科學工作區；熱門主題；配方
solution: Experience Platform
title: 建立零售銷售結構描述和資料集
type: Tutorial
description: 本教學課程提供您所有其他Adobe Experience Platform資料科學工作區教學課程所需的先決條件和資產。 完成後，您和您的組織成員將可在Experience Platform上取得零售銷售結構描述和資料集。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# 建立零售銷售結構描述和資料集

本教學課程提供您所有其他課程所需的先決條件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教學課程。 完成後，您和貴組織成員將可在以下位置使用零售銷售結構和資料集： [!DNL Experience Platform].

## 快速入门

開始進行本教學課程之前，您必須具備下列必要條件：
- 存取 [!DNL Adobe Experience Platform]. 如果您無權存取中的組織 [!DNL Experience Platform]，請在繼續之前聯絡您的系統管理員。
- 進行授權 [!DNL Experience Platform] API呼叫。 完成 [驗證及存取Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en) 教學課程來取得下列值，以成功完成本教學課程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 使用者端密碼： `{CLIENT_SECRET}`
   - 使用者端憑證： `{PRIVATE_KEY}`
- 的範例資料和來源檔案 [零售指導方針](../pre-built-recipes/retail-sales.md). 下載此專案和其他專案所需的資產 [!DNL Data Science Workspace] 教學課程來自 [Adobe公開Git存放庫](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 以及下列專案 [!DNL Python] 套件：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [聽寫器](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 深入瞭解本教學課程使用的下列概念：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [結構描述組合基本概念](../../xdm/schema/field-dictionary.md)

## 建立零售銷售結構描述和資料集

使用提供的啟動程式指令碼，會自動建立零售銷售結構描述和資料集。 請依序遵循下列步驟：

### 設定檔案

1. 內部 [!DNL Experience Platform] 教學課程資源套件，瀏覽至目錄 `bootstrap`，並開啟 `config.yaml` 使用適當的文字編輯器。
2. 在 `Enterprise` 區段，輸入下列值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯下找到的值 `Platform` 區段，範例如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`：API呼叫的基本路徑。 請勿修改此值。
   - `ims_token`：您的 `{ACCESS_TOKEN}` 移至此處。
   - `ingest_data`：在本教學課程中，請將此值設為 `"True"` 以建立零售銷售結構描述和資料集。 值 `"False"` 只會建立結構描述。
   - `build_recipe_artifacts`：在本教學課程中，請將此值設為 `"False"` 以防止指令碼產生配方成品。
   - `kernel_type`：配方成品的執行型別。 此值保留為 `Python` 如果 `build_recipe_artifacts` 設為 `"False"`，否則請指定正確的執行型別。

4. 在 `Titles` 區段，針對零售範例資料提供下列適當資訊，並在完成編輯後儲存並關閉檔案。 範例如下：

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### 執行啟動程式指令碼

1. 開啟您的終端機應用程式，並導覽至 [!DNL Experience Platform] tutorial資源目錄。
2. 設定 `bootstrap` 目錄作為目前的工作路徑，並執行 `bootstrap.py` [!DNL Python] 指令碼，方法是輸入下列命令：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >指令碼可能需要幾分鐘才能完成。

## 后续步骤

成功完成Bootstrap指令碼後，您便可以在上檢視零售銷售輸入和輸出結構描述和資料集 [!DNL Experience Platform]. 請參閱 [預覽結構描述資料教學課程](./preview-schema-data.md)
以取得詳細資訊。

您也已成功將零售業範例資料內嵌至 [!DNL Experience Platform] 使用提供的啟動程式指令碼。

若要繼續使用擷取的資料：
- [使用Jupyter Notebooks分析您的資料](../jupyterlab/analyze-your-data.md)
   - 在資料科學工作區中使用Jupyter Notebooks來存取、探索、視覺化和瞭解您的資料。
- [將來源檔案封裝到配方中](./package-source-files-recipe.md)
   - 按照本教學課程瞭解如何將您自己的模型帶入 [!DNL Data Science Workspace] 將來源檔案封裝在可匯入的「配方」檔案中。
