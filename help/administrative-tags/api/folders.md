---
title: 資料夾端點
description: 瞭解如何使用Adobe Experience Platform API建立、更新、管理和刪除資料夾。
role: Developer
source-git-commit: 8f9a2b5a2063b76518302eb9de38b628c87416e1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 4%

---


# 資料夾端點

>[!IMPORTANT]
>
>這組端點的端點URL為 `https://experience.adobe.io`.

資料夾是一項功能，可讓您更妥善地組織業務物件，以更輕鬆地進行導覽和分類。

本指南提供的資訊可協助您更清楚瞭解資料夾，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 擷取資料夾清單 {#list}

您可以透過向以下網站發出GET請求，擷取屬於您組織的資料夾清單： `/folder` 並指定資料夾型別和父資料夾ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |
| `{PARENT_FOLDER_ID}` | 您要從中擷取資料夾清單的父資料夾ID。 若要檢視所有父資料夾的清單，請使用資料夾ID `root`. |

**要求**

+++列出所有頂層資料夾的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含貴組織中資料集的所有頂層資料夾清單。

+++此範例回應包含貴組織中資料集的所有頂層資料夾清單。

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## 建立新資料夾 {#create}

您可以透過向以下網站發出POST請求來建立新資料夾： `/folder` 端點並指定資料夾型別。

**API格式**

```http
POST /folder/{FOLDER_TYPE}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |

**要求**

+++建立新資料夾的範例要求。

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 您要建立的資料夾名稱。 |
| `parentId` | 上層資料夾的ID。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及您新建立資料夾的詳細資料。

+++包含新建立資料夾詳細資訊的範例回應。

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建立的資料夾的ID。 |
| `createdBy` | 建立資料夾的使用者ID。 |
| `createdAt` | 資料夾建立時間的時間戳記。 |
| `modifiedBy` | 上次修改資料夾的使用者識別碼。 |
| `modifiedAt` | 資料夾上次更新的時間戳記。 |

+++

## 擷取特定資料夾 {#get}

您可以透過向以下專案發出GET請求，擷取屬於您組織的特定資料夾： `/folder` 並指定資料夾型別和資料夾的ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 您要擷取的資料夾識別碼。 |

**要求**

+++擷取特定資料夾的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及要求的資料夾詳細資料。

+++包含請求資料夾詳細資訊的範例回應。

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 要求的資料夾識別碼。 |
| `name` | 要求的資料夾名稱。 |
| `parentId` | 上層資料夾的ID。 |
| `createdBy` | 建立資料夾的使用者ID。 |
| `createdAt` | 資料夾建立時間的時間戳記。 |
| `modifiedBy` | 上次更新資料夾的使用者ID。 |
| `modifiedAt` | 資料夾上次更新的時間戳記。 |
| `status` | 要求的資料夾狀態。 支援的值包括 `IN_USE` 和 `ARCHIVED`. |

+++

## 驗證指定的資料夾 {#validate}

您可以透過向以下專案發出GET請求，驗證資料夾是否符合在其中放置物件的條件： `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` 端點，並提供資料夾型別和ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 您正在驗證的資料夾的ID。 |

**要求**

+++驗證特定資料夾的範例要求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功狀態會傳回HTTP狀態200以及您正在驗證的資料夾詳細資訊。

+++範例回應包含已驗證資料夾的詳細資訊

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## 更新特定資料夾 {#update}

您可以透過向以下專案發出PATCH請求，更新屬於您組織的特定資料夾的詳細資料： `/folder` 並指定資料夾型別和資料夾的ID。

**API格式**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 您要更新的資料夾識別碼。 |

**要求**

+++更新特定資料夾的範例請求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及有關您新更新資料夾的資訊。

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## 刪除特定資料夾 {#delete}

您可以透過向以下專案發出DELETE請求，刪除屬於您組織的特定資料夾： `/folder` 並指定資料夾型別和資料夾的ID。

***API格式**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 資料夾中包含的物件型別。 支援的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 您要刪除的資料夾的ID。 |

**要求**

+++刪除特定資料夾的範例請求

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，並包含訊息內文，通知您資料夾的刪除作業。

```json
{
    "message": "delete request accepted successfully"
}
```

## 後續步驟

閱讀本指南後，您現在已更能瞭解如何使用Adobe Experience Platform API建立、管理和刪除資料夾。
