---
keywords: Experience Platform；匯入封裝的配方；Data Science Workspace；熱門主題；配方；api；sensei機器學習；建立引擎
solution: Experience Platform
title: 使用Sensei機器學習API匯入封裝的配方
type: Tutorial
description: 本教學課程使用Sensei Machine Learning API建立引擎（在使用者介面中又稱為「配方」）。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# 使用Sensei機器學習API匯入封裝的配方

本教學課程使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 建立 [引擎](../api/engines.md)，在使用者介面中又稱為「配方」 。

開始使用前，請務必注意Adobe Experience Platform [!DNL Data Science Workspace] 會使用不同的辭彙來參照API和UI中的類似元素。 在本教學課程中使用API辭彙，下表概述相關辭彙：

| UI詞語 | API詞語 |
| ---- | ---- |
| 指導方針 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 訓練與評估 | [试验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

Engine包含用於解決特定問題的機器學習演演算法和邏輯。 下圖提供視覺效果，顯示中的API工作流程 [!DNL Data Science Workspace]. 本教學課程著重於建立引擎，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入门

本教學課程需要採用Docker URL格式的封裝配方檔案。 請遵循 [將來源檔案封裝到配方中](./package-source-files-recipe.md) 建立封裝配方檔案或提供您自己的教學課程。

- `{DOCKER_URL}`：智慧型服務的Docker影像的URL位址。

本教學課程要求您已完成 [驗證Adobe Experience Platform教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- `{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。
- `{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。
- `{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。

## 建立引擎

可以透過向/engines端點發出POST請求來建立引擎。 已建立的引擎是根據封裝的配方檔案的格式進行設定，配方檔案必須包含在API請求中。

### 使用Docker URL建立引擎 {#create-an-engine-with-a-docker-url}

若要使用儲存在Docker容器中的封裝配方檔案來建立Engine，您必須為封裝的配方檔案提供Docker URL。

>[!CAUTION]
>
> 如果您使用 [!DNL Python] 或R使用下面的請求。 如果您使用PySpark或Scala，請使用位於Python/R範例下方的PySpark/Scala請求範例。

**API格式**

```http
POST /engines
```

**請求Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 属性 | 描述 |
| -------  | ----------- |
| `engine.name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以顯示於 [!DNL Data Science Workspace] 使用者介面做為配方名稱。 |
| `engine.description` | Engine的選擇性說明。 對應至此引擎的配方將繼承此值，以顯示於 [!DNL Data Science Workspace] 使用者介面作為食譜的說明。 請勿移除此屬性；如果您選擇不提供說明，請將此值設為空字串。 |
| `engine.type` | 引擎的執行型別。 此值對應於在其中開發Docker映象的語言。 當提供Docker URL以建立引擎時， `type` 為 `Python`， `R`， `PySpark`， `Spark` (Scala)，或 `Tensorflow`. |
| `artifacts.default.image.location` | 您的 `{DOCKER_URL}` 移至此處。 完整的Docker URL具有以下結構： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker影像檔案的附加名稱。 不要移除此屬性，如果您選擇不提供額外的Docker影像檔案名稱，請讓此值成為空字串。 |
| `artifacts.default.image.executionType` | 此引擎的執行型別。 此值對應於在其中開發Docker映象的語言。 當提供Docker URL以建立引擎時， `executionType` 為 `Python`， `R`， `PySpark`， `Spark` (Scala)，或 `Tensorflow`. |

**請求PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | Engine的選擇性說明。 對應至此引擎的配方將繼承此值，以顯示於UI中的配方說明。 此属性是必需的。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行型別。 此值對應於Docker映像建立在「PySpark」上的語言。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 |
| `artifacts.default.image.location` | Docker URL所連結的Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於Docker映像建立在「Spark」上的語言。 |

**請求Scala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | Engine的選擇性說明。 對應至此引擎的配方將繼承此值，以顯示於UI中的配方說明。 此属性是必需的。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行型別。 此值對應於Docker映像建立在「Spark」上的語言。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 |
| `artifacts.default.image.location` | Docker URL所連結的Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於Docker映像建立在「Spark」上的語言。 |

**响应**

成功回應會傳回包含新建立之引擎的詳細資訊裝載，包括其唯一識別碼(`id`)。 以下範例回應適用於 [!DNL Python] 引擎。 此 `executionType` 和 `type` 金鑰會根據提供的POST而變更。

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

成功的回應會顯示JSON裝載，其中包含有關新建立引擎的資訊。 此 `id` key代表唯一的引擎識別碼，在下一個教學課程中是建立MLInstance的必要專案。 繼續後續步驟之前，請確定已儲存引擎識別碼。

## 后续步骤 {#next-steps}

您已使用API建立引擎，而且取得唯一引擎識別碼做為回應本文的一部分。 您可在下一個教學課程中使用此Engine識別碼，瞭解如何 [使用API建立、訓練和評估模型](./train-evaluate-model-api.md).
