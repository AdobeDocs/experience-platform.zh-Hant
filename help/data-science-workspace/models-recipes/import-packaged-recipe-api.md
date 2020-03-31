---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 匯入封裝的方式(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# 匯入封裝的方式(API)

本教學課程使 [用Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 來建立引擎 [](../api/engines.md)，也稱為使用者介面中的方式。

在開始使用之前，請務必注意，Adobe Experience Platform Data Science Workspace使用不同的術語來參照API和UI中的類似元素。 本教學課程中使用API詞語，下表概述相關詞語：

| UI詞語 | API期限 |
| ---- | ---- |
| 配方 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培訓與評估 | [實驗](../api/experiments.md) |
| 服務 | [MLService](../api/mlservices.md) |

引擎包含機器學習演算法和邏輯，以解決特定問題。 下圖顯示資料科學工作區中的API工作流程。 本教學課程著重於建立引擎，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入門

本教學課程需要以二進位對象或Docker URL格式封裝的Recipe檔案。 請依照「 [封裝來源檔案」教學課程](./package-source-files-recipe.md) ，建立封裝的「配方」檔案或提供您自己的「配方」檔案。

- 二進位對象：二進位偽像(如 JAR, EGG)，用於建立引擎。
- `{DOCKER_URL}` :智慧服務的Docker影像的URL位址。

本教學課程要求您完成「 [Adobe Experience Platform驗證」教學課程](../../tutorials/authentication.md) ，才能成功呼叫平台API。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- `{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。
- `{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。
- `{API_KEY}`:您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。

## 建立引擎

根據要包含在API請求中的封裝方式檔案的形式，引擎會透過下列兩種方式之一建立：
- [使用二進位對象建立引擎](#create-an-engine-with-a-binary-artifact)
- [使用Docker URL建立引擎](#create-an-engine-with-a-docker-url)

### 使用二進位對象建立引擎

要使用本地打包或二進位對象建立引 `.jar` 擎， `.egg` 必須提供本地檔案系統中二進位對象檔案的絕對路徑。 考慮導航到終端環境中包含二進位對象的目錄，並執行絕對路徑的 `pwd` Unix命令。

下列呼叫會建立含二進位物件的引擎：

#### API格式

```http
POST /engines
```

#### 請求

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` :引擎的所需名稱。 與此引擎對應的配方將繼承此值，該值將作為配方的名稱顯示在資料科學工作區用戶介面中。
- `engine > description` :引擎的選用說明。 與此引擎對應的配方將繼承此值，該值將作為配方的說明顯示在Data Science Workspace用戶介面中。 請勿移除此屬性，如果您選擇不提供說明，請讓此值為空字串。
- `engine > type`:引擎的執行類型。 此值與在中開發二進位偽像的語言相對應。

   >[!NOTE] 上載二進位對象以建立引擎時， `type` 為 `Spark` 或 `PySpark`。

- `defaultArtifact` :用於建立引擎的二進位對象檔案的絕對路徑。

   >[!NOTE] 請確定在檔 `@` 案路徑之前加入。

#### 回應

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

成功的回應會顯示JSON裝載，內含有關新建引擎的資訊。 此 `id` 鍵代表唯一的引擎識別碼，並在下一個教學課程中用來建立MLInstance。 請確定引擎識別碼已儲存，然後再繼續進 [行後續步驟](#next-steps)。

### 使用Docker URL建立引擎

若要建立具有儲存在Docker容器中之封裝配方檔案的引擎，您必須為封裝配方檔案提供Docker URL。

下列呼叫會建立具有Docker URL的引擎：

#### API格式

```http
POST /engines
```

#### 請求

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

- `engine > name` :引擎的所需名稱。 與此引擎對應的配方將繼承此值，該值將作為配方的名稱顯示在資料科學工作區用戶介面中。
- `engine > description` :引擎的選用說明。 與此引擎對應的配方將繼承此值，該值將作為配方的說明顯示在Data Science Workspace用戶介面中。 請勿移除此屬性，如果您選擇不提供說明，請讓此值為空字串。
- `engine > type`:引擎的執行類型。 此值與Docker影像開發所用的語言相對應。

   >[!NOTE] 當提供Docker URL來建立引擎時， `type` 為 `Python`、 `R`或 `Tensorflow`。

- `artifacts > default > image > location` :你 `{DOCKER_URL}` 來這。 完整的Docker URL具有下列結構：

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` :Docker映像檔案的附加名稱。 請勿移除此屬性，如果您選擇不提供其他Docker影像檔名，請讓此值為空字串。
- `artifacts > default > image > executionType` :此引擎的執行類型。 此值與Docker影像開發所用的語言相對應。

   >[!NOTE] 當提供Docker URL來建立引擎時， `executionType` 為 `Python`、 `R`或 `Tensorflow`。

#### 回應

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

成功的回應會顯示JSON裝載，內含有關新建引擎的資訊。 此 `id` 鍵代表唯一的引擎識別碼，並在下一個教學課程中用來建立MLInstance。 請確定引擎識別碼已儲存，然後再繼續後續步驟。

## 後續步驟

您已使用API建立引擎，並取得唯一的引擎識別碼作為回應本體的一部分。 在下一個教學課程中，您可以使用此引擎識別碼，學習如 [何使用API建立、訓練和評估模型](./train-evaluate-model-api.md)。