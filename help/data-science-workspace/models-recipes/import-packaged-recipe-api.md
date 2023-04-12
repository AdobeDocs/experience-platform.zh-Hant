---
keywords: Experience Platform；匯入封裝方式；Data Science Workspace；熱門主題；方式；api；感生機器學習；建立引擎
solution: Experience Platform
title: 使用Sensei機器學習API匯入封裝配方
type: Tutorial
description: 本教學課程使用Sensei機器學習API來建立引擎，也稱為使用者介面中的方式。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# 使用Sensei Machine Learning API匯入封裝配方

本教學課程使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 建立 [引擎](../api/engines.md)，在使用者介面中也稱為方式。

開始之前，請務必注意Adobe Experience Platform [!DNL Data Science Workspace] 使用不同的詞語來指稱API和UI中的類似元素。 本教學課程會使用API術語，下表概述相關術語：

| UI詞語 | API詞語 |
| ---- | ---- |
| 方式 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培訓和評價 | [實驗](../api/experiments.md) |
| 服務 | [MLService](../api/mlservices.md) |

引擎包含機器學習演算法和邏輯，以解決特定問題。 下圖以視覺效果呈現 [!DNL Data Science Workspace]. 本教學課程著重於建立引擎，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入門

本教學課程需要封裝的方式檔案，其形式為Docker URL。 關注 [將源檔案打包到配方中](./package-source-files-recipe.md) 建立封裝方式檔案或提供您自己的教學課程。

- `{DOCKER_URL}`:智慧服務的Docker影像的URL位址。

本教學課程要求您完成 [驗證Adobe Experience Platform教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- `{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。
- `{ORG_ID}`:您在獨特Adobe Experience Platform整合中找到的組織認證。
- `{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。

## 建立引擎

您可以向/engines端點提出POST要求，以建立引擎。 已建立的引擎會根據封裝方式檔案的形式進行設定，這些檔案必須包含在API請求中。

### 使用Docker URL建立引擎 {#create-an-engine-with-a-docker-url}

若要建立引擎，其中包含儲存在Docker容器中的配方檔案，必須向包裝的配方檔案提供Docker URL。

>[!CAUTION]
>
> 如果您使用 [!DNL Python] 或使用以下請求。 如果使用PySpark或Scala，請使用位於Python/R示例下方的PySpark/Scala請求示例。

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

| 屬性 | 說明 |
| -------  | ----------- |
| `engine.name` | 引擎的所需名稱。 與此引擎對應的方式將繼承此值，並顯示在 [!DNL Data Science Workspace] 使用者介面作為方式的名稱。 |
| `engine.description` | 引擎的可選說明。 與此引擎對應的方式將繼承此值，並顯示在 [!DNL Data Science Workspace] 作為方式說明的使用者介面。 請勿移除此屬性，如果您選擇不提供說明，請讓此值成為空字串。 |
| `engine.type` | 引擎的執行類型。 此值對應於在中開發Docker映像的語言。 提供Docker URL以建立引擎時， `type` 為 `Python`, `R`, `PySpark`, `Spark` (Scala)或 `Tensorflow`. |
| `artifacts.default.image.location` | 您的 `{DOCKER_URL}` 來這裡。 完整的Docker URL具有下列結構： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker映像檔案的附加名稱。 請勿移除此屬性，如果您選擇不提供其他Docker影像檔案名稱，請讓此值成為空字串。 |
| `artifacts.default.image.executionType` | 此引擎的執行類型。 此值對應於在中開發Docker映像的語言。 提供Docker URL以建立引擎時， `executionType` 為 `Python`, `R`, `PySpark`, `Spark` (Scala)或 `Tensorflow`. |

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

| 屬性 | 說明 |
| --- | --- |
| `name` | 引擎的所需名稱。 與此引擎對應的方式將繼承此值，並以方式名稱的形式顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行類型。 此值對應於在「PySpark」上構建Docker影像的語言。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker映像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值對應於在「Spark」上構建Docker影像的語言。 |

**請求範圍**

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

| 屬性 | 說明 |
| --- | --- |
| `name` | 引擎的所需名稱。 與此引擎對應的方式將繼承此值，並以方式名稱的形式顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行類型。 此值對應於在「Spark」上構建Docker影像的語言。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker映像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值對應於在「Spark」上構建Docker影像的語言。 |

**回應**

成功的回應會傳回包含新建立之引擎詳細資訊（包括其唯一識別碼）的裝載(`id`)。 下列範例回應適用於 [!DNL Python] 引擎。 此 `executionType` 和 `type` 鍵會根據提供的POST而改變。

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

成功的回應會顯示JSON裝載，其中包含新建立引擎的相關資訊。 此 `id` 索引鍵代表唯一的引擎識別碼，是建立MLInstance的下一個教學課程中的必要項目。 繼續執行後續步驟之前，請確定已儲存引擎識別碼。

## 後續步驟 {#next-steps}

您已使用API建立引擎，並且已取得唯一引擎識別碼，作為回應內文的一部分。 您可以在下一個教學課程中使用此引擎識別碼，以了解如何 [使用API建立、訓練和評估模型](./train-evaluate-model-api.md).
