---
keywords: Experience Platform；屬性；訪問分數；熱門主題；下載分數；屬性分數；導出；；屬性分數；訪問分數；熱門主題；下載分數；屬性分數；導出
feature: Attribution AI
title: 下載Attribution AI中的分數
description: 本文檔是下載Attribution AI分數的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 2%

---

# 下載Attribution AI分數

本文檔是下載Attribution AI分數的指南。

## 快速入門

Attribution AI允許您下載Parke檔案格式的分數。 本教程要求您已閱讀並完成下載Attribution AI分數部分。 [開始](./getting-started.md) 的子菜單。

此外，為了訪問Attribution AI的分數，您需要有一個運行狀態成功的服務實例。 要建立新服務實例，請訪問 [Attribution AI使用手冊](./user-guide.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和評分，請允許它24小時才能完成運行。

## 查找您的資料集ID {#dataset-id}

在您的服務實例中，按一下「Attribution AI見解」 *更多操作* 從右上角導航下拉，然後選擇 **[!UICONTROL 訪問分數]**。

![更多操作](./images/download-scores/more-actions.png)

此時將出現一個新對話框，其中包含下載分數文檔和當前實例的資料集ID的連結。 將資料集ID複製到剪貼簿，然後繼續下一步。

![資料集 ID](../customer-ai/images/download-scores/access-scores.png)

## 檢索批ID {#retrieve-your-batch-id}

使用上一步中的資料集ID，需要調用目錄API以檢索批ID。 此API調用使用附加查詢參數，以返回最新成功的批，而不是屬於您組織的批的清單。 要返回附加批，請增加 `limit` 查詢參數到要返回的所需金額。 有關可用查詢參數類型的詳細資訊，請訪問上的指南 [使用查詢參數篩選目錄資料](../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「訪問分數」對話框中可用的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含批ID對象的負載。 在本示例中，返回的對象的鍵值是批ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製批ID以在下次API調用中使用。

>[!NOTE]
>
> 以下答復已 `tags` 對象進行了重構，以獲得可讀性。

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

## 使用批ID檢索下一個API調用 {#retrieve-the-next-api-call-with-your-batch-id}

一旦您擁有了批ID，您就可以發出新的GET請求 `/batches`。 該請求返回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中檢索的批ID [檢索批ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批ID，發出以下請求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含 `_links` 的雙曲餘切值。 在 `_links` 對象是 `href` 將新API調用作為其值。 複製此值以繼續執行下一步。

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

## 檢索檔案 {#retrieving-your-files}

使用 `href` 作為API調用在上一步中獲得的值，請發出新的GET請求以檢索檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在中返回dataSetFile ID `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id)。 在 `data` 對象類型下的陣列 `dataSetFileId`。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能具有一個條目，或者包含屬於該目錄的檔案清單。 下面的示例包含檔案清單，並已壓縮可讀性。 在此方案中，您需要遵循每個檔案的URL才能訪問該檔案。

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


複製 `href` 值 `data` 陣列，然後繼續下一步。

## 下載檔案資料

要下載檔案資料，請向 `"href"` 上一步中複製的值 [正在檢索檔案](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令行中發出此請求，可能會提示您在請求標題後添加輸出。 以下請求示例使用 `--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在中返回dataSetFile ID `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id)。 |
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
>在發出GET請求之前，請確保您所在的目錄或資料夾正確。

**回應**

響應將下載您在當前目錄中請求的檔案。 在本示例中，檔案名為&quot;file.parce&quot;。

![終端](./images/download-scores/terminal-output.png)

下載的分數將採用鑲木格式，或者需要 [!DNL Spark]-shell或Parket讀取器查看分數。 對於原始分數查看，您可以使用 [Apache鑲木工具](https://parquet.apache.org/docs/)。 鑲木工具可以使用 [!DNL Spark]。

## 後續步驟

本文檔概述了下載Attribution AI分數所需的步驟。 有關分數輸出的詳細資訊，請訪問 [屬性AI輸入和輸出](./input-output.md) 文檔。

## 使用Snowflake訪問分數

>[!IMPORTANT]
>
>有關使用Snowflake訪問分數的詳細資訊，請聯繫attributionai-support@adobe.com。

您可以通過Snowflake訪問聚合Attribution AI分數。 目前，您需要通過電子郵件將Adobe支援發送到attributionai-support@adobe.com，以便設定和接收您的讀者帳戶的憑據以進行Snowflake。

一旦Adobe支援處理了您的請求，您將獲得要Snowflake的讀取器帳戶的URL以及下面的相應憑據：

- SnowflakeURL
- 用戶名
- 密碼

>[!NOTE]
>
>讀取器帳戶用於使用支援JDBC連接器的SQL客戶端、工作表和BI解決方案查詢資料。

一旦您擁有了憑據和URL，您就可以查詢模型表，按觸點日期或轉換日期進行聚合。

### 在Snowflake中查找架構

使用提供的憑據登錄到Snowflake。 按一下 **工作表** 頁籤，然後導航到左面板中的資料庫目錄。

![工作表和導航](./images/download-scores/edited_snowflake_1.png)

下一步，按一下 **選擇方案** 在螢幕右上角。 在出現的跨距中，確認您選擇了正確的資料庫。 接下來，按一下 *架構* 下拉並選擇列出的方案之一。 您可以直接從選定方案下列出的分數表中查詢。

![查找架構](./images/download-scores/edited_snowflake_2.png)

## 將PowerBI連接到Snowflake（可選）

您的Snowflake憑據可用於在PowerBI Desktop和Snowflake資料庫之間建立連接。

首先，在 *伺服器* 框中，鍵入SnowflakeURL。 下一個，下 *倉庫*，鍵入「XSMALL」。 然後，鍵入用戶名和密碼。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立連接後，選擇Snowflake資料庫，然後選擇相應的架構。 現在可以載入所有表。
