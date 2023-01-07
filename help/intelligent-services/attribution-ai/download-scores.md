---
keywords: Experience Platform；歸因ai；存取分數；熱門主題；下載分數；歸因ai分數；匯出；匯出
feature: Attribution AI
title: 下載分數(以Attribution AI表示)
description: 本檔案可供下載Attribution AI分數的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 2%

---

# 下載分數(以Attribution AI表示)

本檔案可供下載Attribution AI分數的指南。

## 快速入門

Attribution AI可讓您以Parquet檔案格式下載分數。 本教學課程需要您已閱讀並完成下載Attribution AI分數區段，位於 [快速入門](./getting-started.md) 指南。

此外，若要存取Attribution AI的分數，您必須有一個可使用成功執行狀態的服務執行個體。 若要建立新的服務例項，請造訪 [Attribution AI使用指南](./user-guide.md). 如果您最近建立了一個服務實例，但該實例仍在訓練和分數中，請允許24小時以完成運行。

## 尋找資料集ID {#dataset-id}

在您的服務例項中，按一下以取得Attribution AI分析 *更多動作* 右上方導覽的下拉式清單，然後選取 **[!UICONTROL 存取分數]**.

![更多動作](./images/download-scores/more-actions.png)

隨即出現新的對話方塊，其中包含下載分數檔案的連結以及您目前執行個體的資料集ID。 將資料集ID複製到剪貼簿，然後繼續下一步。

![資料集 ID](../customer-ai/images/download-scores/access-scores.png)

## 擷取批次ID {#retrieve-your-batch-id}

若要使用上一步驟的資料集ID，您必須呼叫目錄API，才能擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回最新成功批次，而非屬於您組織的批次清單。 要返回其他批，請增加 `limit` 查詢參數至您要傳回的所需金額。 如需可用查詢參數類型的詳細資訊，請參閱 [使用查詢參數篩選目錄資料](../../catalog/api/filter-data.md).

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

成功的回應會傳回包含批次ID物件的裝載。 在此範例中，傳回物件的索引鍵值為批次ID `01E5QSWCAASFQ054FNBKYV6TIQ`. 複製您的批次ID以用於下一個API呼叫。

>[!NOTE]
>
> 下列回應已 `tags` 物件已重新格式化以利閱讀。

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

取得批次ID後，您就可以向 `/batches`. 請求會傳回一個連結，用作下一個API請求。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步驟中擷取的批次ID [擷取批次ID](#retrieve-your-batch-id). |

**要求**

使用您自己的批次ID，提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含 `_links` 物件。 在 `_links` 物件是 `href` 以新API呼叫作為其值。 複製此值以繼續執行下一個步驟。

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

使用 `href` 您在上一個步驟中以API呼叫取得的值，請提出新的GET要求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). 您也可以在 `data` 物件類型下的陣列 `dataSetFileId`. |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能包含一個條目，或該目錄下的檔案清單。 以下範例包含檔案清單，並已壓縮以供閱讀。 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

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
| `_links.self.href` | 用於下載目錄中檔案的GET要求URL。 |


複製 `href` 值 `data` 陣列，然後繼續下一步。

## 下載您的檔案資料

若要下載檔案資料，請向 `"href"` 您在上一步驟中複製的值 [擷取檔案](#retrieving-your-files).

>[!NOTE]
>
>如果您直接在命令列中提出此要求，系統可能會提示您在要求標題後新增輸出。 下列請求範例使用 `--output {FILENAME.FILETYPE}`.

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值來自 [上一步](#retrieve-the-next-api-call-with-your-batch-id). |
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
>提出GET要求之前，請確定您所在的目錄或資料夾正確無誤，檔案才會儲存至。

**回應**

回應會下載您在目前目錄中請求的檔案。 在此範例中，檔案名稱為「file.parquet」。

![終端](./images/download-scores/terminal-output.png)

下載的分數將採用Parquet格式，需要 [!DNL Spark]-shell或Parquet讀取器查看分數。 對於原始分數檢視，您可以使用 [阿帕奇鑲木工具](https://parquet.apache.org/docs/). 鑲木工具可使用 [!DNL Spark].

## 後續步驟

本檔案概述了下載Attribution AI分數所需的步驟。 如需分數輸出的詳細資訊，請造訪 [歸因AI輸入和輸出](./input-output.md) 檔案。

## 使用Snowflake存取分數

>[!IMPORTANT]
>
>如需使用Snowflake存取分數的詳細資訊，請連絡attributionai-support@adobe.com 。

您可以透過Snowflake存取匯總的Attribution AI分數。 目前，您需要透過attributionai-support@adobe.com傳送電子郵件給Adobe支援，以設定並接收您的讀者帳戶的認證，以進行Snowflake。

Adobe支援處理完您的請求後，系統會提供您一個URL，供讀者帳戶Snowflake，並提供下列對應憑證：

- SnowflakeURL
- 使用者名稱
- 密碼

>[!NOTE]
>
>讀取器帳戶用於使用支援JDBC連接器的sql客戶端、工作表和BI解決方案查詢資料。

取得認證和URL後，您就可以查詢模型表格，依接觸點日期或轉換日期匯總。

### 在Snowflake中尋找您的結構

使用提供的憑證登入Snowflake。 按一下 **工作表** 標籤，然後導覽至左側面板的資料庫目錄。

![工作表與導覽](./images/download-scores/edited_snowflake_1.png)

下一步，按一下 **選擇架構** 在畫面的右上角。 在顯示的彈出式視窗中，確認您已選取正確的資料庫。 下一步，按一下 *結構* 下拉式清單，然後選取您列出的其中一個結構。 您可以直接從所選架構下列出的分數表中查詢。

![查找架構](./images/download-scores/edited_snowflake_2.png)

## 將PowerBI連接到Snowflake（可選）

您的Snowflake憑證可用於設定PowerBI Desktop和Snowflake資料庫之間的連接。

首先，在 *伺服器* 框中，鍵入SnowflakeURL。 下一個，下 *倉庫*，輸入&quot;XSMALL&quot;。 然後，輸入您的使用者名稱和密碼。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立連線後，請選取您的Snowflake資料庫，然後選取適當的架構。 您現在可以載入所有表格。
