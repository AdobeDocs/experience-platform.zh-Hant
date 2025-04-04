---
keywords: Experience Platform；首頁；熱門主題；雲端儲存；雲端儲存
title: 使用流量服務API探索雲端儲存資料夾
description: 本教學課程使用流量服務API來探索協力廠商雲端儲存系統。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API探索您的雲端儲存資料夾

本教學課程提供如何使用[[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API來探索及預覽雲端儲存空間的結構與內容的步驟。

>[!NOTE]
>
>為了探索您的雲端儲存空間，您必須擁有雲端儲存空間來源的有效基本連線ID。 如果您沒有此ID，請參閱[來源概觀](../../../home.md#cloud-storage)，以取得您可以用來建立基礎連線的雲端儲存空間來源清單。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 探索您的雲端儲存資料夾

您可以在提供來源的基本連線ID時，對[!DNL Flow Service] API發出GET要求，以擷取有關雲端儲存資料夾結構的資訊。

執行GET請求以探索您的雲端儲存空間時，您必須包含下表所列的查詢引數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 您要探索的物件型別。 將此值設定為： <ul><li>`folder`：探索特定目錄</li><li>`root`：探索根目錄。</li></ul> |
| `object` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 |


**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您的雲端儲存空間來源的基本連線ID。 |
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

成功的回應會傳回在查詢的目錄中找到的檔案和資料夾陣列。 記下您要上傳之檔案的`path`屬性，因為您必須在下個步驟中提供該屬性，才能檢查其結構。

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

## 檢查檔案的結構

若要從雲端儲存空間檢查資料檔案的結構，請在提供檔案路徑及型別作為查詢引數的同時，執行GET要求。

您可以在提供檔案路徑和型別的同時，執行GET要求，從雲端儲存空間來源檢查資料檔案的結構。 您也可以檢查不同的檔案型別（例如CSV、TSV或壓縮的JSON）和分隔檔案，方法是將其檔案型別指定為查詢引數的一部分。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 您的雲端儲存空間來源聯結器的連線ID。 |
| `{FILE_PATH}` | 您要檢查的檔案路徑。 |
| `{FILE_TYPE}` | 檔案的型別。 支援的檔案型別包括：<ul><li><code>已分隔</code>：以分隔符號分隔的值。 DSV檔案必須以逗號分隔。</li><li><code>JSON</code>：JavaScript物件標籤法。 JSON檔案必須符合XDM標準</li><li><code>PARQUET</code>：Apache Parquet。 Parquet檔案必須符合XDM標準。</li></ul> |
| `{QUERY_PARAMS}` | 可用來篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](#query)的相關章節。 |

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

成功的回應會傳回查詢檔案的結構，包括表格名稱和資料型別。

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

## 使用查詢引數 {#query}

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)支援使用查詢引數來預覽和檢查不同的檔案型別。

| 參數 | 說明 |
| --------- | ----------- |
| `columnDelimiter` | 您指定為欄分隔字元的單一字元值，以檢查CSV或TSV檔案。 如果未提供引數，則值預設為逗號`(,)`。 |
| `compressionType` | 預覽壓縮的分隔檔案或JSON檔案所需的查詢引數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 定義呈現預覽時要使用的編碼型別。 支援的編碼型別為： `UTF-8`和`ISO-8859-1`。 **注意**： `encoding`引數僅在擷取分隔的CSV檔案時可用。 將使用預設編碼`UTF-8`擷取其他檔案型別。 |

## 後續步驟

依照本教學課程，您已探索您的雲端儲存系統、找到您要帶入[!DNL Experience Platform]的檔案路徑，並檢視其結構。 您可以在下個教學課程中使用此資訊，從您的雲端儲存空間[收集資料，並將其帶入Experience Platform](../collect/cloud-storage.md)。
