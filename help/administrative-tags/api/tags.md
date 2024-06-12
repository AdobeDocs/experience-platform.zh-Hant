---
title: 整合標籤端點
description: 瞭解如何使用Adobe Experience Platform API建立、更新、管理和刪除標籤類別和標籤。
role: Developer
source-git-commit: ede314d0cbe50514090915fccf7ef3c2a5254b7a
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 3%

---


# 統一標籤端點

>[!IMPORTANT]
>
>這組端點的端點URL為 `https://experience.adobe.io`.

標籤是一項可讓您管理中繼資料分類法的功能，可分類商業物件以便輕鬆探索和分類。 您之後可以透過將這些標籤新增到標籤類別來組織這些標籤到其他群組中。

本指南提供的資訊可協助您更清楚瞭解標籤和標籤類別，並且包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南使用的端點是Adobe Experience Platform API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標題以及如何讀取範例API呼叫

### 字彙

下列字彙表著重說明 **標籤** 和 **標籤類別**.

- **標籤**：標籤可讓您管理商業物件的中繼資料分類法，好讓您可以分類這些物件，以便輕鬆探索和分類。
   - **未分類的標籤**：未分類的標籤是不屬於標籤類別的標籤。 依預設，建立的標籤將不會分類。
- **標籤類別**：標籤類別可讓您將標籤分組為有意義的設定，讓您為標籤的用途提供更多內容。

## 擷取標籤類別的清單 {#get-tag-categories}

您可以透過向以下網站發出GET請求，擷取屬於您組織的標籤類別清單： `/tagCategory` 端點。

**API格式**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

擷取標籤類別時，可使用下列選用的查詢引數。

| 查詢引數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `start` | 結果清單的開始位置。 您可以使用它來指示結果分頁的開始索引。 | `start=a` |
| `limit` | 每頁擷取的標籤類別數上限。 | `limit=20` |
| `property` | 擷取標籤類別時，您要篩選的屬性。 支援的值包括： &lt;ul><li>`name`：標籤類別的名稱。</li></ul> | `property=name==category` |
| `sortBy` | 標籤類別排序的順序。 支援的值包括 `name`， `createdAt`、和 `modifiedAt`. | `sortBy=name` |
| `sortOrder` | 標籤類別排序的方向。 支援的值包括 `asc` 和 `desc`. | `sortOrder=asc` |

**要求**

+++列出組織中所有標籤類別的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含貴組織所有標籤類別的清單。

+++包含組織中所有標籤類別清單的範例回應。

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## 建立新標籤類別 {#create-tag-category}

>[!IMPORTANT]
>
>只有系統管理員和產品管理員可以使用此API呼叫。

您可以透過向以下網站發出POST請求，建立新的標籤類別： `/tagCategory` 端點。

**API格式**

```http
POST /tagCategory
```

**要求**

+++建立新標籤類別的範例要求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 您要建立的標籤類別名稱。 |
| `description` | 您要建立的標籤類別說明。 |

+++

**回應**

範例回應會傳回HTTP狀態200以及新建立標籤類別的詳細資料。

