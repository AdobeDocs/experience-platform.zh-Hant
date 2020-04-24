---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 引擎
topic: Developer guide
translation-type: tm+mt
source-git-commit: 45f310eb5747300e13f3c57b3f979c983a03d49d

---


# 引擎

引擎是資料科學工作區中機器學習模型的基礎。 它們包含可解決特定問題的機器學習演算法、可執行特徵工程的特徵管線，或兩者皆可。

## 查找您的Docker註冊表

>[!TIP]
>如果您沒有Docker URL，請造訪 [Package source files into a recipe](../models-recipes/package-source-files-recipe.md) tutorial，以取得建立Docker主機URL的逐步逐步說明。

您的Docker註冊表憑證是上傳封裝的Recipe檔案（包括您的Docker主機URL、使用者名稱和密碼）所必需的。 您可以執行下列GET請求來查閱此資訊：

**API格式**

```https
GET /engines/dockerRegistry
```

**請求**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含Docker註冊表詳細資訊的裝載，包括Docker URL(`host`)、用戶名(`username`)和密碼(`password`)。

>[!NOTE]
>每當您的Docker密碼更新時， `{ACCESS_TOKEN}` 密碼就會變更。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL建立引擎 {#docker-image}

您可以執行POST請求，同時提供中繼資料和Docker URL，以多部分表單引用Docker影像，以建立引擎。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
                    "location": "{DOCKER_URL}",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `type` | 引擎的執行類型。 此值對應於Docker映像所基於的語言，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |
| `algorithm` | 指定機器學習演算法類型的字串。 支援的演算法類型包括「分類」、「回歸」或「自訂」。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker映像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值對應於Docker映像所基於的語言，可以是&quot;Python&quot;、&quot;R&quot;或&quot;Tensorflow&quot;。 |

**要求PySpark/Scala**

提出PySpark配方要求時， `executionType` 和 `type` 是「PySpark」。 提出Scala配方要求時， `executionType` 和 `type` 是「Spark」。 下列Scala配方範例使用Spark:

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
| `type` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 此值可設為Spark或PySpark。 |
| `mlLibrary` | 建立PySpark和Scala配方的引擎時所需的欄位。 此欄位必須設定為 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker映像的位置。 僅支援Azure ACR或Public（未驗證）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 這可以是「Spark」或「PySpark」。 |

**回應**

成功的回應會傳回包含新建立之引擎詳細資料（包括其唯一識別碼）的裝載`id`。 以下是Python引擎的範例回應。 所有引擎回應都遵循下列格式：

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

## 使用Docker URL建立功能管線引擎 {#feature-pipeline-docker}

您可以通過執行POST請求來建立功能管線引擎，同時提供其元資料和引用Docker影像的Docker URL。

**API格式**

```https
POST /engines
```

**請求**

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
           "defaultMLInstanceConfigs": [
           ]
       }
   }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 此值可設為Spark或PySpark。 |
| `algorithm` | 使用的演算法，請將此值設 `fp` 為（特徵管線）。 |
| `name` | 特徵管線引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `mlLibrary` | 建立PySpark和Scala配方的引擎時所需的欄位。 此欄位必須設定為 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker映像的位置。 僅支援Azure ACR或Public（未驗證）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與Docker映像所基於的語言相對應。 這可以是「Spark」或「PySpark」。 |
| `artifacts.default.image.packagingType` | 引擎的封裝類型。 此值應設為 `docker`。 |

**回應**

成功的回應會傳回包含新建立之功能管道引擎詳細資料（包括其唯一識別碼）的裝載`id`值。 以下是PySpark特徵管線引擎的示例響應。

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
            }
        }
    }
}
```

## 擷取引擎清單

您可以執行單一GET請求來擷取引擎清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱有關資產檢索查 [詢參數的附錄部分](./appendix.md#query)。

**API格式**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回引擎清單及其詳細資訊。

```json
{
    "children": [
        {
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

您可以執行GET請求，在請求路徑中包含所需引擎的ID，以擷取特定引擎的詳細資訊。

**API格式**

```https
GET /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的ID。 |

**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含所需引擎詳細資料的裝載。

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 更新引擎

您可以透過PUT請求覆寫現有引擎的屬性，以修改和更新現有引擎，該請求在請求路徑中包含目標引擎的ID，並提供包含更新屬性的JSON裝載。

>[!NOTE] 為確保此PUT請求成功，建議您先執行GET請求，以依ID [擷取引擎](#retrieve-specific)。 然後，修改並更新傳回的JSON物件，並套用已修改的JSON物件作為PUT要求的裝載。

下列範例API呼叫會在最初具有這些屬性時更新引擎的名稱和說明：

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

**請求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "id": "{ENGINE_ID}",
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

您可以執行DELETE請求，同時在請求路徑中指定目標引擎的ID，以刪除引擎。 刪除引擎將級聯刪除引用該引擎的所有MLI實例，包括屬於這些MLI實例的任何實驗和實驗運行。

**API格式**

```https
DELETE /engines/{ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 現有引擎的ID。 |

**請求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 不建議使用的請求

>[!IMPORTANT]
>不再支援二進位對象，並將設定為在以後刪除。 新的PySpark和Scala配方現在應依照Docker影 [像範例](#docker-image) ，建立引擎。

## 使用二進位對象建立引擎——已過時

您可以使用本機或二進 `.jar` 位對象來建 `.egg` 立引擎，方法是執行POST請求，同時以多部分形式提供其中繼資料和對象的路徑。

**API格式**

```https
POST /engines
```

**請求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `algorithm` | 指定機器學習演算法類型的字串。 支援的演算法類型包括「分類」、「回歸」或「自訂」。 |
| `type` | 引擎的執行類型。 此值對應於二進位偽影所建立的語言，可以是&quot;PySpark&quot;或&quot;Spark&quot;。 |


**回應**

成功的回應會傳回包含新建立之引擎詳細資料（包括其唯一識別碼）的裝載`id`。

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 使用二進位工件建立功能管線引擎——已過時 {#create-a-feature-pipeline-engine-using-binary-artifacts}

>[!IMPORTANT]
>不再支援二進位對象，並將設定為在以後刪除。

通過執行POST請求，同時以多部 `.jar` 分表單提供元資料 `.egg` 和對象的路徑，可以使用本地或二進位對象建立特徵管線引擎。 PySpark或Spark引擎可指定計算資源，例如內核數或記憶體量。 如需詳細資訊，請參閱 [PySpark和Spark資源設定的附錄](./appendix.md#resource-config) 。

**API格式**

```https
POST /engines
```

**請求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 引擎的所需名稱。 與此引擎對應的配方將繼承此值，並以配方名稱顯示在UI中。 |
| `description` | 引擎的選用說明。 與此引擎對應的方式將繼承此值，並以方式說明的形式顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `algorithm` | 指定機器學習演算法類型的字串。 將此值設定為&quot;fp&quot;，以將此建立指定為「特徵管線引擎」。 |
| `type` | 引擎的執行類型。 此值對應於建立二進位工件時所使用的語言，可以是&quot;PySpark&quot;或&quot;Spark&quot;。 |

**回應**

成功的回應會傳回包含新建立之引擎詳細資料（包括其唯一識別碼）的裝載`id`。

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```
