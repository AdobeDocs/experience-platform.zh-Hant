---
keywords: Experience Platform；attribution ai；存取分數；熱門主題；下載分數；attribution ai分數；匯出；匯出
feature: Attribution AI
title: 以Attribution AI下載分數
description: 本檔案可用作下載Attribution AI分數的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 2%

---

# 下載Attribution AI中的分數

本檔案可用作下載Attribution AI分數的指南。

## 快速入門

Attribution AI可讓您以Parquet檔案格式下載分數。 本教學課程要求您已閱讀並完成[快速入門](./getting-started.md)指南中的Attribution AI分數下載區段。

此外，若要存取Attribution AI分數，您必須有可取得成功執行狀態的服務執行個體。 若要建立新的服務執行個體，請瀏覽[Attribution AI使用手冊](./user-guide.md)。 如果您最近已建立服務執行個體，但仍在訓練和評分中，請等待24小時讓執行完成。

## 尋找您的資料集ID {#dataset-id}

在用於Attribution AI深入分析的服務執行個體中，按一下右上方導覽中的&#x200B;*更多動作*&#x200B;下拉式清單，然後選取&#x200B;**[!UICONTROL 存取分數]**。

![更多動作](./images/download-scores/more-actions.png)

隨即顯示新對話方塊，其中包含下載分數檔案的連結，以及目前執行個體的資料集ID。 將資料集ID複製到剪貼簿，然後繼續下一個步驟。

![資料集識別碼](../customer-ai/images/download-scores/access-scores.png)

## 擷取您的批次識別碼 {#retrieve-your-batch-id}

使用上一步的資料集ID，您需要呼叫目錄API以擷取批次ID。 此API呼叫使用其他查詢引數，以傳回最新的成功批次，而非屬於您組織的批次清單。 若要傳回其他批次，請將`limit`查詢引數的數字增加到您想要傳回的所需數量。 如需有關可用查詢引數型別的詳細資訊，請瀏覽有關[使用查詢引數篩選目錄資料](../../catalog/api/filter-data.md)的指南。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「存取分數」對話方塊中可用的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含批次ID物件的裝載。 在此範例中，傳回物件的Key值是批次ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製您的批次ID以用於下一個API呼叫。

>[!NOTE]
>
> 下列回應已重新格式化`tags`物件以供閱讀。

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

## 使用您的批次ID擷取下一個API呼叫 {#retrieve-the-next-api-call-with-your-batch-id}

取得批次ID後，您就可以向`/batches`提出新的GET請求。 該請求會傳回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中擷取的批次ID [擷取您的批次ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批次ID提出以下請求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應傳回包含`_links`物件的裝載。 在`_links`物件中，是以新API呼叫作為其值的`href`。 複製此值以繼續執行下一個步驟。

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

## 擷取您的檔案 {#retrieving-your-files}

使用您在上一步中取得的`href`值作為API呼叫，提出新的GET要求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案識別碼是從[前一個步驟](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 它也可在物件型別`dataSetFileId`下的`data`陣列中存取。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含資料陣列，其中可能有單一專案，或屬於該目錄的檔案清單。 以下範例包含檔案清單，並經過壓縮以提高可讀性。 在此案例中，您需要遵循每個檔案的URL才能存取該檔案。

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
| `_links.self.href` | 用來下載目錄中檔案的GET要求URL。 |


複製`data`陣列中任何檔案物件的`href`值，然後繼續下一個步驟。

## 下載您的檔案資料

若要下載您的檔案資料，請對在先前步驟[擷取您的檔案](#retrieving-your-files)中複製的`"href"`值發出GET要求。

>[!NOTE]
>
>如果您直接在命令列中提出此請求，系統可能會提示您先在請求標頭後面新增輸出。 下列要求範例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案識別碼是從[前一個步驟](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 |
| `{FILE_NAME}` | 檔案的名稱。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>在發出GET請求之前，請確定您位於要儲存檔案的正確目錄或資料夾中。

**回應**

回應會將您要求的檔案下載到目前目錄中。 在此範例中，檔案名稱為「file.parquet」。

![終端機](./images/download-scores/terminal-output.png)

下載的分數將為Parquet格式，且需要[!DNL Spark]殼層或Parquet讀取器才能檢視分數。 若要檢視原始分數，您可以使用[Apache Parquet工具](https://parquet.apache.org/docs/)。 Parquet工具可以使用[!DNL Spark]分析資料。

## 後續步驟

本檔案概述下載Attribution AI分數所需的步驟。 如需分數輸出的詳細資訊，請瀏覽[Attribtuion AI輸入和輸出](./input-output.md)檔案。

## 使用Snowflake存取分數

>[!IMPORTANT]
>
>如需使用Snowflake存取評分的詳細資訊，請聯絡attributionai-support@adobe.com。

您可以透過Snowflake存取彙總的Attribution AI分數。 目前，您需要透過電子郵件將Adobe支援傳送到attributionai-support@adobe.com，以設定並接收您的Reader帳戶憑證以進行Snowflake。

在Adobe支援處理完您的請求後，系統就會提供一個URL給您Snowflake的讀者帳戶，以及下列的對應憑證：

- SNOWFLAKEURL
- 使用者名稱
- 密碼

>[!NOTE]
>
>Reader帳戶使用支援JDBC聯結器的SQL使用者端、工作表及BI解決方案來查詢資料。

取得認證和URL後，您就可以查詢模型表格、依接觸點日期或轉換日期彙總。

### 在Snowflake中尋找您的結構描述

使用提供的憑證登入Snowflake。 按一下左上方主導覽列中的&#x200B;**工作表**&#x200B;索引標籤，然後導覽至左側面板中的資料庫目錄。

![工作表與導覽](./images/download-scores/edited_snowflake_1.png)

接著，按一下畫面右上角的&#x200B;**選取結構描述**。 在顯示的彈出視窗中，確認您已選取正確的資料庫。 接著，按一下&#x200B;*結構描述*&#x200B;下拉式清單，並選取其中一個列出的結構描述。 您可從選取的綱要下列出的評分表格直接進行查詢。

![尋找結構描述](./images/download-scores/edited_snowflake_2.png)

## 將PowerBI連線至Snowflake （選購）

您可以使用您的Snowflake認證來設定PowerBI Desktop與Snowflake資料庫之間的連線。

首先，在&#x200B;*伺服器*&#x200B;方塊下，輸入您的SnowflakeURL。 接下來，在&#x200B;*倉儲*&#x200B;下，輸入「XSMALL」。 然後，輸入您的使用者名稱和密碼。

![POWERBI範例](./images/download-scores/powerbi-snowflake.png)

建立連線之後，請選取您的Snowflake資料庫，然後選取適當的綱要。 您現在可以載入所有表格。
