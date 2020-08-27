---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 匯入封裝的方式(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 2%

---


# 匯入封裝的方式(API)

本教學課程 [使用[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)[](../api/engines.md)來建立引擎，在使用者介面中也稱為「配方」。

在開始使用之前，請務必注意，Adobe Experience Platform使用不 [!DNL Data Science Workspace] 同的術語來參照API和UI中的類似元素。 本教學課程中使用API詞語，下表概述相關詞語：

| UI詞語 | API期限 |
| ---- | ---- |
| 配方 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培訓與評估 | [實驗](../api/experiments.md) |
| 服務 | [MLService](../api/mlservices.md) |

引擎包含機器學習演算法和邏輯，以解決特定問題。 下圖顯示了中的API工作流程 [!DNL Data Science Workspace]。 本教學課程著重於建立引擎，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入門

本教學課程需要以Docker URL格式封裝的配方檔案。 請依照「 [封裝來源檔案」教學課程](./package-source-files-recipe.md) ，建立封裝的「配方」檔案或提供您自己的「配方」檔案。

- `{DOCKER_URL}`:智慧服務的Docker影像的URL位址。

本教學課程要求您完成「 [Adobe Experience Platform驗證」教學課程](../../tutorials/authentication.md) ，才能成功呼叫 [!DNL Platform] API。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。
- `{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。
- `{API_KEY}`:您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。

## 建立引擎

對/engines端點發出POST請求可以建立引擎。 所建立的引擎是根據封裝的方式檔案的格式來設定，該檔案必須包含在API要求中。

### 使用Docker URL建立引擎 {#create-an-engine-with-a-docker-url}

若要建立具有儲存在Docker容器中之封裝配方檔案的引擎，您必須為封裝配方檔案提供Docker URL。

>[!CAUTION]
>
> 如果您使用或 [!DNL Python] R使用下列請求。 如果您使用PySpark或Scala，請使用位於Python/R範例下方的PySpark/Scala請求範例。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `engine.name` | 引擎的所需名稱。 與此引擎對應的處方將繼承此值，該值將作為處方 [!DNL Data Science Workspace] 的名稱顯示在用戶介面中。 |
| `engine.description` | 引擎的選用說明。 與此引擎對應的處方將繼承此值，該值將作為處方 [!DNL Data Science Workspace] 的說明顯示在用戶介面中。 請勿移除此屬性，如果您選擇不提供說明，請讓此值為空字串。 |
| `engine.type` | 引擎的執行類型。 此值與Docker影像開發所用的語言相對應。 當提供Docker URL來建立引擎時， `type` 為 `Python`、 `R`、 `PySpark`( `Spark` Scala)或 `Tensorflow`。 |
| `artifacts.default.image.location` | 你 `{DOCKER_URL}` 來這。 完整的Docker URL具有下列結構： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker映像檔案的附加名稱。 請勿移除此屬性，如果您選擇不提供其他Docker影像檔名，請讓此值為空字串。 |
| `artifacts.default.image.executionType` | 此引擎的執行類型。 此值與Docker影像開發所用的語言相對應。 當提供Docker URL來建立引擎時， `executionType` 為 `Python`、 `R`、 `PySpark`( `Spark` Scala)或 `Tensorflow`。 |

**要求PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行類型。 此值對應於Docker影像建立在&quot;PySpark&quot;上的語言。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker映像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker影像建立在&quot;Spark&quot;上的語言相對應。 |

**請求標準**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行類型。 此值與Docker影像建立在&quot;Spark&quot;上的語言相對應。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker映像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker影像建立在&quot;Spark&quot;上的語言相對應。 |

**回應**

成功的回應會傳回包含新建立之引擎詳細資料（包括其唯一識別碼）的裝載`id`。 以下是引擎的範例回 [!DNL Python] 應。 根據 `executionType` 提供 `type` 的開機自檢更改和鍵。

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

成功的回應會顯示JSON裝載，內含有關新建引擎的資訊。 此 `id` 鍵代表唯一的引擎識別碼，並在下一個教學課程中用來建立MLInstance。 請確定引擎識別碼已儲存，然後再繼續後續步驟。

## 下一步 {#next-steps}

您已使用API建立引擎，並取得唯一的引擎識別碼作為回應本體的一部分。 在下一個教學課程中，您可以使用此引擎識別碼，學習如 [何使用API建立、訓練和評估模型](./train-evaluate-model-api.md)。