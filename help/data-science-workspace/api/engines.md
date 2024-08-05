---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；引擎；sensei機器學習api
solution: Experience Platform
title: 引擎API端點
description: 引擎是數據科學工作環境中機器學習模型的基礎。 它們包含解決特定問題的機器學習演演算法、執行特徵工程的特徵配管或兩者。
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 2%

---

# 引擎端點

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

引擎是資料科學Workspace中機器學習模型的基礎。 它們包含解決特定問題的機器學習演演算法、執行特徵工程的特徵配管或兩者。

## 查詢您的Docker登錄檔

>[!TIP]
>
>如果您沒有Docker URL，請造訪[將來源檔案封裝到配方](../models-recipes/package-source-files-recipe.md)教學課程中，以逐步瞭解如何建立Docker主機URL。

需要 Docker 註冊表憑據才能上傳打包的配方文件，包括 Docker 主機 URL、使用者名和密碼。 您可以透過執行以下GET 要求來尋找此資訊：

**API 格式**

```https
GET /engines/dockerRegistry
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含Docker登入詳細資訊的承載，包括Docker URL (`host`)、使用者名稱(`username`)和密碼(`password`)。

>[!NOTE]
>
>每當更新 `{ACCESS_TOKEN}` 時，您的 Docker 密碼都會更改。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用 Docker URL 建立引擎 {#docker-image}

您可以通過執行POST 要求來創建引擎，同時提供其中繼資料和以多部分形式引用 Docker 映射的 Docker URL。

**API 格式**

```https
POST /engines
```

**請求 Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 屬性 | 說明 |
| --- | --- |
| `name` | Engine所需的名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 「引擎」的選擇性說明。 對應至此引擎的配方將繼承此值，以作為配方說明顯示在UI中。 此屬性為必要項。 如果您不想要提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行型別。 此值對應於Docker影像建置所在的語言，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |
| `algorithm` | 字串；指定機器學習演演算法的型別。 支援的演演算法型別包括「分類」、「回歸」或「自訂」。 |
| `artifacts.default.image.location` | Docker URL所連結之Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於Docker影像建置所在的語言，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |

**請求 PySpark/Scala**

在為 PySpark 配方製作請求時， `executionType` 和 `type` 是“PySpark”。 在為 Scala 配方製作請求時， `executionType` 和 `type` 是“火花”。 以下 Scala 方式示例使用 Spark：

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
| `name` | Engine所需的名稱。 與此引擎對應的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的配方將繼承此值，以在UI中顯示為方式的描述。 此屬性為必填項。 如果不想提供說明，請將其值設置為空字串。 |
| `type` | 引擎的執行類型。 此值對應於構建 Docker 映像所基於的語言。 該值可以設置為Spark或 PySpark。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 此欄位必須設定為`databricks-spark`。 |
| `artifacts.default.image.location` | Docker 映射的位置。 僅支援 Azure ACR 或公共（未經身份驗證）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值對應於構建 Docker 映像所基於的語言。 這可以是“Spark”或“PySpark”。 |

**回應**

成功的回應會返回一個有效負載，其中包含新創建的引擎的詳細資訊，包括其唯一標識碼 （`id`）。 以下示例回應適用於 Python 引擎。 所有引擎回應追隨此格式：

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 使用 Docker URL 建立功能管道引擎 {#feature-pipeline-docker}

您可以通過執行POST 要求來創建功能管道引擎，同時提供其中繼資料和引用 Docker 映射的 Docker URL。

**API 格式**

```https
POST /engines
```

**要求**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 引擎的執行類型。 此值對應於構建 Docker 映像所基於的語言。 該值可以設置為Spark或 PySpark。 |
| `algorithm` | 正在使用的演算法，將此值 `fp` 設置為 （功能管道）。 |
| `name` | 特徵配管引擎的所需名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 「引擎」的選擇性說明。 對應至此引擎的配方將繼承此值，以作為配方說明顯示在UI中。 此屬性為必填項。 如果不想提供說明，請將其值設置為空字串。 |
| `mlLibrary` | 為 PySpark 和 Scala 配方建立引擎時需要的欄位。 這個欄位必須設定為 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker映像的位置。 僅支援Azure ACR或公用（未驗證） Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於構建Docker映像的語言。 這可以是&quot;Spark&quot;或&quot;PySpark&quot;。 |
| `artifacts.default.image.packagingType` | 引擎的封裝型別。 此值應設為`docker`。 |
| `artifacts.default.defaultMLInstanceConfigs` | 您的 `pipeline.json` 配置檔案參數。 |

**回應**

成功的回應會傳回承載，其中包含新建立功能管道引擎的詳細資料，包括其唯一識別碼(`id`)。 以下示例回應適用於 PySpark 功能管道引擎。

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## 擷取引擎清單

您可以透過執行單一GET請求來擷取引擎清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 有關可用查詢的清單，請参閱有關資產檢索](./appendix.md#query)的查詢参数的[附錄部分。

**API 格式**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回清單引擎及其詳細數據。

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### 檢索特定引擎 {#retrieve-specific}

您可以透過執行GET請求（包含請求路徑中所需引擎的ID）來擷取特定引擎的詳細資訊。

**API格式**

```https
GET /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的ID。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含所需引擎詳細資訊的裝載。

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## 更新引擎

您可以透過PUT請求（請求路徑中包含目標引擎的ID）來覆寫現有引擎的屬性，並提供包含已更新屬性的JSON裝載，藉此修改和更新現有引擎。

>[!NOTE]
>
>為確保此PUT要求成功，建議您先執行GET要求，以[依ID](#retrieve-specific)擷取引擎。 然後，修改和更新返回的 JSON 物件，並將整個修改後的 JSON 物件應用為PUT 要求的有效負載。

以下範例 API 呼叫將更新引擎的名稱和描述，同時最初具有這些屬性：

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API格式**

```https
PUT /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的識別碼。 |

**要求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**回應**

成功的回應會傳回包含引擎更新詳細資料的裝載。

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 刪除引擎

您可以在請求路徑中指定DELETE引擎的ID時，透過執行目標請求來刪除引擎。 刪除引擎將會階層式刪除參照該引擎的所有MLInstances，包括屬於這些MLInstances的所有實驗與實驗執行。

**API格式**

```https
DELETE /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的識別碼。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
