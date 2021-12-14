---
keywords: Experience Platform；首頁；熱門主題；建立批次；目錄服務；api
solution: Experience Platform
title: 在API中建立批次
topic-legacy: developer guide
description: 您可以在目錄API中向/batches端點提出POST請求，以建立批次。
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 建立批次

資料集若要內嵌資料，必須有與資料集相關聯的批次資料。 使用 `id` 值，您可以透過向POST請求建立批次 `/batches` 端點 [!DNL Catalog] API。

**API格式**

```HTTP
POST /batches
```

**要求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `datasetId` | 此 `id` 批次關聯的資料集。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立），而回應物件會包含新建立批次的詳細資訊，包括其 `id`，此為唯讀、系統產生的字串。

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
