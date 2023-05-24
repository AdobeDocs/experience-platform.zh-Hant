---
keywords: Experience Platform；分段；分段服務；故障排除；API;seg;segment;Segment;search;segment search;segment search;
title: 段搜索API終結點
description: 在Adobe Experience Platform分段服務API中，段搜索用於搜索包含在各種資料源中的欄位，並以接近即時的方式返回這些欄位。 本指南提供資訊，幫助您更好地瞭解段搜索，並包括使用API執行基本操作的示例API調用。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 段搜索終結點

段搜索用於搜索包含在各種資料源中的欄位，並以接近即時的方式返回這些欄位。

本指南提供資訊，幫助您更好地瞭解段搜索，並包括使用API執行基本操作的示例API調用。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

除了入門部分中概述的必需標頭外，所有對段搜索終結點的請求都需要以下附加標頭：

- x-ups-search-version:&quot;1.0&quot;

### 跨多個命名空間搜索

此搜索終結點可用於跨各種命名空間搜索，返回搜索計數結果的清單。 可以使用多個參數，用和符號(&amp;)分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}表示與搜索對象關聯的架構類值。 當前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}表示符合Microsoft的 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜索術語，則與關聯的所有記錄 `schema.name` 的雙曲餘切值。 更詳細的解釋可在 [附錄](#appendix) 的子菜單。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功響應返回HTTP狀態200，並返回以下資訊。

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

### 搜索單個實體

此搜索終結點可用於檢索指定命名空間中所有全文索引對象的清單。 可以使用多個參數，用和符號(&amp;)分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含與搜索對象關聯的架構類值。 當前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含要在其中搜索的命名空間。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}包含符合Microsoft的 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 如果未指定搜索術語，則與關聯的所有記錄 `schema.name` 的雙曲餘切值。 更詳細的解釋可在 [附錄](#appendix) 的子菜單。 |
| `entityId={ENTITY_ID}` | *（可選）* 將搜索限制為在指定的資料夾內（使用{ENTITY_ID}指定）。 |
| `limit={LIMIT}` | *（可選）* 其中{LIMIT}表示要返回的搜索結果數。 預設值為 50。 |
| `page={PAGE}` | *（可選）* 其中{PAGE}表示用於對搜索的查詢結果進行分頁的頁碼。 請注意，頁碼的開頭是 **0**。 |


**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功的響應返回HTTP狀態200，結果與搜索查詢匹配。

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

### 獲取有關搜索對象的結構資訊

此搜索端點可用於獲取有關所請求搜索對象的結構資訊。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必需）** 其中{SCHEMA}包含與搜索對象關聯的架構類值。 當前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必需）** 其中{NAMESPACE}包含要在其中搜索的命名空間。 |
| `entityId={ENTITY_ID}` | **（必需）** 要獲取有關的結構資訊的搜索對象的ID，使用{ENTITY_ID}指定。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關所請求搜索對象的詳細結構資訊。

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

閱讀本指南後，您現在可以更好地瞭解段搜索的工作方式。

## 附錄 {#appendix}

以下各節提供了有關搜索詞如何工作的附加資訊。 搜索查詢的編寫方式如下： `s={FieldName}:{SearchExpression}`。 例如，要搜索名為或的AAM段 [!DNL Platform]，將使用以下搜索查詢： `s=segmentName:AAM%20OR%20Platform`。

> !![NOTE] 對於最佳做法，搜索表達式應像上面所示的示例那樣進行HTML編碼。

### 搜索欄位 {#search-fields}

下表列出了可在搜索查詢參數中搜索的欄位。

| 欄位名稱 | 說明 |
| ---------- | ----------- |
| 資料夾ID | 具有指定搜索的資料夾ID的資料夾或資料夾。 |
| 資料夾位置 | 具有指定搜索的資料夾位置的位置或位置。 |
| 父資料夾ID | 具有指定搜索的父資料夾ID的段或資料夾。 |
| 段ID | 段與指定搜索的段ID匹配。 |
| 段名稱 | 段與指定搜索的段名稱匹配。 |
| segmentDescription | 該段與指定搜索的段說明匹配。 |

### 搜索表達式 {#search-expression}

下表列出了使用段搜索API時搜索查詢的具體工作方式。

>!![NOTE] 以下示例以非HTML編碼格式顯示，以便更清晰。 為了獲得最佳實踐，HTML對搜索表達式進行編碼。

| 示例搜索表達式 | 說明 |
| ------------------------- | ----------- |
| fook | 搜索任何單詞。 如果在任何可搜索欄位中都找到單詞&quot;foo&quot;，則此操作將返回結果。 |
| foo和欄 | 布爾搜索。 如果 **兩者** 「foo」和「bar」字在任何可搜索欄位中找到。 |
| foo OR欄 | 布爾搜索。 如果 **或** 在任何可搜索欄位中都可找到單詞&quot;foo&quot;或單詞&quot;bar&quot;。 |
| foo NOT欄 | 布爾搜索。 如果在任何可搜索欄位中都找不到單詞&quot;foo&quot;，則返回結果。 |
| 名稱：foo和欄 | 布爾搜索。 如果 **兩者** 「foo」和「bar」在「name」欄位中找到。 |
| 運行 | 通配符搜索。 使用星號(*)匹配0個或更多字元，這意味著如果任何可搜索欄位的內容包含以「run」開頭的單詞，則返回結果。 例如，如果出現「runs」、「running」、「runner」或「runt」等字，則此操作將返回結果。 |
| 小卡？ | 通配符搜索。 使用問號(?) 只匹配一個字元，這意味著如果任何可搜索欄位的內容以「cam」和附加字母開頭，則返回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;等字，則返回結果；如果出現&quot;camera&quot;或&quot;campfire&quot;等字，則不返回結果。 |
| &quot;藍傘&quot; | 片語搜索。 如果任何可搜索欄位的內容包含全片語「藍色雨傘」，則將返回結果。 |
| 藍色\~ | 模糊搜索。 或者，可以在顎化符(~)後加上一個介於0-2之間的數字來指定編輯距離。 例如，「blue\~1」將返回「blue」、「blues」或「gluse」。 模糊搜索 **僅** 應用於術語，而不是短語。 但是，可以在短語中將顎化符附加到每個單詞的末尾。 例如，&quot;camping\~ in\~ the\~ summer\~&quot;與&quot;camping in the summer\~&quot;相匹配。 |
| &quot;酒店機場&quot;\~5 | 近距搜索。 此類搜索用於查找文檔中彼此接近的詞。 例如，短語 `"hotel airport"~5` 在檔案中找到5字以內的&quot;旅館&quot;和&quot;機場&quot;。 |
| `/a[0-9]+b$/` | 規則運算式搜索。 此類搜索基於正斜槓「/」之間的內容查找匹配項，如RegExp類中所述。 例如，要查找包含&quot;motel&quot;或&quot;hotel&quot;的文檔，請指定 `/[mh]otel/`。 規則運算式搜索與單詞匹配。 |

有關查詢語法的更詳細文檔，請閱讀 [Lucene查詢語法文檔](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。
