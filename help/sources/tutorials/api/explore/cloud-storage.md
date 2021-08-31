---
keywords: Experience Platform；首頁；熱門主題；雲端儲存空間；雲端儲存空間
solution: Experience Platform
title: 使用流服務API探索Cloud儲存系統
topic-legacy: overview
description: 本教學課程使用流量服務API來探索協力廠商雲端儲存系統。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API探索雲儲存系統

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)來探索協力廠商雲端儲存系統。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功連接到雲儲存系統。

### 取得連線ID

若要使用[!DNL Platform] API探索第三方雲端儲存空間，您必須擁有有效的連線ID。 如果您尚未連接要使用的儲存，則可以通過以下教程建立連接：

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

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 探索雲端儲存空間

使用雲端儲存空間的連線ID，您可以執行GET請求來探索檔案和目錄。 執行GET請求以探索雲端儲存空間時，您必須包含下表所列的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 要瀏覽的對象類型。 將此值設定為： <ul><li>`folder`:探索特定目錄</li><li>`root`:瀏覽根目錄。</li></ul> |
| `object` | 只有在查看特定目錄時，才需要此參數。 其值表示要瀏覽的目錄的路徑。 |

使用以下調用查找要帶入[!DNL Platform]的檔案的路徑：

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 雲端儲存來源連接器的連線ID。 |
| `{PATH}` | 目錄的路徑。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回在查詢的目錄中找到的檔案和資料夾陣列。 記下您要上傳之檔案的`path`屬性，因為您必須在下一個步驟中提供該屬性以檢查其結構。

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
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 雲儲存源連接器的連接ID。 |
| `{FILE_PATH}` | 要檢查的檔案的路徑。 |
| `{FILE_TYPE}` | 檔案的類型。 支援的檔案類型包括：<ul><li>分隔字元</code>:分隔字元分隔值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>:JavaScript物件標籤法。 JSON檔案必須符合XDM</li><li>PARQUET</code>:阿帕奇拼花。 拼花檔案必須符合XDM標準。</li></ul> |
| `{QUERY_PARAMS}` | 可用於篩選結果的選用查詢參數。 如需詳細資訊，請參閱[查詢參數](#query)上的一節。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)支援使用查詢參數來預覽和檢查不同的檔案類型。

| 參數 | 說明 |
| --------- | ----------- |
| `columnDelimiter` | 您指定為欄分隔字元以檢查CSV或TSV檔案的單一字元值。 如果未提供參數，值預設為逗號`(,)`。 |
| `compressionType` | 預覽壓縮的分隔字元或JSON檔案所需的查詢參數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## 後續步驟

依照本教程，您已探索雲儲存系統，找到要帶入[!DNL Platform]的檔案路徑，並檢視其結構。 您可以在下一個教學課程中使用此資訊，以從您的雲端儲存空間收集資料，並將其匯入Platform](../collect/cloud-storage.md)。[
