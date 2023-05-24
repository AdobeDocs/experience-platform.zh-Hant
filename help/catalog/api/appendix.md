---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄api；附錄
solution: Experience Platform
title: 目錄服務API指南附錄
description: 本文檔包含其他資訊以幫助您使用Adobe Experience Platform的目錄API。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附錄

此文檔包含其他資訊，可幫助您使用 [!DNL Catalog] API。

## 查看相關對象 {#view-interrelated-objects}

部分 [!DNL Catalog] 對象可以與其他 [!DNL Catalog] 對象。 前置詞為的任何欄位 `@` 響應負載表示相關對象。 這些欄位的值採用URI的形式，可在單獨的GET請求中使用URI來檢索它們所表示的相關對象。

在文檔中返回的示例資料集 [查找特定資料集](look-up-object.md) 包含 `files` 具有以下URI值的欄位： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`。 的內容 `files` 使用此URI作為新GET請求的路徑可查看欄位。

**API格式**

```http
GET {OBJECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_URI}` | 由相關對象欄位提供的URI(不包括 `@` )的正平方根。 |

**要求**

以下請求使用URI提供示例資料集的 `files` 屬性，以檢索資料集的關聯檔案清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回相關對象的清單。 在此示例中，返回資料集檔案的清單。

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

## 在單個呼叫中發出多個請求

的根端點 [!DNL Catalog] API允許在單個調用中發出多個請求。 該請求負載包含表示通常是單個請求的對象的陣列，然後按順序執行。

如果這些請求是對 [!DNL Catalog] 任何更改都會失敗，所有更改都將恢復。

**API格式**

```http
POST /
```

**要求**

以下請求將建立新資料集，然後為該資料集建立相關視圖。 此示例演示了使用模板語言來訪問先前調用中返回的值，以便在後續調用中使用。

例如，如果要引用從上一個子請求返回的值，可以以下格式建立引用： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` ( `{REQUEST_ID}` 是用戶為子請求提供的ID，如下所示)。 您可以使用這些模板來引用先前子請求的響應對象正文中可用的任何屬性。

>[!NOTE]
>
>當執行的子請求僅返回對對象的引用(這是目錄API中大多數POST和PUT請求的預設值)時，此引用將別名為值 `id` 可用作  `<<{OBJECT_ID}.id>>`。

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
| `id` | 附加到響應對象的用戶提供的ID，以便您可以將請求與響應匹配。 [!DNL Catalog] 不儲存此值，而只是將其返回到響應中以供參考。 |
| `resource` | 相對於的根的資源路徑 [!DNL Catalog] API。 協定和域不應是此值的一部分，並且應在前面加上「/」。 <br/><br/> 將PATCH或DELETE用作子請求 `method`，將對象ID包括在資源路徑中。 不要與用戶提供的混淆 `id`，資源路徑使用的ID [!DNL Catalog] 對象本身(例如， `resource: "/dataSets/1234567890"`)。 |
| `method` | 與請求中發生的操作相關的方法(GET、PUT、POST、PATCH或DELETE)的名稱。 |
| `body` | 通常作為POST、PUT或PATCH請求中的負載傳遞的JSON文檔。 此屬性不是GET或DELETE請求所必需的。 |

**回應**

成功的響應返回包含 `id` 分配給每個請求的HTTP狀態代碼，以及響應 `body`。 由於三個示例請求都是為建立新對象， `body` 每個對象的陣列只包含新建立對象的ID，而POST響應最成功的標準陣列 [!DNL Catalog]。

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

檢查對多請求的響應時要小心，因為您需要驗證每個子請求的代碼，而不是僅依賴父POST請求的HTTP狀態代碼。  單個子請求可以返回404(例如對無效資源的GET請求)，而總請求返回200。

## 其他請求標頭

[!DNL Catalog] 提供了多種標題約定，以幫助您在更新期間保持資料的完整性。

### If-Match

最好使用對象版本控制來防止當多個用戶幾乎同時保存對象時發生的資料損壞類型。

更新對象時的最佳做法是首先進行API調用以查看(GET)要更新的對象。 包含在響應（以及響應包含單個對象的任何調用）中是 `E-Tag` 包含對象版本的標題。 將對象版本添加為名為的請求標題 `If-Match` 在更新(PUT或PATCH)調用中，只有在版本仍然相同的情況下才會成功更新，從而有助於防止資料衝突。

如果版本不匹配（自您檢索到該對象後，該對象被其他進程修改），您將收到HTTP狀態412（前提條件失敗），表示對目標資源的訪問被拒絕。

### Pragma

有時，您可能希望驗證對象而不保存資訊。 使用 `Pragma` 值為 `validate-only` 允許您僅為驗證目的發送POST或PUT請求，從而防止對資料的任何更改被保留。

## 資料壓縮

壓縮是 [!DNL Experience Platform] 將小檔案中的資料合併到大檔案中而不更改任何資料的服務。 出於效能原因，有時將一組小檔案合併到較大檔案中是有益的，以便在查詢時能夠更快地訪問資料。

當所攝取批中的檔案已壓縮時，其關聯 [!DNL Catalog] 對象已更新以用於監視目的。
