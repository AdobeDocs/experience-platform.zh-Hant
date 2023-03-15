---
keywords: Experience Platform；首頁；熱門主題；雲端儲存空間；雲端儲存空間
title: 使用流服務API探索雲儲存資料夾
description: 本教學課程使用流量服務API來探索協力廠商雲端儲存系統。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教學課程提供如何探索及預覽雲端儲存空間的結構和內容的步驟，使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
>若要探索雲端儲存空間，您必須擁有雲端儲存空間來源的有效基本連線ID。 如果您沒有此ID，請參閱 [來源概觀](../../../home.md#cloud-storage) 以取得可建立基本連線的雲儲存來源清單。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).

## 探索您的雲儲存資料夾

您可以向提出GET要求，以擷取雲端儲存資料夾結構的相關資訊 [!DNL Flow Service] API，同時提供來源的基本連線ID。

執行GET請求以探索雲端儲存空間時，您必須包含下表所列的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 要瀏覽的對象類型。 將此值設定為： <ul><li>`folder`:探索特定目錄</li><li>`root`:瀏覽根目錄。</li></ul> |
| `object` | 只有在查看特定目錄時，才需要此參數。 其值表示要瀏覽的目錄的路徑。 |


**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 雲儲存源的基本連接ID。 |
| `{PATH}` | 目錄的路徑。 |

**要求**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回在查詢的目錄中找到的檔案和資料夾陣列。 請注意 `path` 屬性，因為您必須在下一個步驟中提供該屬性以檢查其結構。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect檔案結構

若要從雲端儲存體檢查資料檔案的結構，請執行GET要求，同時提供檔案的路徑和類型作為查詢參數。

您可以在提供檔案路徑和類型的同時，執行GET請求，以檢查雲端儲存來源中的資料檔案結構。 您也可以在查詢參數中指定不同的檔案類型，以檢查不同的檔案類型，例如CSV、TSV或壓縮的JSON和分隔檔案。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 雲儲存源連接器的連接ID。 |
| `{FILE_PATH}` | 要檢查的檔案的路徑。 |
| `{FILE_TYPE}` | 檔案的類型。 支援的檔案類型包括：<ul><li>分隔</code>:分隔字元分隔值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>:JavaScript物件標籤法。 JSON檔案必須符合XDM</li><li>鑲木</code>:阿帕奇拼花。 拼花檔案必須符合XDM標準。</li></ul> |
| `{QUERY_PARAMS}` | 可用於篩選結果的選用查詢參數。 請參閱 [查詢參數](#query) 以取得更多資訊。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢的檔案的結構，包括表名和資料類型。

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## 使用查詢參數 {#query}

此 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 支援使用查詢參數來預覽和檢查不同的檔案類型。

| 參數 | 說明 |
| --------- | ----------- |
| `columnDelimiter` | 您指定為欄分隔字元以檢查CSV或TSV檔案的單一字元值。 如果未提供參數，值會預設為逗號 `(,)`. |
| `compressionType` | 預覽壓縮的分隔字元或JSON檔案所需的查詢參數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 定義呈現預覽時要使用的編碼類型。 支援的編碼類型為： `UTF-8` 和 `ISO-8859-1`. **附註**:此 `encoding` 只有擷取分隔的CSV檔案時，才可使用參數。 其他檔案類型將會以預設編碼擷取， `UTF-8`. |

## 後續步驟

依照本教學課程，您已探索雲端儲存系統，並找到您要帶入的檔案路徑 [!DNL Platform]，並檢視其結構。 您可以在下一個教學課程中使用此資訊，以 [從雲端儲存空間收集資料並匯入Platform](../collect/cloud-storage.md).
