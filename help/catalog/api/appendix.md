---
keywords: Experience Platform;home；熱門主題；目錄服務；目錄api；附錄
solution: Experience Platform
title: 目錄服務API指南附錄
topic-legacy: developer guide
description: 本檔案包含其他資訊，可協助您使用Adobe Experience Platform的Catalog API。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附錄

本檔案包含協助您使用[!DNL Catalog] API的其他資訊。

## 查看相關對象{#view-interrelated-objects}

某些[!DNL Catalog]對象可以與其他[!DNL Catalog]對象相關聯。 在響應負載中以`@`為前置詞的任何欄位都表示相關對象。 這些欄位的值採用URI的形式，可用於個別的GET請求，以擷取其所代表的相關物件。

在[查找特定資料集](look-up-object.md)的文檔中返回的示例資料集包含具有以下URI值的`files`欄位：`"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`。 使用此URI作為新GET請求的路徑，可以查看`files`欄位的內容。

**API格式**

```http
GET {OBJECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_URI}` | 由相關對象欄位（不包括`@`符號）提供的URI。 |

**要求**

下列請求使用範例資料集的`files`屬性提供的URI來擷取資料集相關聯檔案的清單。

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

[!DNL Catalog] API的根端點允許在單次呼叫中發出多個請求。 請求裝載包含代表通常是個別請求的物件陣列，然後依序執行。

如果這些請求是對[!DNL Catalog]的修改或添加，而且任何更改都失敗，則所有更改都將恢復。

**API格式**

```http
POST /
```

**要求**

下列請求會建立新資料集，然後建立該資料集的相關檢視。 此範例示範如何使用範本語言來存取先前呼叫中傳回的值，以便用於後續呼叫。

例如，如果您想要參考從先前的子請求傳回的值，則可以建立以下格式的參考：`<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>`（其中`{REQUEST_ID}`是使用者提供的子請求ID，如下所示）。 您可以使用這些範本，來參考先前子請求回應物件內文中可用的任何屬性。

>[!NOTE]
>
>當執行的子請求僅返回對對象的引用(在目錄API中，對於大多數POST和PUT請求，此為預設值)時，此引用將別名化為值`id`，並可用作`<<{OBJECT_ID}.id>>`。

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
| `id` | 附加至回應物件的使用者提供ID，以便您將要求與回應相符。 [!DNL Catalog] 不會儲存此值，只會在回應中傳回該值，以供參考。 |
| `resource` | 相對於[!DNL Catalog] API根的資源路徑。 協定和域不應是此值的一部分，並且應加上前置詞&quot;/&quot;。 <br/><br/> 當使用PATCH或DELETE作為子請求時， `method`請在資源路徑中包括對象ID。不要與用戶提供的`id`混淆，資源路徑使用[!DNL Catalog]對象本身的ID（例如`resource: "/dataSets/1234567890"`）。 |
| `method` | 與請求中所發生動作相關的方法(GET、PUT、POST、PATCH或DELETE)名稱。 |
| `body` | 通常會在POST、PUT或PATCH請求中作為裝載傳遞的JSON檔案。 此屬性不是GET或DELETE請求的必需屬性。 |

**回應**

成功的響應返回一組對象，這些對象包含您分配給每個請求的`id`、單個請求的HTTP狀態代碼和響應`body`。 由於三個示例請求都是為了建立新對象，因此每個對象的`body`都是一個僅包含新建立對象ID的陣列，而[!DNL Catalog]中最成功POST響應的標準陣列也是如此。

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

檢查多重請求的回應時請務必小心，因為您需要驗證每個個別子請求的程式碼，而不要只依賴父POST請求的HTTP狀態程式碼。  單個子請求可以傳回404(例如對無效資源的GET請求)，而整體請求傳回200。

## 其他請求標題

[!DNL Catalog] 提供數種標題慣例，以協助您在更新期間維持資料的完整性。

### If-Match

最好使用物件版本控制來防止多個使用者同時儲存物件時發生的資料損毀類型。

更新物件時的最佳實務是先進行API呼叫，以檢視(GET)要更新的物件。 包含在回應中（以及任何回應包含單一物件的呼叫）是包含物件版本的`E-Tag`標題。 在更新(PUT或PATCH)呼叫中將物件版本新增為名為`If-Match`的請求標題，只有在版本不變時，才會成功進行更新，有助於避免資料衝突。

如果版本不匹配（自您檢索到該對象後，該對象被其他進程修改），則您將收到HTTP狀態412（先決條件失敗），表示對目標資源的訪問被拒絕。

### Pragma

有時，您可能希望驗證對象而不保存資訊。 使用`Pragma`標題（其值為`validate-only`）可讓您僅傳送POST或PUT請求以進行驗證，避免對資料進行任何變更。

## 資料壓縮

壓縮是一種[!DNL Experience Platform]服務，可將小檔案的資料合併為大檔案，而不會變更任何資料。 出於效能原因，有時將一組小檔案合併為較大的檔案，以便在查詢時提供更快速的資料存取。

當收錄批次中的檔案已壓縮時，會更新其相關的[!DNL Catalog]物件，以利監控。