+++包含新建立標籤類別詳細資訊的範例回應。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 擷取特定標籤類別 {#get-tag-category}

您可以透過向以下專案發出GET請求，擷取屬於您組織的特定標籤類別： `/tagCategory` 端點並指定標籤類別的ID。

**API格式**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 您要擷取的標籤類別ID。 |

**要求**

+++擷取特定標籤類別的範例請求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及指定標籤類別的詳細資料。

+++包含指定標籤類別詳細資訊的範例回應。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 請求的標籤類別的ID。 |
| `name` | 要求的標籤類別名稱。 |
| `description` | 要求之標籤類別的說明。 |
| `createdBy` | 建立標籤類別的使用者ID。 |
| `createdAt` | 建立標籤類別時的時間戳記。 |
| `modifiedBy` | 上次更新標籤類別的使用者ID。 |
| `modifiedAt` | 標籤類別上次更新的時間戳記。 |
| `tagCount` | 屬於標籤類別的標籤數。 |

+++

## 更新特定標籤類別 {#update-tag-category}

>[!IMPORTANT]
>
>只有系統管理員和產品管理員可以使用此API呼叫。

您可以透過向以下專案發出PATCH請求，更新屬於您組織的特定標籤類別的詳細資料： `/tagCategory` 端點並指定標籤類別的ID。

**API格式**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 您要擷取的標籤類別ID。 |

**要求**

+++更新特定標籤類別的範例請求

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| 參數 | 說明 |
| --------- | ----------- |
| `op` | 完成的作業。 若要更新特定標籤類別，請將此值設為 `replace`. |
| `path` | 將更新的欄位路徑。 支援的值包括 `name` 和 `description`. |
| `value` | 要更新的欄位之更新值。 |
| `from` | 要更新的欄位原始值。 |

+++

**回應**

成功回應HTTP狀態200，其中包含您新更新標籤類別的相關資訊。

+++包含新更新標籤類別詳細資訊的範例回應。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 刪除特定標籤類別 {#delete-tag-category}

>[!IMPORTANT]
>
>只有系統管理員和產品管理員可以使用此API呼叫。

您可以透過向以下專案發出DELETE請求，刪除屬於您組織的特定標籤類別： `/tagCategory` 端點並指定標籤類別的ID。

**API格式**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 您要擷取的標籤類別ID。 |

**要求**

+++刪除特定標籤類別的範例請求

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及空白回應。

## 擷取標籤清單 {#get-tags}

您可以透過向以下網站發出GET請求，擷取屬於您組織的標籤清單： `/tags` 端點以及標籤類別的ID。

**API格式**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

擷取標籤時，可使用下列選用的查詢引數。

| 查詢引數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `start` | 結果清單的開始位置。 您可以使用它來指示結果分頁的開始索引。 | `start=a` |
| `limit` | 每頁要擷取的標籤數上限。 | `limit=20` |
| `property` | 擷取標籤時，您要篩選的屬性。 支援的值包括：<ul><li>`name`：標籤的名稱。</li><li>`archived`：是否封存或取消封存標籤。 您可以將此值設為 `true` 或 `false`.</li><li>`tagCategoryId`：標籤所屬的標籤類別的ID。</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | 標籤排序的順序。 支援的值包括 `name`， `createdAt`、和 `modifiedAt`. | `sortBy=name` |
| `sortOrder` | 標籤類別排序的方向。 支援的值包括 `asc` 和 `desc`. | `sortOrder=asc` |


**要求**

+++擷取屬於特定標籤類別之所有標籤的範例請求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含屬於該標籤類別的標籤詳細資訊。

+++ 包含請求標籤詳細資訊的範例回應。

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## 建立新標籤 {#create-tag}

>[!IMPORTANT]
>
>只有系統管理員和產品管理員可以使用此API呼叫，在指定的標籤類別中建立新標籤。
>
>如果您要建立未分類的標籤，您可以 **非** 需要管理員許可權。

您可以透過向以下網站發出POST請求來建立新標籤： `/tags` 端點。

**API格式**

```http
POST /tags
```

**要求**

+++建立新標籤的範例要求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | **必填**. 您要建立的標簽名稱。 |
| `tagCategoryId` | *可選*. 您要標籤所屬的標籤類別ID。 如果未指定，則會建立標籤作為「未分類」類別的一部分。 |

+++

**回應**

成功的回應會傳回HTTP狀態201以及新建立標籤的詳細資料。

+++包含新建立標籤詳細資料的範例回應。

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `name` | 新建立標籤的名稱。 |
| `id` | 新建立標籤的ID。 |
| `org` | 標籤所屬組織的ID。 |
| `createdAt` | 建立標籤時的時間戳記。 |
| `createdBy` | 建立標籤的使用者ID。 |
| `modifiedAt` | 標籤上次更新的時間戳記。 |
| `modifiedBy` | 上次更新標籤的使用者ID。 |
| `tagCategoryId` | 標籤所屬的標籤類別ID。 |
| `tagCategoryName` | 標籤所屬的標籤類別名稱。 |

+++

## 擷取特定標籤 {#get-tag}

您可以透過向以下網站發出GET請求，擷取屬於您組織的特定標籤： `/tags` 端點，並指定您要擷取的標籤ID。

**API格式**

```http
GET /tags/{TAG_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_ID}` | 您要擷取的標籤ID。 |

**要求**

+++擷取特定標籤的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及指定標籤的詳細資料。

+++包含指定標籤詳細資訊的範例回應。

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `name` | 您擷取的標籤名稱。 |
| `id` | 您擷取的標籤ID。 |
| `org` | 標籤所屬組織的ID。 |
| `createdAt` | 建立標籤時的時間戳記。 |
| `createdBy` | 建立標籤的使用者ID。 |
| `modifiedAt` | 標籤上次更新的時間戳記。 |
| `modifiedBy` | 上次更新標籤的使用者ID。 |
| `tagCategoryId` | 標籤所屬的標籤類別ID。 |
| `tagCategoryName` | 標籤所屬的標籤類別名稱。 |
| `archived` | 標籤的封存狀態。 如果設為 `true`，表示標籤已封存。 |

+++

## 驗證標籤 {#validate-tags}

您可以透過向發出POST請求來驗證標籤是否存在 `/tags/validate` 端點。

**API格式**

```http
POST /tags/validate
```

**要求**

+++驗證所提供標籤ID的範例要求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `ids` | 包含您要驗證之標籤ID清單的陣列。 |
| `entity` | 請求驗證的實體。 您可以使用 `{API_KEY}` 此引數的值。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含哪些標籤有效及無效的資訊。

+++顯示哪些標籤有效及無效的範例回應。

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `invalidTags` | 包含無效標籤ID清單的陣列。 |
| `validTags` | 包含有效標籤ID清單的陣列。 |

+++

## 更新特定標籤 {#update-tag}

您可以透過向以下專案發出PATCH請求來更新指定的標籤： `/tags` 端點，並提供您要更新的標籤ID。

**API格式**

```http
PATCH /tags/{TAG_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_ID}` | 您要更新之標籤的ID。 |

**要求**

+++更新特定標籤的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `op` | 需要完成的作業。 在此使用案例中，此設定一律為 `replace`. |
| `path` | 將更新的欄位路徑。 支援的值包括 `name`， `archived`、和 `tagCategoryId`. |
| `value` | 要更新的欄位之更新值。 |
| `from` | 要更新的欄位原始值。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及新更新標籤的詳細資訊。

+++包含更新標籤詳細資訊的範例回應。

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## 刪除特定標籤 {#delete-tag}

>[!IMPORTANT]
>
>只有系統管理員和產品管理員可以使用此API呼叫。
>
>此外，標籤 **無法** 與任何企業物件相關聯，並且 **必須** 在您可以刪除標籤之前先封存。 您可以使用封存標籤 [更新標籤端點](#update-tag).

您可以透過對以下專案建立DELETE標籤來刪除特定標籤： `/tags` 並指定您要刪除之標籤的ID。

**API格式**

```http
DELETE /tags/{TAG_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TAG_ID}` | 您要刪除之標籤的ID。 |

**要求**

+++刪除特定標籤的範例請求

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及空白回應。

## 後續步驟

閱讀本指南後，您已更加瞭解如何使用Adobe Experience Platform API建立、管理和刪除標籤和標籤類別。 如需使用UI管理標籤的詳細資訊，請參閱 [managing tags指南](../ui/managing-tags.md). 如需使用UI管理標籤類別的詳細資訊，請參閱 [標籤類別指南](../ui/tags-categories.md).
