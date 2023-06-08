---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄api；附錄
solution: Experience Platform
title: 目錄服務API指南附錄
description: 本檔案包含協助您在Adobe Experience Platform中使用目錄API的其他資訊。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附錄

本檔案包含可協助您使用的其他資訊 [!DNL Catalog] API。

## 檢視相互關聯的物件 {#view-interrelated-objects}

部分 [!DNL Catalog] 物件可以與其他物件相互關聯 [!DNL Catalog] 物件。 前置詞為的任何欄位 `@` 回應中裝載表示相關物件。 這些欄位的值採用URI的形式，可用於單獨的GET請求中，以檢索它們表示的相關物件。

檔案傳回的範例資料集，於 [查詢特定資料集](look-up-object.md) 包含 `files` 具有下列URI值的欄位： `"@/datasetFiles?datasetId={DATASET_ID}"`. 的內容 `files` 欄位可透過使用此URI作為新GET請求的路徑來檢視。

**API格式**

```http
GET {OBJECT_URI}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_URI}` | 相互關聯的物件欄位提供的URI (不包括 `@` 符號)。 |

**要求**

以下請求會使用範例資料集的URI `files` 屬性，可擷取資料集關聯檔案的清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
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

## 其他請求標頭

[!DNL Catalog] 提供數個標題慣例，協助您在更新期間維持資料的完整性。

### If-Match

使用物件版本設定是很好的做法，以防止當多個使用者幾乎同時儲存物件時發生的資料損毀型別。

更新物件時的最佳實務是先進行API呼叫以檢視(GET)要更新的物件。 包含在回應中（以及任何回應包含單一物件的呼叫）是 `E-Tag` 包含物件版本的標頭。 將物件版本新增為名為的請求標頭 `If-Match` 只有在版本仍相同的情況下，更新(PUT或PATCH)呼叫才會導致更新成功，有助於防止資料衝突。

如果版本不符（物件在您擷取之後被其他處理序修改），您將會收到HTTP狀態412 （先決條件失敗），表示存取目標資源已被拒絕。

### Pragma

有時您可能會想要驗證物件而不儲存資訊。 使用 `Pragma` 值為的標頭 `validate-only` 可讓您傳送POST或PUT請求，但僅供驗證之用，以防止保留對資料的任何變更。

## 資料壓縮

壓縮是 [!DNL Experience Platform] 此服務可將小型檔案中的資料合併至大型檔案，而不需變更任何資料。 基於效能考量，將一組小型檔案合併成大型檔案有時會有好處，這樣就能在查詢時更快速地存取資料。

當已壓縮所擷取批次中的檔案時，其相關聯的 [!DNL Catalog] 物件會更新以供監控之用。
