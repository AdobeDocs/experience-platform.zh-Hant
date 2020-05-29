---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;
solution: Adobe Experience Platform
title: 區段API開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: f489e9f9dfc9c7e94f76a6825e7ca24c41ee8a66
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 2%

---


# 區段搜尋

「區段搜尋」可用來搜尋並索引各種資料來源所包含的可設定欄位，並近乎即時地傳回這些欄位。

本指南提供相關資訊，以協助您進一步瞭解區段搜尋，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的API端點是區段API的一部分。 在繼續之前，請先閱讀區 [段開發人員指南](getting-started.md)。

尤其是，區 [段開發人員指南的](getting-started.md) 「快速入門」區段包含相關主題的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫Experience Platform API所需之必要標題的重要資訊。

除了快速入門區段中概述的必要標題外，對「區段搜尋API」的所有請求都需要下列額外標題：

- x-ups-search-version: &quot;1.0&quot;

### 跨多個名稱空間搜尋

此搜索端點可用於跨各種名稱空間搜索，返回搜索計數結果清單。 可以使用多個參數，由&amp;符號分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** ，其中{SCHEMA}表示與搜索對象關聯的方案類值。 目前僅支 `_xdm.context.segmentdefinition` 援。 |
| `s={SEARCH_TERM}` | *（可選）* ，其中{SEARCH_TERM}代表符合Microsoft實作的 [Lucene搜尋語法的查詢](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜尋詞，則會傳回與所有相關 `schema.name` 的記錄。 本檔案附錄提供更詳細 [的說](#appendix) 明。 |

**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功的回應會傳回HTTP狀態200，並提供下列資訊。

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### 搜尋個別實體

此搜索端點可用於檢索指定命名空間內所有全文索引對象的清單。 可以使用多個參數，由&amp;符號分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** ，其中{SCHEMA}包含與搜索對象關聯的方案類值。 目前僅支 `_xdm.context.segmentdefinition` 援。 |
| `namespace={NAMESPACE}` | **（必要）** ，其中{NAMESPACE}包含您要在其中搜尋的命名空間。 |
| `s={SEARCH_TERM}` | *（可選）* {SEARCH_TERM}包含符合Microsoft實作 [Lucene搜尋語法的查詢](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜尋詞，則會傳回與所有相關 `schema.name` 的記錄。 本檔案附錄提供更詳細 [的說](#appendix) 明。 |
| `entityId={ENTITY_ID}` | *（選用）* ，將搜尋限制在指定的資料夾內，以{ENTITY_ID}指定。 |
| `limit={LIMIT}` | *（可選）* ，其中{LIMIT}代表要傳回的搜尋結果數。 預設值為 50。 |
| `page={PAGE}` | *（可選）* ，其中{PAGE}代表用於為所搜尋查詢結果編頁的頁碼。 請注意，頁碼是從 **0開始**。 |


**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功的回應會傳回HTTP狀態200，其結果符合搜尋查詢。

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### 取得搜尋物件的結構資訊

該搜索端點可用於獲取有關所請求搜索對象的結構資訊。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** ，其中{SCHEMA}包含與搜索對象關聯的方案類值。 目前僅支 `_xdm.context.segmentdefinition` 援。 |
| `namespace={NAMESPACE}` | **（必要）** ，其中{NAMESPACE}包含您要在其中搜尋的命名空間。 |
| `entityId={ENTITY_ID}` | **（必要）** ，您要取得相關結構資訊的搜尋物件ID，使用{ENTITY_ID}指定。 |

**請求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含所請求搜尋物件的詳細結構資訊。

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## 後續步驟

閱讀本指南後，您現在可以更深入瞭解「區段搜尋」的運作方式。 如需劃分的詳細資訊，請閱讀劃分 [概觀](../home.md)。

## 附錄 {#appendix}

以下各節提供搜尋詞如何運作的其他資訊。 搜索查詢的編寫方式如下： `s={FieldName}:{SearchExpression}`. 因此，例如，若要搜尋名為AAM或平台的區段，您應使用下列搜尋查詢： `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 為獲得最佳實務，搜尋運算式應採用HTML編碼，如上例所示。

### 搜尋欄位 {#search-fields}

下表列出了可在搜索查詢參數中搜索的欄位。

| 欄位名稱 | 說明 |
| ---------- | ----------- |
| folderId | 具有指定搜索的資料夾ID的資料夾或資料夾。 |
| folderLocation | 具有指定搜索的資料夾位置的位置。 |
| parentFolderId | 具有指定搜尋之父資料夾ID的區段或資料夾。 |
| segmentId | 區段符合您指定搜尋的區段ID。 |
| segmentName | 區段會符合您指定搜尋的區段名稱。 |
| segmentDescription | 區段會符合您指定搜尋的區段說明。 |

### 搜尋運算式 {#search-expression}

下表列出使用區段搜尋API時搜尋查詢的運作方式。

>!![NOTE] 以下範例以非HTML編碼格式顯示，以提高清晰度。 為獲得最佳實務，HTML會為您的搜尋運算式編碼。

| 範例搜尋運算式 | 說明 |
| ------------------------- | ----------- |
| foo | 搜尋任何字詞。 如果在任何可搜尋的欄位中都找到&quot;foo&quot;，則會傳回結果。 |
| foo AND列 | 布爾式搜尋。 如果在任何可搜尋 **的欄位** 中都找到&quot;foo&quot;和&quot;bar&quot;兩字，就會傳回結果。 |
| foo OR列 | 布爾式搜尋。 如果在任何可搜 **尋的欄位中** ，找到&quot;foo&quot;或&quot;bar&quot;兩字，就會傳回結果。 |
| foo NOT欄 | 布爾式搜尋。 如果找到&quot;foo&quot;字詞，但在任何可搜尋欄位中找不到&quot;bar&quot;字詞，則會傳回結果。 |
| 名稱： foo AND列 | 布爾式搜尋。 如果在「名稱」欄 **位中** ，同時找到&quot;foo&quot;和&quot;bar&quot;兩個字，則會傳回結果。 |
| run* | 通配符搜索。 使用星號(*)符合0個或多個字元，這表示如果任何可搜尋欄位的內容包含以&quot;run&quot;開頭的字詞，則會傳回結果。 例如，如果出現&quot;runs&quot;、&quot;running&quot;、&quot;runner&quot;或&quot;runt&quot;等字詞，則會傳回結果。 |
| 小卡？ | 通配符搜索。 使用問號(?) 只匹配一個字元，這表示如果任何可搜尋欄位的內容以「cam」和其他字母開頭，則會傳回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;字樣，則會傳回結果，但如果出現&quot;camera&quot;或&quot;campfire&quot;字樣，則不會傳回結果。 |
| &quot;藍傘&quot; | 片語搜尋。 如果任何可搜尋欄位的內容包含完整字句「blue burmal」，則會傳回結果。 |
| 藍色\~ | 模糊搜索。 或者，您可在波狀符號(~)後加上0-2的數字，以指定編輯距離。 例如，&quot;blue\~1&quot;會傳回&quot;blue&quot;、&quot;blues&quot;或&quot;glue&quot;。 模糊搜尋只 **能套用** 至詞語，不能套用至片語。 不過，您可以在片語中每個字詞的結尾附加波狀符號。 例如，&quot;camping\~ in\~ the\~ summer\~&quot;會與&quot;camping in the summer&quot;相符。 |
| &quot;酒店機場&quot;\~5 | 近距離搜尋。 此類搜尋用於尋找檔案中彼此接近的詞語。 例如，此片語 `"hotel airport"~5` 將在檔案中找到5個字內的&quot;hotel&quot;和&quot;airport&quot;。 |
| `/a[0-9]+b$/` | 規則運算式搜尋。 這種搜索類型根據正斜線&quot;/&quot;之間的內容查找匹配項，如RegExp類中所述。 例如，若要尋找包含&quot;motel&quot;或&quot;hotel&quot;的檔案，請指定 `/[mh]otel/`。 規則運算式搜尋會與單一字詞比對。 |

有關查詢語法的更詳細文檔，請閱讀 [Lucene查詢語法文檔](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。
