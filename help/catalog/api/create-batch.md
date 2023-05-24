---
keywords: Experience Platform；首頁；熱門主題；建立批處理；目錄服務；api
solution: Experience Platform
title: 在API中建立批
description: 可以通過向目錄API中的/batches終結點發出POST請求來建立批。
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 建立批

為了使資料集能夠接收資料，它必須具有與其關聯的批處理。 使用 `id` 現有資料集的值，可以通過向POST請求建立批 `/batches` 端點 [!DNL Catalog] API。

**API格式**

```HTTP
POST /batches
```

**要求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `datasetId` | 的 `id` 將與批關聯的資料集。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立批的詳細資訊（包括其）的響應對象 `id`，只讀，系統生成的字串。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
