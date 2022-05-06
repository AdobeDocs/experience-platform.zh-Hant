---
keywords: Experience Platform；首頁；熱門主題；雲儲存；雲儲存
title: 使用流服務API瀏覽雲儲存資料夾
description: 本教程使用流服務API來瀏覽第三方雲儲存系統。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程提供了有關如何使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
>為了瀏覽雲儲存，您必須已擁有雲儲存源的有效基本連接ID。 如果您沒有此ID，請查看 [源概述](../../../home.md#cloud-storage) 的子目錄。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../landing/api-guide.md)。

## 瀏覽雲儲存資料夾

您可以通過向以下站點發出GET請求來檢索有關雲儲存資料夾結構的資訊 [!DNL Flow Service] API，同時提供源的基本連接ID。

執行GET請求以瀏覽雲儲存時，必須包括下表中列出的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 要瀏覽的對象的類型。 將此值設定為： <ul><li>`folder`:瀏覽特定目錄</li><li>`root`:瀏覽根目錄。</li></ul> |
| `object` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 |


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

成功的響應返回查詢目錄中找到的檔案和資料夾陣列。 注意 `path` 要上載的檔案的屬性，因為需要在下一步中提供該屬性以檢查其結構。

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

要從雲儲存中檢查資料檔案的結構，請在提供檔案路徑和類型作為查詢參數的同時執行GET請求。

您可以在提供檔案路徑和類型的同時執行GET請求，從雲儲存源檢查資料檔案的結構。 您還可以通過指定不同檔案類型作為查詢參數的一部分來檢查不同的檔案類型，如CSV、TSV或壓縮的JSON和分隔檔案。

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
| `{FILE_TYPE}` | 檔案的類型。 支援的檔案類型包括：<ul><li>分隔</code>:分隔符分隔的值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>:JavaScript對象表示法。 JSON檔案必須符合XDM</li><li>鑲木</code>:阿帕奇鑲木地板。 拼花檔案必須符合XDM。</li></ul> |
| `{QUERY_PARAMS}` | 可用於篩選結果的可選查詢參數。 請參閱 [查詢參數](#query) 的子菜單。 |

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

成功的響應將返回查詢檔案的結構，包括表名和資料類型。

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

的 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 支援使用查詢參數來預覽和檢查不同的檔案類型。

| 參數 | 說明 |
| --------- | ----------- |
| `columnDelimiter` | 指定為列分隔符以檢查CSV或TSV檔案的單個字元值。 如果未提供參數，則值預設為逗號 `(,)`。 |
| `compressionType` | 預覽壓縮分隔檔案或JSON檔案所需的查詢參數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 定義呈現預覽時要使用的編碼類型。 支援的編碼類型有： `UTF-8` 和 `ISO-8859-1`。 **注釋**:的 `encoding` 參數僅在插入分隔的CSV檔案時可用。 其他檔案類型將採用預設編碼， `UTF-8`。 |

## 後續步驟

按照本教程，您已探索了雲儲存系統，找到了要導入的檔案的路徑 [!DNL Platform]，並查看其結構。 您可以在下一教程中使用此資訊 [從雲儲存中收集資料並將其引入平台](../collect/cloud-storage.md)。
