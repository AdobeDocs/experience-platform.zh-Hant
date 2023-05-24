---
keywords: Experience Platform；導入打包的配方；資料科學工作區；熱門主題；配方；api;sensei machine learning;create engine
solution: Experience Platform
title: 使用Sensei機器學習API導入打包的配方
type: Tutorial
description: 本教程使用Sensei機器學習API建立引擎，也稱為用戶介面中的配方。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# 使用Sensei機器學習API導入打包的配方

本教程使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 建立 [引擎](../api/engines.md)，也稱為用戶介面中的配方。

在開始之前，必須指出Adobe Experience Platform [!DNL Data Science Workspace] 使用不同術語來引用API和UI中的類似元素。 API術語在本教程中使用，下表概述了相關術語：

| UI術語 | API術語 |
| ---- | ---- |
| 食譜 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培訓和評價 | [實驗](../api/experiments.md) |
| 服務 | [MLService](../api/mlservices.md) |

一個引擎包含機器學習算法和邏輯來解決特定問題。 下圖提供了一個顯示中API工作流的可視化 [!DNL Data Science Workspace]。 本教程重點介紹如何建立「引擎」，即機器學習模型的大腦。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入門

本教程要求以Docker URL形式打包的配方檔案。 關注 [將源檔案打包到配方](./package-source-files-recipe.md) 教程，建立打包的配方檔案或提供您自己的配方檔案。

- `{DOCKER_URL}`:智慧服務的Docker映像的URL地址。

本教程要求您完成 [驗證Adobe Experience Platform教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] API。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- `{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。
- `{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。
- `{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。

## 建立引擎

通過向/engines端點發出POST請求，可以建立引擎。 建立的引擎基於打包的處方檔案的形式進行配置，這些檔案必須作為API請求的一部分包含。

### 使用Docker URL建立引擎 {#create-an-engine-with-a-docker-url}

為了建立具有儲存在Docker容器中的打包處方檔案的引擎，必須為打包的處方檔案提供Docker URL。

>[!CAUTION]
>
> 如果您使用 [!DNL Python] 或者使用以下請求。 如果使用PySpark或Scala，請使用位於Python/R示例下方的PySpark/Scala請求示例。

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
| `engine.name` | 引擎的所需名稱。 與此引擎對應的處方將繼承此值，顯示在 [!DNL Data Science Workspace] 用戶介面作為處方名稱。 |
| `engine.description` | 引擎的可選說明。 與此引擎對應的處方將繼承此值，顯示在 [!DNL Data Science Workspace] 用戶介面，作為處方說明。 不要刪除此屬性，如果選擇不提供說明，則讓此值為空字串。 |
| `engine.type` | 引擎的執行類型。 此值與在中開發Docker影像的語言相對應。 當提供Docker URL以建立引擎時， `type` 或 `Python`。 `R`。 `PySpark`。 `Spark` （斯卡拉），或 `Tensorflow`。 |
| `artifacts.default.image.location` | 您 `{DOCKER_URL}` 到這裡。 完整的Docker URL具有以下結構： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker映像檔案的附加名稱。 不要刪除此屬性，如果選擇不提供其他Docker映像檔案名，則讓此值為空字串。 |
| `artifacts.default.image.executionType` | 此引擎的執行類型。 此值與在中開發Docker影像的語言相對應。 當提供Docker URL以建立引擎時， `executionType` 或 `Python`。 `R`。 `PySpark`。 `Spark` （斯卡拉），或 `Tensorflow`。 |

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
| `name` | 引擎的所需名稱。 與此引擎對應的處方將繼承此值，該值將作為處方名稱顯示在UI中。 |
| `description` | 引擎的可選說明。 與此引擎對應的處方將繼承此值，該值將作為處方說明顯示在UI中。 此為必要屬性。如果不想提供說明，請將其值設定為空字串。 |
| `type` | 引擎的執行類型。 此值與在「PySpark」上構建Docker映像的語言相對應。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與在「Spark」上構建Docker映像的語言相對應。 |

**請求斯卡拉**

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
| `type` | 引擎的執行類型。 此值與在「Spark」上構建Docker映像的語言相對應。 |
| `mlLibrary` | 為PySpark和Scala配方建立引擎時所需的欄位。 |
| `artifacts.default.image.location` | 由Docker URL連結到的Docker影像的位置。 |
| `artifacts.default.image.executionType` | 引擎的執行類型。 此值與在「Spark」上構建Docker映像的語言相對應。 |

**回應**

成功的響應返回包含新建立引擎的詳細資訊（包括其唯一標識符）的負載(`id`)。 以下示例響應是 [!DNL Python] 引擎。 的 `executionType` 和 `type` 鍵會根據提供的POST更改。

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

成功的響應顯示JSON負載，其中包含有關新建立的引擎的資訊。 的 `id` key表示唯一的引擎標識符，在下一教程中建立MLInstance是必需的。 確保在繼續執行後續步驟之前保存引擎標識符。

## 後續步驟 {#next-steps}

您已使用API建立了引擎，並且作為響應主體的一部分獲得了唯一的引擎標識符。 在學習如何進行下一教程時，可以使用此引擎標識符 [使用API建立、訓練和評估模型](./train-evaluate-model-api.md)。
