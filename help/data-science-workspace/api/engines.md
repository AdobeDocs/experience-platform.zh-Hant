---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；引擎；感性機器學習api
solution: Experience Platform
title: 引擎API終結點
description: 引擎是資料科學工作區中機器學習模型的基礎。 它們包含可解決特定問題的機器學習算法、用於執行特徵工程的特徵管線，或兩者兼有。
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---

# 引擎端點

引擎是資料科學工作區中機器學習模型的基礎。 它們包含可解決特定問題的機器學習算法、用於執行特徵工程的特徵管線，或兩者兼有。

## 查找您的Docker註冊表

>[!TIP]
>
>如果您沒有Docker URL，請訪問 [將源檔案打包到處方](../models-recipes/package-source-files-recipe.md) 有關建立Docker主機URL的逐步步驟的教程。

要上載打包的處方檔案，需要您的Docker註冊表憑據，包括您的Docker主機URL、用戶名和密碼。 您可以通過執行以下GET請求來查找此資訊：

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

成功的響應返回包含Docker註冊表詳細資訊（包括Docker URL）的負載(`host`)，用戶名(`username`)和密碼(`password`)。

>[!NOTE]
>
>您的Docker密碼隨時更改 `{ACCESS_TOKEN}` 。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL建立引擎 {#docker-image}

您可以通過在提供元資料和引用多部件表單中Docker影像的Docker URL的同時執行POST請求來建立引擎。

**API格式**

```https
POST /engines
```

**請求Python/R**

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
| `name` | 引擎的所需名稱。 與此引擎對應的處方將繼承此值，該值將作為處方名稱顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的處方將繼承此值，該值將作為處方說明顯示在UI中。 此為必要屬性。如果不想提供說明，請將其值設定為空字串。 |
| `type` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |
| `algorithm` | 指定機器學習算法類型的字串。 支援的算法類型包括「分類」、「回歸」或「自定義」。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |

**請求PySpark/Scala**

在請求PySpark配方時， `executionType` 和 `type` 是&quot;PySpark&quot; 請求斯卡拉食譜時， `executionType` 和 `type` 是&quot;火花&quot; 以下Scala配方示例使用Spark:

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
| `name` | 引擎的所需名稱。 與此引擎對應的處方將繼承此值，該值將作為處方名稱顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的處方將繼承此值，該值將作為處方說明顯示在UI中。 此為必要屬性。如果不想提供說明，請將其值設定為空字串。 |
| `type` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 該值可設定為「Spark」或「PySpark」。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 此欄位必須設定為 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker影像的位置。 僅支援AzureACR或Public（未驗證）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 這可以是「Spark」或「PySpark」。 |

**回應**

成功的響應返回包含新建立引擎的詳細資訊（包括其唯一標識符）的負載(`id`)。 以下示例響應是Python引擎。 所有引擎響應都遵循以下格式：

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

## 使用Docker URL建立特徵管線引擎 {#feature-pipeline-docker}

通過在提供其元資料和引用Docker影像的Docker URL的同時執行POST請求，可以建立功能管線引擎。

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
| `type` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 該值可設定為「Spark」或「PySpark」。 |
| `algorithm` | 所使用的算法，將此值設定為 `fp` （特徵管線）。 |
| `name` | 特徵管線引擎的所需名稱。 與此引擎對應的處方將繼承此值，該值將作為處方名稱顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的處方將繼承此值，該值將作為處方說明顯示在UI中。 此為必要屬性。如果不想提供說明，請將其值設定為空字串。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 此欄位必須設定為 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker影像的位置。 僅支援AzureACR或Public（未驗證）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 這可以是「Spark」或「PySpark」。 |
| `artifacts.default.image.packagingType` | 引擎的包裝類型。 此值應設定為 `docker`。 |
| `artifacts.default.defaultMLInstanceConfigs` | 您 `pipeline.json` 配置檔案參數。 |

**回應**

成功的響應返回包含新建立的功能管道引擎詳細資訊（包括其唯一標識符）的負載(`id`)。 以下示例響應是PySpark特徵管道引擎。

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

## 檢索引擎清單

通過執行單個GET請求，可以檢索引擎清單。 要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

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

成功的響應返回引擎及其詳細資訊的清單。

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

通過執行請求路徑中包含所需引擎ID的GET請求，可以檢索特定引擎的詳細資訊。

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

成功的響應返回包含所需引擎詳細資訊的負載。

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

您可以通過PUT請求覆蓋現有引擎的屬性來修改和更新現有引擎，該請求在請求路徑中包括目標引擎的ID，並提供包含已更新屬性的JSON負載。

>[!NOTE]
>
>為確保此PUT請求成功，建議您首先執行GET請求， [按ID檢索引擎](#retrieve-specific)。 然後，修改和更新返回的JSON對象，並應用已修改的JSON對象的整個作為PUT請求的負載。

以下示例API調用將在最初具有這些屬性時更新引擎的名稱和說明：

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
| `{ENGINE_ID}` | 現有引擎的ID。 |

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

成功的響應返回包含引擎更新的詳細資訊的負載。

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

在請求路徑中指定目標引擎的ID時，可通過執行DELETE請求來刪除引擎。 刪除引擎將級聯刪除引用該引擎的所有MLInstance，包括屬於這些MLInstance的任何「實驗」和「實驗」運行。

**API格式**

```https
DELETE /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的ID。 |

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
