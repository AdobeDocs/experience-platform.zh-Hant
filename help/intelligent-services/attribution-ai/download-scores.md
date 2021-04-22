---
keywords: Experience Platform；歸因ai；訪問分數；熱門主題；下載分數；歸因ai分數；導出；導出
solution: Experience Platform, Intelligent Services
title: 下載Attribution AI中的分數
topic-legacy: Downloading scores
description: 本檔案可做為下載Attribution AI分數的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---

# 下載Attribution AI分數

本檔案可做為下載Attribution AI分數的指南。

## 快速入門

Attribution AI可讓您下載Parce檔案格式的分數。 本教學課程要求您已閱讀並完成[快速入門](./getting-started.md)指南中的下載Attribution AI分數區段。

此外，若要存取Attribution AI的分數，您必須有成功執行狀態的服務例項可供使用。 要建立新服務實例，請訪問[Attribution AI使用手冊](./user-guide.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

## 尋找您的資料集ID {#dataset-id}

在您的服務例項中，按一下右上方導覽中的&#x200B;*更多動作*&#x200B;下拉式清單，然後選取&#x200B;**[!UICONTROL Access scores]**。

![更多動作](./images/download-scores/more-actions.png)

此時會出現新對話方塊，其中包含下載分數檔案的連結以及目前例項的資料集ID。 將資料集ID複製至剪貼簿，然後繼續下一步驟。

![資料集 ID](../customer-ai/images/download-scores/access-scores.png)

## 擷取您的批次ID {#retrieve-your-batch-id}

使用上一步的資料集ID，您必須呼叫目錄API以擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回最新成功的批次，而非屬於您組織的批次清單。 要返回其他批，請將`limit`查詢參數的數量增加到希望返回的所需金額。 有關可用查詢參數類型的詳細資訊，請訪問[使用查詢參數](../../catalog/api/filter-data.md)過濾目錄資料的指南。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「存取分數」對話方塊中提供的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含批次ID物件的裝載。 在此示例中，返回對象的鍵值是批ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製您的批次ID以用於下一個API呼叫。

>[!NOTE]
>
> 以下響應已對`tags`對象進行了可讀性重新格式化。

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5e8f81cf7a4ecb28a8d85b22"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## 使用您的批次ID {#retrieve-the-next-api-call-with-your-batch-id}擷取下一個API呼叫

一旦擁有批次ID，您就可以向`/batches`提出新的GET請求。 請求會傳回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步[中擷取的批次ID會擷取您的批次ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批次ID，請提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含`_links`對象的裝載。 在`_links`物件中是`href`，其值是新的API呼叫。 複製此值以繼續下一步。

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## 檢索檔案{#retrieving-your-files}

使用您在上一步驟中取得的`href`值做為API呼叫，提出新的GET請求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID會從[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 在`data`陣列中，對象類型`dataSetFileId`下也可以訪問它。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能包含一個條目，或是屬於該目錄的檔案清單。 以下範例包含檔案清單，並已壓縮為可讀性。 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `_links.self.href` | 用於下載目錄中檔案的GET請求URL。 |


複製`data`陣列中任何檔案對象的`href`值，然後繼續執行下一步。

## 下載您的檔案資料

若要下載檔案資料，請向您在上一步驟[中複製的`"href"`值提出GET要求，以擷取您的檔案](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令列中提出此請求，可能會提示您在請求標題後新增輸出。 下列請求範例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID會從[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 |
| `{FILE_NAME}` | 檔案的名稱。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>在提出GET請求之前，請確定您位在您要儲存檔案的正確目錄或資料夾中。

**回應**

回應會下載您在目前目錄中要求的檔案。 在此示例中，檔案名為&quot;file.parce&quot;。

![終端](./images/download-scores/terminal-output.png)

下載的分數將採用Parce格式，需要[!DNL Spark]-shell或Parce閱讀器才能檢視分數。 對於原始分數檢視，您可以使用[Apache Parce Parce工具](https://github.com/apache/parquet-mr/tree/master/parquet-tools)。 拼花工具可以使用[!DNL Spark]分析資料。

## 後續步驟

本檔案概述了下載Attribution AI分數所需的步驟。 有關分數輸出的更多資訊，請造訪[屬性AI輸入與輸出](./input-output.md)檔案。

## 使用Snowflake存取分數

>[!IMPORTANT]
>
>如需使用Snowflake存取分數的詳細資訊，請聯絡attributionai-support@adobe.com。

您可以透過Attribution AI存取匯總的Snowflake分數。 目前，您需要以電子郵件寄送Adobe支援至attributionai-support@adobe.com，才能設定並接收您的SnowflakeReader帳戶的認證。

在Adobe支援處理您的請求後，會提供您要Snowflake的讀者帳戶URL，以及下列相應的認證：

- SnowflakeURL
- 使用者名稱
- 密碼

>[!NOTE]
>
>Reader帳戶是使用支援JDBC連接器的SQL客戶端、工作表和BI解決方案查詢資料。

一旦擁有認證和URL，您就可以查詢模型表格、依觸點日期或轉換日期進行匯總。

### 在Snowflake中查找結構

使用提供的憑據，登錄到Snowflake。 按一下左上角主導航中的&#x200B;**工作表**&#x200B;頁籤，然後導航到左面板中的資料庫目錄。

![工作表與導覽](./images/download-scores/edited_snowflake_1.png)

接著，按一下畫面右上角的「選擇架構」。 ****&#x200B;在出現的快顯視窗中，確認您已選取正確的資料庫。 接著，按一下&#x200B;*Schema*&#x200B;下拉式清單，並選取其中一個列出的結構。 您可以直接從所選方案下列出的分數表中查詢。

![查找架構](./images/download-scores/edited_snowflake_2.png)

## 將PowerBI連接到Snowflake（可選）

您的Snowflake憑證可用於設定PowerBI Desktop和Snowflake資料庫之間的連接。

首先，在&#x200B;*Server*&#x200B;方塊下，輸入您的SnowflakeURL。 接著，在&#x200B;*Warehouse*&#x200B;下，輸入&quot;XSMALL&quot;。 然後，輸入您的使用者名稱和密碼。

![POWERBI範例](./images/download-scores/powerbi-snowflake.png)

建立連接後，選擇Snowflake資料庫，然後選擇適當的方案。 您現在可以載入所有表格。
