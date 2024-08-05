---
keywords: Experience Platform；匯入封裝的配方；資料科學Workspace；熱門主題；配方；api；sensei機器學習；建立引擎
solution: Experience Platform
title: 使用Sensei機器學習API匯入封裝的配方
type: Tutorial
description: 本教學課程使用Sensei Machine Learning API建立引擎，也稱為使用者介面中的方式。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 3%

---

# 使用Sensei機器學習API匯入封裝的配方

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

此教學課程使用[[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)來建立[引擎](../api/engines.md)，也稱為使用者介面中的配方。

在開始使用之前，請務必注意，Adobe Experience Platform [!DNL Data Science Workspace]使用不同的辭彙來參照API和UI中的類似元素。 在本教學課程中使用API辭彙，下表概述相關辭彙：

| UI術語 | API 術語 |
| ---- | ---- |
| 配方 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 訓練與評估 | [實驗](../api/experiments.md) |
| 服務 | [MLS服務](../api/mlservices.md) |

引擎包含用於解決特定問題的機器學習演算法和邏輯。 下圖提供顯示[!DNL Data Science Workspace]中API工作流程的視覺效果。 本教學課程著重於建立引擎，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入門

本教學課程需要採用Docker URL格式的封裝配方檔案。 依照[將來源檔案封裝到配方](./package-source-files-recipe.md)教學課程中，以建立封裝的配方檔案或提供您自己的檔案。

- `{DOCKER_URL}`：智慧型服務Docker映像的URL位址。

此教學課程需要您完成[對Adobe Experience Platform的驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform] API。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。
- `{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。
- `{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。

## 建立引擎

可以透過向/engines端點發出POST請求來建立引擎。 創建的引擎是根據打包的配方文件的格式配置的，該文件必須作為 API 請求的一部分包含在內。

### 建立帶有 Docker URL的引擎 {#create-an-engine-with-a-docker-url}

若要使用儲存在Docker容器中的封裝配方檔案建立引擎，您必須提供封裝配方檔案的Docker URL。

>[!CAUTION]
>
> 如果您使用[!DNL Python]或R，請使用以下要求。 如果您使用PySpark或Scala，請使用位於Python/R範例下方的PySpark/Scala要求範例。

**API格式**

```http
POST /engines
```

**要求Python/R**

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
| `engine.name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，以用戶介面中 [!DNL Data Science Workspace] 顯示為配方的名稱。 |
| `engine.description` | 引擎的可選說明。 與此引擎對應的配方將繼承此值用戶以顯示為 [!DNL Data Science Workspace] 配方的描述。 請勿移除此屬性，如果您選擇不提供說明，請將此值設為空字串。 |
| `engine.type` | 引擎的執行型別。 此值對應於在其中開發Docker映像的語言。 當提供Docker URL以建立引擎時，`type`是`Python`、`R`、`PySpark`、`Spark` (Scala)或`Tensorflow`。 |
| `artifacts.default.image.location` | 您的`{DOCKER_URL}`將移至此處。 完整的Docker URL具有以下結構： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker影像檔案的額外名稱。 請勿移除此屬性，如果您選擇不提供額外的Docker影像檔案名稱，請將此值設為空字串。 |
| `artifacts.default.image.executionType` | 此引擎的執行類型。 此值對應於開發 Docker 映射時使用的語言。 當提供 Docker URL 以建立引擎時， `executionType` 為 `Python`、 `R`、 `PySpark`、（ `Spark` Scala） 或 `Tensorflow`。 |

**要求PySpark**

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
| `name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 「引擎」的選擇性說明。 與此引擎對應的配方將繼承此值，以在UI中顯示為方式的描述。 此屬性為必填項。 如果不想提供說明，請將其值設置為空字串。 |
| `type` | 引擎的執行類型。 此值對應於在「PySpark」上構建 Docker 映像的語言。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 |
| `artifacts.default.image.location` | Docker URL所連結之Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於在「Spark」上構建Docker影象的語言。 |

**要求Scala**

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
| `name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 「引擎」的選擇性說明。 對應至此引擎的配方將繼承此值，以作為配方說明顯示在UI中。 此屬性為必要項。 如果您不想要提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行型別。 此值對應於在「Spark」上構建 Docker 映像的語言。 |
| `mlLibrary` | 為 PySpark 和 Scala 配方建立引擎時需要的欄位。 |
| `artifacts.default.image.location` | Docker URL所連結之Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於在「Spark」上構建Docker影象的語言。 |

**回應**

成功的回應會傳回承載，其中包含新建立之引擎的詳細資料，包括其唯一識別碼(`id`)。 下列範例回應適用於[!DNL Python]引擎。 根據提供的POST，`executionType`和`type`金鑰會變更。

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

成功的回應會顯示一個 JSON 有效負載，其中包含有關新創建的引擎的資訊。 密鑰 `id` 表示唯一的引擎標識符，在下一個教學課程中創建 MLInstance 時需要該密鑰。 確保已保存引擎標識碼，然後再繼續執行後續步驟。

## 後續步驟 {#next-steps}

您已使用 API 建立了一個引擎，並且作為回應正文的一部分獲取了唯一的引擎識別碼。 當您瞭解如何使用API[建立、訓練及評估模型](./train-evaluate-model-api.md)時，可以在下一個教學課程中使用此引擎識別碼。
