---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；引擎；sensei機器學習api
solution: Experience Platform
title: 引擎API端點
description: 引擎是資料科學Workspace中機器學習模型的基礎。 它們包含解決特定問題的機器學習演演算法、執行特徵工程的特徵配管或兩者。
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 2%

---

# 引擎端點

引擎是資料科學Workspace中機器學習模型的基礎。 它們包含解決特定問題的機器學習演演算法、執行特徵工程的特徵配管或兩者。

## 查詢您的Docker登錄檔

>[!TIP]
>
>如果您沒有Docker URL，請造訪[將來源檔案封裝到配方](../models-recipes/package-source-files-recipe.md)教學課程中，以逐步瞭解如何建立Docker主機URL。

需要Docker登入認證才能上傳封裝的配方檔案，包括您的Docker主機URL、使用者名稱和密碼。 您可以透過執行以下GET請求來查詢此資訊：

**API格式**

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
>每當`{ACCESS_TOKEN}`更新時，您的Docker密碼都會變更。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL建立引擎 {#docker-image}

您可以透過執行POST請求來建立引擎，同時提供其中繼資料以及參照多部分表單中Docker影像的Docker URL。

**API格式**

```https
POST /engines
```

**要求Python/R**

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

**要求PySpark/Scala**

請求PySpark配方時，`executionType`和`type`為「PySpark」。 請求Scala配方時，`executionType`和`type`為「Spark」。 下列Scala配方範例使用Spark：

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
| `type` | 引擎的執行型別。 此值對應於構建Docker映像的語言。 此值可設為Spark或PySpark。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 此欄位必須設定為`databricks-spark`。 |
| `artifacts.default.image.location` | Docker映像的位置。 僅支援Azure ACR或公用（未驗證） Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於構建Docker映像的語言。 這可以是&quot;Spark&quot;或&quot;PySpark&quot;。 |

**回應**

成功的回應會傳回承載，其中包含新建立之引擎的詳細資料，包括其唯一識別碼(`id`)。 以下範例回應適用於Python引擎。 所有引擎回應都遵循此格式：

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

## 使用Docker URL建立功能管道引擎 {#feature-pipeline-docker}

您可以透過執行POST請求來建立功能管道引擎，同時提供其中繼資料和參考Docker影像的Docker URL。

**API格式**

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
| `type` | 引擎的執行型別。 此值對應於構建Docker映像的語言。 此值可設為Spark或PySpark。 |
| `algorithm` | 正在使用的演演算法，將此值設定為`fp` （功能管道）。 |
| `name` | 特徵配管引擎的所需名稱。 對應至此引擎的配方將繼承此值，以作為配方名稱顯示在UI中。 |
| `description` | 「引擎」的選擇性說明。 對應至此引擎的配方將繼承此值，以作為配方說明顯示在UI中。 此屬性為必要項。 如果您不想要提供說明，請將其值設為空字串。 |
| `mlLibrary` | 建立PySpark和Scala配方引擎時所需的欄位。 此欄位必須設定為`databricks-spark`。 |
| `artifacts.default.image.location` | Docker映像的位置。 僅支援Azure ACR或公用（未驗證） Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行型別。 此值對應於構建Docker映像的語言。 這可以是&quot;Spark&quot;或&quot;PySpark&quot;。 |
| `artifacts.default.image.packagingType` | 引擎的封裝型別。 此值應設為`docker`。 |
| `artifacts.default.defaultMLInstanceConfigs` | 您的`pipeline.json`組態檔引數。 |

**回應**

成功的回應會傳回承載，其中包含新建立功能管道引擎的詳細資料，包括其唯一識別碼(`id`)。 下列範例回應適用於PySpark特徵配管引擎。

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

您可以透過執行單一GET請求來擷取引擎清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

**API格式**

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

成功的回應會傳回引擎清單及其詳細資料。

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

### 擷取特定引擎 {#retrieve-specific}

您可以透過執行GET請求（包含請求路徑中所需引擎的ID）來擷取特定引擎的詳細資訊。

**API格式**

```https
GET /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的識別碼。 |

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
>為確保此PUT要求成功，建議您先執行GET要求，以[依ID](#retrieve-specific)擷取引擎。 然後，修改和更新傳回的JSON物件，並套用整個修改的JSON物件作為PUT請求的裝載。

以下範例API呼叫最初具有這些屬性時會更新引擎的名稱和說明：

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
