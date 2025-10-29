---
title: 區段搜尋API端點
description: Adobe Experience Platform Segmentation Service API中，區段搜尋是用來搜尋各種資料來源包含的欄位，並近乎即時地傳回。 本指南提供的資訊可協助您更清楚瞭解區段搜尋，且包含使用API執行基本動作的範例API呼叫。
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 2%

---

# 區段搜尋端點

區段搜尋用於搜尋各種資料來源包含的欄位，並近乎即時地傳回這些欄位。

本指南提供的資訊可協助您更清楚瞭解區段搜尋，且包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

除了快速入門一節中列出的必要標題外，所有對區段搜尋端點的請求都需要以下額外標題：

- x-ups-search-version： &quot;1.0&quot;

### 在多個名稱空間中搜尋

此搜尋端點可用於跨不同名稱空間搜尋，並傳回搜尋計數結果的清單。 可使用多個引數，以&amp;分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）**&#x200B;其中{SCHEMA}代表與搜尋物件相關聯的結構描述類別值。 目前僅支援`_xdm.context.segmentdefinition`。 |
| `s={SEARCH_TERM}` | *（選擇性）*&#x200B;其中{SEARCH_TERM}代表符合Microsoft實作[Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)的查詢。 如果未指定搜尋字詞，則會傳回與`schema.name`關聯的所有記錄。 如需更詳細的說明，請參閱本檔案的[附錄](#appendix)。 |

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

成功的回應會傳回HTTP狀態200及以下資訊。

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

此搜尋端點可用來擷取指定名稱空間內所有全文檢索索引物件的清單。 可使用多個引數，以&amp;分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）**&#x200B;其中{SCHEMA}包含與搜尋物件相關聯的結構描述類別值。 目前僅支援`_xdm.context.segmentdefinition`。 |
| `namespace={NAMESPACE}` | **（必要）**&#x200B;其中{NAMESPACE}包含您要搜尋的名稱空間。 |
| `s={SEARCH_TERM}` | *（選擇性）*&#x200B;其中{SEARCH_TERM}包含符合Microsoft實作[Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)的查詢。 如果未指定搜尋字詞，則會傳回與`schema.name`關聯的所有記錄。 如需更詳細的說明，請參閱本檔案的[附錄](#appendix)。 |
| `entityId={ENTITY_ID}` | *（選擇性）*&#x200B;將搜尋限制在指定的資料夾內，並以{ENTITY_ID}指定。 |
| `limit={LIMIT}` | *（選擇性）*&#x200B;其中{LIMIT}代表要傳回的搜尋結果數目。 預設值為 50。 |
| `page={PAGE}` | *（選擇性）*&#x200B;其中{PAGE}代表用於分頁搜尋之查詢結果的頁碼。 請注意，頁碼從&#x200B;**0**&#x200B;開始。 |


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

成功的回應會傳回HTTP狀態200，且結果與搜尋查詢相符。

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

此搜尋端點可用於取得有關要求的搜尋物件的結構資訊。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 參數 | 說明 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）**&#x200B;其中{SCHEMA}包含與搜尋物件相關聯的結構描述類別值。 目前僅支援`_xdm.context.segmentdefinition`。 |
| `namespace={NAMESPACE}` | **（必要）**&#x200B;其中{NAMESPACE}包含您要搜尋的名稱空間。 |
| `entityId={ENTITY_ID}` | **（必要）**&#x200B;您要取得結構資訊之搜尋物件的識別碼，以{ENTITY_ID}指定。 |

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

成功的回應會傳回HTTP狀態200，其中包含有關請求搜尋物件的詳細結構資訊。

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

閱讀本指南後，您現在能更清楚瞭解區段搜尋的運作方式。

## 附錄 {#appendix}

以下幾節提供有關搜尋詞如何運作的額外資訊。 搜尋查詢的寫入方式如下： `s={FieldName}:{SearchExpression}`。 因此，舉例來說，若要搜尋名為AAM或[!DNL Platform]的區段定義，您可以使用下列搜尋查詢： `s=segmentName:AAM%20OR%20Platform`。

