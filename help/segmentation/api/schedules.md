---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 計畫
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 排程開發人員指南

介紹

- 檢索計劃清單
- 建立新排程
- 擷取特定排程
- 更新特定排程
- 刪除特定計畫

## 快速入門

本指南中使用的API端點是區段API的一部分。 在繼續之前，請先閱讀區 [段開發人員指南](./getting-started.md)。

尤其是，區 [段開發人員指南的](./getting-started.md#getting-started) 「快速入門」區段包含相關主題的連結、閱讀檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 檢索計劃清單

您可以向端點提出GET請求，以擷取IMS組織的所有排程清 `/config/schedules` 單。

**API格式**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(可&#x200B;*選*)新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，由&amp;符號(`&`)分隔。 以下列出可用參數。

**查詢參數**

以下是列出計畫的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下呼叫此端點將檢索組織可用的所有計畫。

| 參數 | 說明 |
| --------- | ----------- |
| `start` | 指定偏移的起始頁。 依預設，此值為0。 |
| `limit` | 指定返回的調度數。 依預設，此值為100。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的排程清單列為JSON。

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## 建立新排程

您可以向端點發出POST請求，以建立新的計 `/config/schedules` 划。

**API格式**

```http
POST /config/schedules
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| 參數 | 說明 |
| --------- | ------------ |
| `name` | **必填.** 排程的字串名稱。 |
| `type` | **必填.** 作業的字串類型。 支援的兩種類型是 `batch_segmentation` 和 `export`。 |
| `properties` | **必填.** 包含與調度相關的其他屬性的對象。 |
| `properties.segments` | **等於時`type`為必`batch_segmentation`要。** 使用可 `["*"]` 確保包含所有區段。 |
| `schedule` | **必填.** 包含作業計畫的字串。 有關cron時間表的更多資訊，請閱讀 [cron表達式格式文檔](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此範例中，&quot;0 0 1 * *&quot;表示此排程將在每月首日的午夜執行。 |
| `state` | *可選.* 包含計畫狀態的字串。 兩個受支援狀態是 `active` 和 `inactive`。 預設情況下，狀態設定為 `inactive`。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## 擷取特定排程

通過向端點發出GET請求並在請求路徑中提供計畫值，可以檢索有關特 `/config/schedules` 定計畫的 `id` 詳細資訊。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:您 `id` 要擷取的排程值。

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## 更新特定排程的詳細資料

通過向端點發出PATCH請求並在請求路徑中提 `/config/schedules` 供調度值，可以更新指 `id` 定的調度。

PATCH請求支援兩種不同的路徑： `/state` 和 `/schedule`。

### 更新計畫狀態

您可以使用 `/state` 更新計畫的狀態- 「活動」或「非活動」。 若要更新狀態，您必須將值設為 `active` 或 `inactive`。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:您 `id` 要更新的排程值。

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| 參數 | 說明 |
| --------- | ----------- |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您要更新計畫的狀態，因此需要將值設定為 `path``/state`。 |
| `value` | 的更新值 `/state`。 此值可設為，或 `active` 啟用 `inactive` 或停用排程。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

### 更新計畫cron計畫

您可以使 `schedule` 用來更新cron排程。 有關cron時間表的更多資訊，請閱讀 [cron表達式格式文檔](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:您 `id` 要更新的排程值。

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| 參數 | 說明 |
| --------- | ----------- |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您要更新計畫的cron計畫，因此需要將值設 `path` 為 `/schedule`。 |
| `value` | 的更新值 `/state`。 此值必須以cron計畫的形式。 在此範例中，排程將在每月的第二天執行。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

## 刪除特定計畫

您可以向請求路徑發出DELETE請求並提供計畫值，以 `/config/schedules` 請求刪除指定 `id` 的計畫。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:您 `id` 要刪除的排程值。

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容），並顯示下列訊息：

```json
(No Content) Schedule deleted successfully
```

## 後續步驟
