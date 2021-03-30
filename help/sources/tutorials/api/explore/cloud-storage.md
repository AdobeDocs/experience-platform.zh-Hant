---
keywords: Experience Platform；首頁；熱門主題；雲儲存；雲儲存
solution: Experience Platform
title: 使用Flow Service API探索Cloud儲存系統
topic: 概述
description: 本教學課程使用Flow Service API來探索協力廠商雲端儲存系統。
translation-type: tm+mt
source-git-commit: 457fc9e1b0c445233f0f574fefd31bc1fc3bafc8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API探索雲端儲存系統

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)來探索協力廠商雲端儲存系統。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連線至雲端儲存系統。

### 取得連線ID

若要使用[!DNL Platform] API來探索第三方雲端儲存空間，您必須擁有有效的連線ID。 如果您尚未連接要使用的儲存，則可以通過以下教程建立一個：

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 探索您的雲端儲存空間

使用雲端儲存空間的連線ID，您可以執行GET要求來探索檔案和目錄。 執行GET請求以探索雲端儲存空間時，您必須包含下表所列的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 您要探索的物件類型。 將此值設定為： <ul><li>`folder`:探索特定目錄</li><li>`root`:探索根目錄。</li></ul> |
| `object` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 |

使用以下調用可查找要導入[!DNL Platform]的檔案路徑：

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 雲端儲存空間來源連接器的連線ID。 |
| `{PATH}` | 目錄的路徑。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢目錄內找到的檔案和資料夾陣列。 請注意您要上傳之檔案的`path`屬性，因為您必須在下一步驟中提供它以檢查其結構。

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

若要從雲端儲存空間檢查資料檔案的結構，請執行GET要求，同時提供檔案的路徑和類型作為查詢參數。

您可以在提供檔案路徑和類型的同時，執行GET要求，從雲端儲存來源檢查資料檔案的結構。 您也可以透過指定檔案類型作為查詢參數的一部分，來檢查不同的檔案類型，例如CSV、TSV或壓縮的JSON和分隔檔案。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 雲端儲存空間來源連接器的連線ID。 |
| `{FILE_PATH}` | 要檢查的檔案的路徑。 |
| `{FILE_TYPE}` | 檔案的類型。 支援的檔案類型包括：<ul><li>分隔字元</code>:分隔字元分隔值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>:JavaScript物件符號。 JSON檔案必須符合XDM規範</li><li>PARCE</code>:阿帕奇鑲木地板。 拼花檔案必須與XDM相容。</li></ul> |
| `{QUERY_PARAMS}` | 可用於篩選結果的可選查詢參數。 如需詳細資訊，請參閱[查詢參數](#query)一節。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢檔案的結構，包括表名和資料類型。

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

## 使用查詢參數{#query}

[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)支援使用查詢參數來預覽和檢查不同的檔案類型。

| 參數 | 說明 |
| --------- | ----------- |
| `columnDelimiter` | 您指定為欄分隔字元的單一字元值，用來檢查CSV或TSV檔案。 如果未提供參數，則值預設為逗號`(,)`。 |
| `compressionType` | 預覽壓縮分隔字元或JSON檔案的必要查詢參數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## 後續步驟

通過本教程，您已探索了雲儲存系統，找到了要導入[!DNL Platform]的檔案的路徑，並查看了其結構。 您可以在下一個教學課程中使用這些資訊，從您的雲端儲存空間收集資料，並將其匯入Platform](../collect/cloud-storage.md)。[