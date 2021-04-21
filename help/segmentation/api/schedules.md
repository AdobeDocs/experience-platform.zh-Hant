---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；調度；計畫；api;API;
solution: Experience Platform
title: 排程API端點
topic-legacy: developer guide
description: 排程是一種工具，可用來每天自動執行一次批次分段工作。
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---

# 計畫端點

排程是一種工具，可用來每天自動執行一次批次分段工作。 您可以使用`/config/schedules`端點來檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請參閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 檢索計劃清單{#retrieve-list}

您可以向`/config/schedules`端點提出GET請求，以擷取IMS組織的所有排程清單。

**API格式**

`/config/schedules`端點支援數個查詢參數，以協助篩選結果。 雖然這些參數是可選的，但強烈建議使用這些參數以幫助降低昂貴的開銷。 在沒有參數的情況下呼叫此端點將檢索組織可用的所有計畫。 可以包括多個參數，用&amp;符號(`&`)分隔。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{START}` | 指定偏移的起始頁。 依預設，此值為0。 |
| `{LIMIT}` | 指定返回的調度數。 依預設，此值為100。 |

**要求**

下列請求將擷取IMS組織中張貼的最後十個排程。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的排程清單列為JSON。

>[!NOTE]
>
>下列回應已截斷空間，並僅顯示傳回的第一個排程。

```json
{
    "_page": {
        "totalCount": 10,
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

| 屬性 | 說明 |
| -------- | ------------ |
| `_page.totalCount` | 傳回的排程總數。 |
| `_page.pageSize` | 排程頁面的大小。 |
| `children.name` | 排程的字串名稱。 |
| `children.type` | 作業的字串類型。 支援的兩種類型為「batch_segmentation」和「export」。 |
| `children.properties` | 包含與調度相關的其他屬性的對象。 |
| `children.properties.segments` | 使用`["*"]`可確保包含所有區段。 |
| `children.schedule` | 包含作業計畫的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 有關cron計畫的更多資訊，請閱讀[cron表達式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)文檔。 在此範例中，&quot;0 0 1 * *&quot;表示此排程將在每月首日的午夜執行。 |
| `children.state` | 包含計畫狀態的字串。 兩個支援的狀態是「作用中」和「非作用中」。 依預設，狀態會設為「非作用中」。 |

## 建立新計畫{#create}

您可以通過向`/config/schedules`端點發出POST請求來建立新調度。

**API格式**

```http
POST /config/schedules
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| 屬性 | 說明 |
| -------- | ------------ |
| `name` | **必填。** 排程的字串名稱。 |
| `type` | **必填。** 作業的字串類型。支援的兩種類型為「batch_segmentation」和「export」。 |
| `properties` | **必填。** 包含與調度相關的其他屬性的對象。 |
| `properties.segments` | **等於「 `type` batch_segmentation」時為必要項目。** 使用 `["*"]` 可確保包含所有區段。 |
| `schedule` | *選擇性.* 包含作業計畫的字串。作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 有關cron計畫的更多資訊，請閱讀[cron表達式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)文檔。 在此範例中，&quot;0 0 1 * *&quot;表示此排程將在每月首日的午夜執行。 <br><br>如果未提供此字串，系統會自動產生排程。 |
| `state` | *選擇性.* 包含計畫狀態的字串。兩個支援的狀態是「作用中」和「非作用中」。 依預設，狀態會設為「非作用中」。 |

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

## 檢索特定計畫{#get}

通過向`/config/schedules`端點發出GET請求，並在請求路徑中提供要檢索的調度的ID，可以檢索有關特定調度的詳細資訊。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 您要擷取之排程的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
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
}
```

| 屬性 | 說明 |
| -------- | ------------ |
| `name` | 排程的字串名稱。 |
| `type` | 作業的字串類型。 支援的兩種類型是`batch_segmentation`和`export`。 |
| `properties` | 包含與調度相關的其他屬性的對象。 |
| `properties.segments` | 使用`["*"]`可確保包含所有區段。 |
| `schedule` | 包含作業計畫的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 有關cron計畫的更多資訊，請閱讀[cron表達式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)文檔。 在此範例中，&quot;0 0 1 * *&quot;表示此排程將在每月首日的午夜執行。 |
| `state` | 包含計畫狀態的字串。 支援的兩種狀態為`active`和`inactive`。 預設情況下，狀態設定為`inactive`。 |

## 更新特定計畫{#update}的詳細資料

您可以通過向`/config/schedules`端點發出PATCH請求並提供您嘗試在請求路徑中更新的計畫的ID來更新特定計畫。

PATCH請求允許您更新個別計畫的[state](#update-state)或[cron計畫](#update-schedule)。

### 更新計畫狀態{#update-state}

您可以使用JSON修補程式作業來更新排程的狀態。 若要更新狀態，請將`path`屬性宣告為`/state`，並將`value`設為`active`或`inactive`。 如需JSON修補程式的詳細資訊，請閱讀[JSON修補程式](http://jsonpatch.com/)檔案。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 您要更新的計畫的`id`值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您要更新計畫的狀態，因此需要將`path`的值設定為&quot;/state&quot;。 |
| `value` | 計畫狀態的更新值。 此值可設為「作用中」或「非作用中」以啟用或停用排程。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

### 更新cron計畫{#update-schedule}

您可以使用JSON修補程式作業來更新cron排程。 要更新計畫，請將`path`屬性聲明為`/schedule`，並將`value`設定為有效的cron計畫。 如需JSON修補程式的詳細資訊，請閱讀[JSON修補程式](http://jsonpatch.com/)檔案。 有關cron計畫的更多資訊，請閱讀[cron表達式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)文檔。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 您要更新的計畫的`id`值。 |

**要求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `path` | 您要更新的值的路徑。 在這種情況下，由於您正在更新cron計畫，因此需要將`path`的值設定為`/schedule`。 |
| `value` | cron計畫的更新值。 此值必須以cron排程的形式。 在此範例中，排程將在每月的第二天執行。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

## 刪除特定計畫

您可以向`/config/schedules`端點發出DELETE請求，並在請求路徑中提供要刪除的計畫ID，以請求刪除特定計畫。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要刪除的計畫的`id`值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

## 後續步驟

閱讀本指南後，您現在可以進一步瞭解排程的運作方式。