>[!NOTE]
>
>為達到最佳實務，搜尋運算式應使用HTML編碼，如上述範例所示。

### 搜尋欄位 {#search-fields}

下表列出可在搜尋查詢引數中搜尋的欄位。

| 欄位名稱 | 說明 |
| ---------- | ----------- |
| folderId | 具有您指定之搜尋的資料夾ID的資料夾。 |
| folderLocation | 具有您指定之搜尋的資料夾位置的一或多個位置。 |
| parentFolderId | 具有您指定之搜尋的父資料夾ID的區段定義或資料夾。 |
| segmentId | 符合指定搜尋的區段ID的區段定義。 |
| segmentName | 符合指定搜尋之區段名稱的區段定義。 |
| segmentDescription | 符合指定搜尋之區段說明的區段定義。 |

### 搜尋運算式 {#search-expression}

下表列出使用區段搜尋API時，搜尋查詢運作方式的詳細資訊。

>[!NOTE]
>
>下列範例以非HTML編碼格式顯示，以更清楚明瞭。 為求最佳實務，HTML會對您的搜尋運算式進行編碼。

| 搜尋運算式範例 | 說明 |
| ------------------------- | ----------- |
| foo | 搜尋任何單字。 如果在任何可搜尋欄位中找到「foo」這個字，就會傳回結果。 |
| Foo和BAR | 布林值搜尋。 如果在任何可搜尋欄位中找到&#x200B;**字詞「foo」和「bar」，則會傳回結果。** |
| foo OR列 | 布林值搜尋。 如果在任何可搜尋欄位中找到&#x200B;**任何**&#x200B;單字「foo」或「bar」都會傳回結果。 |
| foo NOT列 | 布林值搜尋。 如果找到「foo」一詞，但在任何可搜尋欄位中找不到「bar」一詞，則會傳回結果。 |
| 名稱： foo AND列 | 布林值搜尋。 如果&#x200B;**在[名稱]欄位中找到[foo]和[bar]這兩個字，就會傳回結果。** |
| 執行* | 萬用字元搜尋。 使用星號(*)會符合0或更多字元，這表示如果任何可搜尋欄位的內容包含以「run」開頭的單字，則會傳回結果。 例如，如果出現「runs」、「running」、「runner」或「runt」等字詞，就會傳回結果。 |
| 凸輪？ | 萬用字元搜尋。 使用問號(？) 只符合一個字元，這表示如果任何可搜尋欄位的內容以「cam」和另一個字母開頭，則會傳回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;字詞，這將傳回結果，但如果&quot;camera&quot;或&quot;campfire&quot;字詞出現，將不會傳回結果。 |
| 「藍色雨傘」 | 字詞搜尋。 如果任何可搜尋欄位的內容包含完整的片語「藍色雨傘」，則會傳回結果。 |
| 藍色\~ | 模糊搜尋。 或者，您可以在波狀符號(~)後面加上一個介於0到2之間的數字，以指定編輯距離。 例如，「blue\~1」會傳回「blue」、「blues」或「glue」。 模糊搜尋&#x200B;**只能**&#x200B;套用至辭彙，而非片語。 不過，您可以在片語中每個字的結尾附加波狀符號。 舉例來說，「夏令營」與「夏令營」並不相符。 |
| 「飯店機場」\~5 | 近似程度搜尋。 這類搜尋用於尋找檔案中彼此接近的字詞。 例如，片語`"hotel airport"~5`會在檔案中找到5個字內相隔的字詞「hotel」和「airport」。 |
| `/a[0-9]+b$/` | 規則運算式搜尋。 這類搜尋會根據正斜線「/」之間的內容尋找相符專案，如RegExp類別中所述。 例如，若要尋找包含「motel」或「hotel」的檔案，請指定`/[mh]otel/`。 規則運算式搜尋會根據單一字詞進行比對。 |

如需有關查詢語法的詳細檔案，請參閱[Lucene查詢語法檔案](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。
