---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄api；附錄
solution: Experience Platform
title: 目錄服務API指南附錄
description: 本檔案包含其他資訊，可協助您使用Adobe Experience Platform中的目錄API。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附錄

本檔案包含其他資訊，可協助您使用 [!DNL Catalog] API。

## 查看相關對象 {#view-interrelated-objects}

部分 [!DNL Catalog] 對象可以與其他對象相關聯 [!DNL Catalog] 對象。 前置詞為的任何欄位 `@` 響應有效載荷表示相關對象。 這些欄位的值採用URI的形式，URI可用於單獨的GET請求，以檢索它們表示的相關對象。

檔案中傳回的範例資料集 [查詢特定資料集](look-up-object.md) 包含a `files` 欄位，其中包含以下URI值： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 內容 `files` 使用此URI作為新GET請求的路徑可以查看欄位。

**API格式**

```http
GET {OBJECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_URI}` | 由相關對象欄位提供的URI(不包括 `@` 符號)。 |

**要求**

以下請求使用範例資料集的 `files` 屬性來擷取資料集的關聯檔案清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回相關物件的清單。 在此範例中，會傳回資料集檔案清單。

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

的根端點 [!DNL Catalog] API可在單一呼叫中提出多個要求。 要求裝載包含代表一般為個別要求的物件陣列，接著會依序執行。

若這些請求是 [!DNL Catalog] 而且任何一項更改都會失敗，所有更改都將恢復。

**API格式**

```http
POST /
```

**要求**

下列請求會建立新資料集，然後為該資料集建立相關檢視。 此範例示範如何使用範本語言來存取先前呼叫中傳回的值，以便用於後續呼叫。

例如，如果您想要參考從先前子請求傳回的值，可以以下格式建立參考： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其中 `{REQUEST_ID}` 是使用者提供的子請求ID，如下所示)。 您可以使用這些範本，來參考先前子請求回應物件內文中可用的任何屬性。

>[!NOTE]
>
>當執行的子請求只傳回對象的參考時(目錄API中大部分POST和PUT請求的預設值亦同)，此參考會將別名傳送至值 `id` 可作為  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `id` | 附加至回應物件的使用者提供ID，以便您能比對回應的要求。 [!DNL Catalog] 不會儲存此值，而只是將其傳回回應中以供參考。 |
| `resource` | 相對於的根的資源路徑 [!DNL Catalog] API。 通訊協定和網域不應屬於此值，且應加上前置詞「/」。 <br/><br/> 使用PATCH或DELETE作為子請求時 `method`，在資源路徑中包含物件ID。 不要與用戶提供的混淆 `id`，資源路徑會使用 [!DNL Catalog] 物件本身(例如， `resource: "/dataSets/1234567890"`)。 |
| `method` | 與請求中發生的動作相關的方法名稱(GET、PUT、POST、PATCH或DELETE)。 |
| `body` | 通常會在POST、PUT或PATCH要求中作為裝載傳遞的JSON檔案。 GET或DELETE請求不需要此屬性。 |

**回應**

成功的回應會傳回包含 `id` 指派給每個請求的HTTP狀態代碼，以及回應 `body`. 由於三個範例要求都是要建立新物件，因此 `body` 每個物件的陣列僅包含新建立物件的ID，如中最成功POST回應的標準 [!DNL Catalog].

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

檢查多個請求的回應時請務必小心，因為您需要驗證每個個別子請求的程式碼，而非僅依賴上層POST請求的HTTP狀態程式碼。  單個子請求可以返回404(例如無效資源上的GET請求)，而整體請求返回200。

## 其他請求標題

[!DNL Catalog] 提供數個標題慣例，協助您在更新期間維護資料的完整性。

### If-Match

最好使用對象版本設定來防止當多個用戶幾乎同時保存對象時發生的資料損壞類型。

更新物件時的最佳實務是先進行API呼叫以檢視(GET)要更新的物件。 包含在回應中（以及回應包含單一物件的任何呼叫）是 `E-Tag` 包含對象版本的標題。 將物件版本新增為請求標題，命名為 `If-Match` 在您的更新(PUT或PATCH)呼叫中，只有在版本仍相同時，更新才會成功，有助於防止資料衝突。

如果版本不匹配（自您檢索到該對象後，其他進程已修改該對象），您將收到HTTP狀態412（先決條件失敗），指示已拒絕對目標資源的訪問。

### Pragma

有時，您可能希望驗證對象而不保存資訊。 使用 `Pragma` 標題，值為 `validate-only` 可讓您僅針對驗證目的傳送POST或PUT要求，防止資料的任何變更持續存在。

## 資料壓縮

壓縮是 [!DNL Experience Platform] 將小檔案中的資料合併為大檔案而不變更任何資料的服務。 基於效能原因，有時將一組小檔案組合成較大的檔案，以便在查詢時提供對資料的更快速的訪問是有益的。

壓縮所擷取批次中的檔案時，會與 [!DNL Catalog] 物件已更新，以供監控之用。
