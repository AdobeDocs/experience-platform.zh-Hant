---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目錄服務開發人員指南附錄
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# 目錄服務開發人員指南附錄

本檔案包含協助您使用目錄API的其他資訊。

## 查看相關對象 {#view-interrelated-objects}

某些目錄對象可以與其他目錄對象相互關聯。 任何在響應負載中前置詞的 `@` 欄位都表示相關對象。 這些欄位的值採用URI的形式，可用於個別的GET請求，以擷取其所代表的相關物件。

查找特定資料集時在文檔中 [返回的示例資料集包含](look-up-object.md)`files` 具有以下URI值的欄位： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 使用此URI `files` 作為新GET請求的路徑，即可檢視欄位內容。

**API格式**

```http
GET {OBJECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_URI}` | 由相關對象欄位（不包括符號）提供 `@` 的URI。 |

**請求**

以下請求使用URI(提供範例資料集的屬 `files` 性)來擷取資料集相關聯檔案的清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回相關對象的清單。 在此範例中，會傳回資料集檔案的清單。

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 在單一呼叫中提出多個請求

目錄API的根端點允許在單次呼叫中發出多個請求。 請求裝載包含代表通常是個別請求的物件陣列，然後依序執行。

如果這些請求是目錄的修改或添加，且任何更改都失敗，則所有更改都將恢復。

**API格式**

```http
POST /
```

**請求**

下列請求會建立新資料集，然後建立該資料集的相關檢視。 此範例示範如何使用範本語言來存取先前呼叫中傳回的值，以便用於後續呼叫。

例如，如果您想要參考從先前的子請求傳回的值，則可以建立以下格式的參考： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其 `{REQUEST_ID}` 中是使用者提供的子請求ID，如下所示)。 您可以使用這些範本，來參考先前子請求回應物件內文中可用的任何屬性。

>[!NOTE]
>
>當執行的子請求只傳回物件的參考（在目錄API中，大部分POST和PUT請求的預設值）時，此參考會設為值 `id` 別名，可當做 `<<{OBJECT_ID}.id>>`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 附加至回應物件的使用者提供ID，以便您將要求與回應相符。 目錄不會儲存此值，只會在回應中傳回該值，以供參考。 |
| `resource` | 目錄API根目錄的資源路徑。 協定和域不應是此值的一部分，並且應加上前置詞&quot;/&quot;。 <br/><br/> 使用PATCH或DELETE作為子請求時， `method`請在資源路徑中包含對象ID。 不要與用戶提供的路徑混淆 `id`，資源路徑使用目錄對象本身的ID(例如 `resource: "/dataSets/1234567890"`)。 |
| `method` | 與請求中發生的動作相關的方法名稱（GET、PUT、POST、PATCH或DELETE）。 |
| `body` | 通常會在POST、PUT或PATCH請求中作為裝載傳遞的JSON檔案。 GET或DELETE請求不需要此屬性。 |

**回應**

成功的回應會傳回一組物件，其中包 `id` 含您指派給每個請求的物件、個別請求的HTTP狀態碼，以及回應 `body`。 由於這三個範例請求都是為了建立新物件，因此每個物件的陣列都只包含新建立物件的ID，而Catalog中最成功的POST回應也是標準。 `body`

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

檢查多重請求的回應時請務必小心，因為您需要驗證每個個別子請求的程式碼，而不要只依賴父POST請求的HTTP狀態程式碼。  單一子請求可能會傳回404（例如無效資源上的GET請求），而整體請求則會傳回200。

## 其他請求標題

目錄提供數種標題慣例，可協助您在更新期間維持資料的完整性。

### If-Match

最好使用物件版本控制來防止多個使用者同時儲存物件時發生的資料損毀類型。

更新物件時的最佳實務是先進行API呼叫以檢視(GET)要更新的物件。 包含在回應中（以及任何回應包含單一物件的呼叫）是包含 `E-Tag` 物件版本的標題。 將物件版本新增為更新(PUT或 `If-Match` PATCH)呼叫中命名的請求標題，只有在版本不變時，才會成功進行更新，有助於避免資料衝突。

如果版本不匹配（自您檢索到該對象後，該對象被其他進程修改），則您將收到HTTP狀態412（先決條件失敗），表示對目標資源的訪問被拒絕。

### Pragma

有時，您可能希望驗證對象而不保存資訊。 使用 `Pragma` 具有值的標題 `validate-only` 可讓您僅傳送POST或PUT要求以進行驗證，避免資料的任何變更持續存在。

## 資料壓縮

Compaction是Experience Platform服務，可將小檔案的資料合併為大檔案，而不會變更任何資料。 基於效能的考慮，將一組小型檔案合併為較大的檔案有時很有幫助，以便在查詢資料時能更快速地存取資料。

當收錄批次中的檔案已壓縮時，會更新其關聯的目錄物件，以利監控。