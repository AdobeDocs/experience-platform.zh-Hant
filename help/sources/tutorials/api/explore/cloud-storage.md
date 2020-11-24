---
keywords: Experience Platform;home;popular topics;cloud storage;Cloud storage
solution: Experience Platform
title: 使用Flow Service API探索雲端儲存系統
topic: overview
description: 本教學課程使用Flow Service API來探索協力廠商雲端儲存系統。
translation-type: tm+mt
source-git-commit: 026007e5f80217f66795b2b53001b6cf5e6d2344
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 2%

---


# 使用 [!DNL Flow Service] API探索雲端儲存系統

本教學課程使 [[!DNL Flow Service] 用API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 來探索協力廠商雲端儲存系統。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API成功連線至雲端儲存系統。

### 取得連線ID

若要使用API來探索第三方雲端儲存 [!DNL Platform] 空間，您必須擁有有效的連線ID。 如果您尚未連接要使用的儲存，則可以通過以下教程建立一個：

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Azure檔案儲存](../create/cloud-storage/azure-file-storage.md)
* [Google雲端商店](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [SFTP](../create/cloud-storage/sftp.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 探索您的雲端儲存空間

使用雲端儲存空間的連線ID，您可以執行GET請求來探索檔案和目錄。 當執行GET請求以探索您的雲端儲存空間時，您必須包含下表所列的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `objectType` | 您要探索的物件類型。 將此值設定為： <ul><li>`folder`:探索特定目錄</li><li>`root`:探索根目錄。</li></ul> |
| `object` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 |

使用下列呼叫來尋找您要放入的檔案路徑 [!DNL Platform]:

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

成功的響應返回查詢目錄內找到的檔案和資料夾陣列。 請注意您要 `path` 上傳的檔案屬性，因為您必須在下個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## 檢查檔案結構

若要從雲端儲存空間檢查資料檔案的結構，請執行GET要求，同時提供檔案的路徑和類型作為查詢參數。

您可以指定自訂分隔字元作為查詢周長，以檢查CSV或TSV檔案的結構。 任何單一字元值都是允許的欄分隔字元。 如果未提供，則使 `(,)` 用逗號作為預設值。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 雲端儲存空間來源連接器的連線ID。 |
| `{FILE_PATH}` | 要檢查的檔案的路徑。 |
| `{FILE_TYPE}` | 檔案的類型。 支援的檔案類型包括：<ul><li>分隔字元</code>:分隔字元分隔值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>:JavaScript物件符號。 JSON檔案必須符合XDM規範</li><li>PARCE</code>:阿帕奇鑲木地板。 拼花檔案必須與XDM相容。</li></ul> |
| `columnDelimiter` | 您指定為欄分隔字元的單一字元值，用來檢查CSV或TSV檔案。 如果未提供參數，則值預設為逗號 `(,)`。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

## 後續步驟

通過本教程，您已探索了雲儲存系統，找到了要導入的檔案的路徑，並查看了 [!DNL Platform]其結構。 您可以在下一個教學課程中使用此資 [訊，從雲端儲存空間收集資料並匯入平台](../collect/cloud-storage.md)。