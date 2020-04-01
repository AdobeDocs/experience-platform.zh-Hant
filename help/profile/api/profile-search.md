---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# 描述檔搜尋

描述檔搜尋可用來搜尋並索引各種資料來源所包含的可設定欄位，並幾乎即時傳回這些欄位。

本指南提供相關資訊，以協助您進一步瞭解描述檔搜尋，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的API端點是即時客戶個人檔案API的一部分。 在繼續之前，請先閱讀「即 [時客戶基本資料開發人員指南」](getting-started.md)。

尤其是，「描述檔開 [發人員指南](getting-started.md) 」的「快速入門」區段包含相關主題的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

### 取得搜尋結果

該搜索端點可用於基於所需參數的值和附加的可選查詢參 `schema.name` 數獲得搜索結果。 可以使用多個參數，由&amp;符號分隔。

**API格式**

```http
GET /search?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
|---|---|
| `schema.name` | **必填.** 包含要搜索內容的架構類的名稱，以點標籤格式寫入。 目前僅支 `schema.name=_xdm.context.segmentdefinition` 援。 |
| `limit` | 要返回的搜索結果數。 預設值為 50。 |
| `page` | 用於為搜索的查詢結果編頁的頁碼。 |
| `s` | 符合Microsoft實作 [Lucene搜尋語法的查詢](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜尋詞，則會傳回與所有相關 `schema.name` 的記錄。 如需更詳細的說明，請參閱本文 [件的「搜尋參數](#search-parameters) 」一節。 |
| `namespace` | 標識要在參數中指定的方案類上搜索的實際 `schema.name` 資料。 |
| `organization.type` | 決定回應的內容。 傳回的內容格式取決於中使用的值 `schema.name`。 對 `_xdm.context.segmentdefinition`於，有效值 `hierarchy` 為或 `hierarchyinfo`。 |
| `organization.id` | **指定時`organization.type`為必要。** 在與層次結構一起使用時，提供指定組織的 `organization.type` 層次結構。 |

**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回符合搜尋准則的物件陣列。 在此範例中，由於參 `schema.name` 數為 `_xdm.context.segmentdefinition`參數，因此會傳回區段定義清單。

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### 建立布建請求

通過向端點發出POST請求，您可以建立置備請求以啟用對方案的配置檔案 `/search/provisioning/component/init` 搜索。

**請求**

>[!CAUTION]
>此POST請求不包含裝載，因此不需要「內容類型」標題。 此外，沒有沙盒標題，因為所有資料都會傳送至全域沙盒。

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**回應**

成功的回應會傳回HTTP狀態201（已建立）和下列訊息：

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### 處理配置請求

配置端點可用於為新的IMS組織設定正確的索引、索引器和資料源連接。 要處理配置請求，需要兩個屬性： `databaseName` 和 `containerName`。

`databaseName` 表示要配置的組織的Profile資料庫的名稱。

`containerName` 代表由資料連接器填入的容器名稱，此為設定期間讀取的內容。 POST請求中可 `containerName`以使用兩個值，一個或兩個值：
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### 建立設定要求

下列API呼叫根據請求裝載中提供的參數產生所需的資料來源、索引器和索引。

**API格式**

```http
POST /search/configure
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受）和明文訊息。

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### 刪除配置請求

下列API呼叫移除相符的索引項目，並根據請求裝載中提供的參數刪除索引器和資料來源。

>[!NOTE]
>索引本身不會刪除，因為它是共用資源。

**API格式**

```http
DELETE /search/configure
```

**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受）和明文訊息。

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## 後續步驟

閱讀本指南後，您現在更能瞭解即時客戶個人檔案搜尋的運作方式。 如需即時客戶個人檔案的詳細資訊，請閱讀即 [時客戶個人檔案總覽](../home.md)。 如需劃分的詳細資訊，請閱讀劃分 [概觀](../../segmentation/home.md)。

## 附錄 {#appendix}

### 搜尋參數 {#search-parameters}

下表列出使用搜尋API時搜尋參數的運作方式。

| 搜尋查詢 | 說明 |
|------------ | -----------|
| foo | 搜尋任何字詞。 如果在任何可搜尋的欄位中都找到&quot;foo&quot;，則會傳回結果。 |
| foo AND列 | 布爾式搜尋。 如果在任何可搜尋 **的欄位** 中都找到&quot;foo&quot;和&quot;bar&quot;兩字，就會傳回結果。 |
| foo OR列 | 布爾式搜尋。 如果在任何可搜 **尋的欄位中** ，找到&quot;foo&quot;或&quot;bar&quot;兩字，就會傳回結果。 |
| foo NOT欄 | 布爾式搜尋。 如果找到&quot;foo&quot;字詞，但在任何可搜尋欄位中找不到&quot;bar&quot;字詞，則會傳回結果。 |
| 名稱：foo AND列 | 布爾式搜尋。 如果在「名稱」欄 **位中** ，同時找到&quot;foo&quot;和&quot;bar&quot;兩個字，則會傳回結果。 |
| run* | 通配符搜索。 使用星號(*)符合0個或多個字元，這表示如果任何可搜尋欄位的內容包含以&quot;run&quot;開頭的字詞，則會傳回結果。 例如，如果出現&quot;runs&quot;、&quot;running&quot;、&quot;runner&quot;或&quot;runt&quot;等字詞，則會傳回結果。 |
| 小卡？ | 通配符搜索。 使用問號(?)只匹配一個字元，這表示如果任何可搜尋欄位的內容以「cam」和其他字母開頭，則會傳回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;字樣，則會傳回結果，但如果出現&quot;camera&quot;或&quot;campfire&quot;字樣，則不會傳回結果。 |
| &quot;藍傘&quot; | 片語搜尋。 如果任何可搜尋欄位的內容包含完整字句「blue burmal」，則會傳回結果。 |
| 藍色\~ | 模糊搜索。 或者，您可在波狀符號(~)後加上0-2的數字，以指定編輯距離。 例如，&quot;blue\~1&quot;會傳回&quot;blue&quot;、&quot;blues&quot;或&quot;glue&quot;。 模糊搜尋只 **能套用** 至詞語，不能套用至片語。 不過，您可以在片語中每個字詞的結尾附加波狀符號。 例如，&quot;camping\~ in\~ the\~ summer\~&quot;會與&quot;camping in the summer&quot;相符。 |
| &quot;酒店機場&quot;\~5 | 近距離搜尋。 此類搜尋用於尋找檔案中彼此接近的詞語。 例如，此片語 `"hotel airport"~5` 將在檔案中找到5個字內的&quot;hotel&quot;和&quot;airport&quot;。 |
| `/a[0-9]+b$/` | 規則運算式搜尋。 這種搜索類型根據正斜線&quot;/&quot;之間的內容查找匹配項，如RegExp類中所述。 例如，若要尋找包含&quot;motel&quot;或&quot;hotel&quot;的檔案，請指定 `/[mh]otel/`。 規則運算式搜尋會與單一字詞比對。 |

有關查詢語法的更詳細文檔，請閱讀 [Lucene查詢語法文檔](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。
