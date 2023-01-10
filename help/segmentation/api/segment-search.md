---
keywords: Experience Platform；分段；分段服務；疑難排解；API；區段；區段；區段；搜尋；區段搜尋；
title: 區段搜尋API端點
description: 在Adobe Experience Platform區段服務API中，區段搜尋用於搜尋各種資料來源所包含的欄位，並近乎即時傳回。 本指南提供相關資訊，協助您更清楚了解區段搜尋，並包含使用API執行基本動作的範例API呼叫。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 區段搜尋端點

「區段搜尋」可用來搜尋各種資料來源所包含的欄位，並近乎即時傳回。

本指南提供相關資訊，協助您更清楚了解區段搜尋，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點屬於 [!DNL Adobe Experience Platform Segmentation Service] API。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

除了快速入門區段中概述的必要標題外，向「區段搜尋」端點提出的所有請求都需要下列額外標題：

- x-ups-search-version:&quot;1.0&quot;

### 跨多個命名空間搜尋

此搜尋端點可用來搜尋各種命名空間，並傳回搜尋計數結果清單。 可使用多個參數，以&amp;符號分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}表示與搜索對象關聯的架構類值。 目前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}代表符合Microsoft實作的查詢 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索詞，則與關聯的所有記錄 `schema.name` 將會傳回。 如需更詳細的說明，請參閱 [附錄](#appendix) 檔案。 |

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

成功的回應會傳回HTTP狀態200，並包含下列資訊。

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

此搜索終結點可用於檢索指定命名空間內所有全文索引對象的清單。 可使用多個參數，以&amp;符號分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}包含與搜索對象關聯的架構類值。 目前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必要）** 其中{NAMESPACE}包含要在內搜索的命名空間。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}包含符合Microsoft實作的查詢 [Lucene的搜索語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜索詞，則與關聯的所有記錄 `schema.name` 將會傳回。 如需更詳細的說明，請參閱 [附錄](#appendix) 檔案。 |
| `entityId={ENTITY_ID}` | *（可選）* 將搜索限制為在指定資料夾內，使用{ENTITY_ID}指定。 |
| `limit={LIMIT}` | *（可選）* 其中{LIMIT}表示要返回的搜索結果數。 預設值為 50。 |
| `page={PAGE}` | *（可選）* 其中{PAGE}表示用於為搜索的查詢結果編頁的頁碼。 請注意，頁碼開始於 **0**. |


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

成功的回應會傳回HTTP狀態200，且結果符合搜尋查詢。

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
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}包含與搜索對象關聯的架構類值。 目前，僅 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必要）** 其中{NAMESPACE}包含要在內搜索的命名空間。 |
| `entityId={ENTITY_ID}` | **（必要）** 要獲取有關的結構資訊的搜索對象的ID，用{ENTITY_ID}指定。 |

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

閱讀本指南後，您現在更了解區段搜尋的運作方式。

## 附錄 {#appendix}

以下各節提供搜尋詞如何運作的其他資訊。 搜索查詢的編寫方式如下： `s={FieldName}:{SearchExpression}`. 例如，若要搜尋名為AAM或 [!DNL Platform]，則會使用下列搜尋查詢： `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 為獲得最佳實務，搜尋運算式應進行HTML編碼，如上所示範例。

### 搜尋欄位 {#search-fields}

下表列出可在搜尋查詢參數內搜尋的欄位。

| 欄位名稱 | 說明 |
| ---------- | ----------- |
| folderId | 具有指定搜索的資料夾ID的資料夾或資料夾。 |
| folderLocation | 具有指定搜索的資料夾位置的位置。 |
| parentFolderId | 具有指定搜索的父資料夾ID的段或資料夾。 |
| segmentId | 區段會比對您指定搜尋的區段ID。 |
| segmentName | 區段會比對您指定搜尋的區段名稱。 |
| segmentDescription | 區段會比對您指定搜尋的區段說明。 |

### 搜尋運算式 {#search-expression}

下表列出使用區段搜尋API時，搜尋查詢運作方式的詳細資訊。

>!![NOTE] 下列範例以非HTML編碼格式顯示，以更清楚明瞭。 如需最佳實務，請HTML將搜尋運算式編碼。

| 搜索表達式示例 | 說明 |
| ------------------------- | ----------- |
| foo | 搜索任何單詞。 如果在任何可搜尋欄位中找到&quot;foo&quot;一詞，則會傳回結果。 |
| FOO和條 | 布林值搜尋。 若 **both** 「foo」和「bar」這兩個字都位於任何可搜尋的欄位中。 |
| FOO或條 | 布林值搜尋。 若 **heer** 任何可搜尋欄位都提供&quot;foo&quot;或&quot;bar&quot;字。 |
| FOO NOT欄 | 布林值搜尋。 如果找到&quot;foo&quot;字，但在任何可搜尋欄位中找不到&quot;bar&quot;字，則會傳回結果。 |
| 名稱：FOO和條 | 布林值搜尋。 若 **both** &quot;name&quot;欄位中提供&quot;foo&quot;和&quot;bar&quot;兩字。 |
| 跑* | 通配符搜索。 使用星號(*)可匹配0個或多個字元，這表示如果任何可搜尋欄位的內容包含以「run」開頭的字詞，則會傳回結果。 例如，如果出現&quot;runs&quot;、&quot;running&quot;、&quot;runner&quot;或&quot;runt&quot;等字，則會傳回結果。 |
| 小卡？ | 通配符搜索。 使用問號(?) 只匹配一個字元，這表示如果任何可搜尋欄位的內容以「cam」開頭，並加上其他字母，則會傳回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;兩字，則會傳回結果，但若出現&quot;camera&quot;或&quot;campfire&quot;兩字，則不會傳回結果。 |
| &quot;藍傘&quot; | 片語搜尋。 如果任何可搜尋欄位的內容包含完整字句「藍色傘」，系統便會傳回結果。 |
| 藍色\~ | 模糊搜索。 或者，您可以在波狀符號(~)後面加上0-2之間的數字，以指定編輯距離。 例如，&quot;blue\~1&quot;會傳回&quot;blue&quot;、&quot;blues&quot;或&quot;gule&quot;。 模糊搜索 **僅限** 會套用至詞語，而非詞句。 但是，您可以在短語中的每個單詞的結尾附加波狀符。 比如，&quot;在\~中露營\~到\~夏天\~&quot;與&quot;在夏天露營&quot;相符。 |
| &quot;酒店機場&quot;\~5 | 近距搜索。 此類搜索用於查找文檔中彼此接近的詞。 例如，片語 `"hotel airport"~5` 在檔案中5個字內找到「酒店」和「機場」。 |
| `/a[0-9]+b$/` | 規則運算式搜尋。 如RegExp類中所述，此類搜尋會根據正斜線「/」之間的內容尋找相符項目。 例如，要查找包含&quot;motel&quot;或&quot;hotel&quot;的文檔，請指定 `/[mh]otel/`. 規則運算式搜尋會比對單一字詞。 |

如需查詢語法的詳細檔案，請參閱 [Lucene查詢語法檔案](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
