---
keywords: Experience Platform;home;popular topics;create batch;catalog service;api
solution: Experience Platform
title: 建立資料集
topic: developer guide
description: 為了讓資料集收錄資料，資料集必須有與其關聯的批次。 使用現有資料集的id值，您可以透過對目錄API中的/batches端點提出POST請求來建立批次。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 3%

---


# 建立批次

為了讓資料集收錄資料，資料集必須有與其關聯的批次。 使用現 `id` 有資料集的值，您可以透過對API中的端點提出POST要求來 `/batches` 建立批 [!DNL Catalog] 次。

**API格式**

```HTTP
POST /batches
```

**請求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `datasetId` | 批 `id` 次將關聯的資料集。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立批的詳細資訊的響應對象，包括其只讀 `id`系統生成的字串。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
