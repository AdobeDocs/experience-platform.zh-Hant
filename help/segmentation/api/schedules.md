---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；排程；排程；API; API;
solution: Experience Platform
title: 排程API端點
description: 排程是一種工具，可用來每天自動執行一次批次分段工作。
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 3%

---

# 計畫端點

排程是一種工具，可用來每天自動執行一次批次分段工作。 您可以使用 `/config/schedules` 端點來檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

## 快速入門

本指南中使用的端點屬於 [!DNL Adobe Experience Platform Segmentation Service] API。 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功對API進行呼叫，您必須知道的重要資訊，包括必要的標題以及如何讀取範例API呼叫。

## 擷取排程清單 {#retrieve-list}

您可以向 `/config/schedules` 端點。

**API格式**

此 `/config/schedules` 端點支援數個查詢參數，可協助篩選結果。 雖然這些參數為可選參數，但強烈建議使用這些參數，以幫助降低昂貴的開銷。 在沒有參數的情況下對此端點進行呼叫將檢索組織可用的所有計畫。 可包含多個參數，以&amp;符號分隔(`&`)。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{START}` | 指定偏移將從哪個頁面開始。 預設情況下，此值為0。 |
| `{LIMIT}` | 指定傳回的排程數。 依預設，此值為100。 |

**要求**

下列請求會擷取您組織中張貼的最後十個排程。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的排程清單顯示為JSON。

>[!NOTE]
>
>下列回應已因空間而截斷，且只顯示傳回的第一個排程。

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
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
| `children.name` | 排程的名稱為字串。 |
| `children.type` | 作為字串的作業類型。 支援的兩種類型為「batch_segmentation」和「export」。 |
| `children.properties` | 包含與排程相關的其他屬性的物件。 |
| `children.properties.segments` | 使用 `["*"]` 確保包含所有區段。 |
| `children.schedule` | 包含作業計畫的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 欲知關於cron時間表的更多資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 *」表示此排程將每天凌晨1:00執行。 |
| `children.state` | 包含排程狀態的字串。 兩個支援的狀態為「作用中」和「非作用中」。 依預設，狀態會設為「非使用中」。 |

## 建立新排程 {#create}

您可以向 `/config/schedules` 端點。

**API格式**

```http
POST /config/schedules
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **必填。** 排程的名稱為字串。 |
| `type` | **必填。** 作為字串的作業類型。 支援的兩種類型為「batch_segmentation」和「export」。 |
| `properties` | **必填。** 包含與排程相關的其他屬性的物件。 |
| `properties.segments` | **必要時機 `type` 等於「batch_segmentation」。** 使用 `["*"]` 確保包含所有區段。 |
| `schedule` | *選填.* 包含作業計畫的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 欲知關於cron時間表的更多資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 *」表示此排程將每天凌晨1:00執行。 <br><br>如果未提供此字串，將自動生成系統生成的調度。 |
| `state` | *選填.* 包含排程狀態的字串。 兩個支援的狀態為「作用中」和「非作用中」。 依預設，狀態會設為「非使用中」。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

## 擷取特定排程 {#get}

您可以向提出GET請求，以擷取特定排程的詳細資訊 `/config/schedules` 端點，並提供您要在請求路徑中擷取之排程的ID。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您要擷取之排程的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定排程的詳細資訊。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `name` | 排程的名稱為字串。 |
| `type` | 作為字串的作業類型。 支援的兩種類型為 `batch_segmentation` 和 `export`. |
| `properties` | 包含與排程相關的其他屬性的物件。 |
| `properties.segments` | 使用 `["*"]` 確保包含所有區段。 |
| `schedule` | 包含作業計畫的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 欲知關於cron時間表的更多資訊，請閱讀 [cron運算式格式](#appendix). 在此範例中，「0 0 1 *」表示此排程將每天凌晨1:00執行。 |
| `state` | 包含排程狀態的字串。 兩個支援的狀態為 `active` 和 `inactive`. 依預設，狀態會設為 `inactive`. |

## 更新特定排程的詳細資訊 {#update}

您可以向發出PATCH請求以更新特定排程 `/config/schedules` 端點，並提供您嘗試在請求路徑中更新之排程的ID。

PATCH請求可讓您更新 [state](#update-state) 或 [cron排程](#update-schedule) ，以取得個別排程。

### 更新計畫狀態 {#update-state}

您可以使用JSON修補程式操作來更新排程的狀態。 若要更新狀態，請宣告 `path` 屬性為 `/state` 並設定 `value` 為 `active` 或 `inactive`. 如需JSON修補程式的詳細資訊，請參閱 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 檔案。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的計畫的值。 |

**要求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | 要修補的值的路徑。 在此情況下，由於您要更新排程的狀態，因此必須設定 `path` 「/state」。 |
| `value` | 計畫狀態的更新值。 此值可設為「作用中」或「非作用中」，以啟用或停用排程。 請注意 **不能** 如果已啟用串流功能，請停用排程。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

### 更新cron排程 {#update-schedule}

您可以使用JSON修補程式操作來更新cron排程。 若要更新排程，請宣告 `path` 屬性為 `/schedule` 並設定 `value` 至有效的cron排程。 如需JSON修補程式的詳細資訊，請參閱 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 檔案。 欲知關於cron時間表的更多資訊，請閱讀 [cron運算式格式](#appendix).

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的計畫的值。 |

**要求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | 您要更新之值的路徑。 在此情況下，由於您要更新cron排程，因此需要設定 `path` to `/schedule`. |
| `value` | cron排程的更新值。 此值必須以cron排程的形式。 在此範例中，排程將在每個月的第二個執行。 |

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

## 刪除特定排程

您可以向提出DELETE請求，以請求刪除特定排程 `/config/schedules` 端點，並在請求路徑中提供您要刪除之排程的ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要刪除的排程值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）。

## 後續步驟

閱讀本指南後，您現在更了解排程的運作方式。

## 附錄 {#appendix}

下列附錄說明排程中使用的cron運算式格式。

### 格式

cron運算式是由6或7個欄位組成的字串。 運算式看起來會類似下列：

`0 0 12 * * ?`

在cron運算式字串中，第一個欄位代表秒，第二個欄位代表分鐘，第三個欄位代表小時，第四個欄位代表月的某天，第五個欄位代表月，第六個欄位代表一週的某天。 您也可以選擇加入代表年份的第七個欄位。

| 欄位名稱 | 必填 | 可能的值 | 允許的特殊字元 |
| ---------- | -------- | --------------- | -------------------------- |
| 秒 | 是 | 0-59 | `, - * /` |
| 分鐘 | 是 | 0-59 | `, - * /` |
| 小時 | 是 | 0-23 | `, - * /` |
| 當月日期 | 是 | 1-31 | `, - * ? / L W` |
| 月 | 是 | 1-12,1月12日 | `, - * /` |
| 週中的日 | 是 | 1-7, SUN-SAT | `, - * ? / L #` |
| 年 | 無 | 空，1970-2099年 | `, - * /` |

>[!NOTE]
>
>月份的名稱和一週中的天數 **not** 區分大小寫。 因此， `SUN` 等同於使用 `sun`.

允許的特殊字元代表下列意義：

| 特殊字元 | 說明 |
| ----------------- | ----------- |
| `*` | 此值用於選取 **all** 值。 例如，將 `*` 在「小時」欄位中 **ever** 小時。 |
| `?` | 此值表示不需要特定值。 這通常用於在一個欄位中指定允許字元的項目，但不能在另一個欄位中指定。 例如，如果您想要每月的3日觸發事件，但不關心一週的哪一天，您會放置 `3` 在「月」欄位的某天和 `?` 在「星期」欄位中。 |
| `-` | 此值用於指定 **包容性** 欄位的範圍。 例如，若您將 `9-15` 在「小時」欄位中，這表示小時將包括9、10、11、12、13、14和15。 |
| `,` | 此值可用來指定其他值。 例如，若您將 `MON, FRI, SAT` 在「星期」欄位中，這表示一週中的天數將包括星期一、星期五和星期六。 |
| `/` | 此值用於指定增量。 放在 `/` 決定其遞增的位置，而值放置在 `/` 決定增加的幅度。 例如，若您將 `1/7` 在「分鐘」欄位中，這表示分鐘將包括1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用於指定 `Last`，且具有不同的意義，視其使用的欄位而定。 若將其與「月日」欄位搭配使用，則代表該月的最後一天。 如果單獨將其與一週的某天欄位搭配使用，則代表一週的最後一天，即星期六(`SAT`)。 如果將其與一週中的某天欄位搭配使用，並搭配其他值，則代表該月該類型的最後一天。 例如，若您將 `5L` 在星期幾欄位中 **僅限** 包括當月最後一個星期五。 |
| `W` | 此值可用來指定與指定日最接近的工作日。 例如，若您將 `18W` 在「月的某天」欄位中，當月的18日是星期六，則會在17日（星期五）觸發，這是最接近的工作日。 如果當月18日是星期日，則會在19日的星期一觸發，這是最接近的工作日。 請注意，若您 `1W` 在「月」欄位的「天」中，最接近的工作日是在前一個月，事件仍會在的最接近工作日觸發 **電流** 月。</br></br>此外，您也可以 `L` 和 `W` 製作 `LW`，指定當月的最後一個工作日。 |
| `#` | 此值可用來指定一個月內的第n天。 放在 `#` 代表一週中的某天，而在 `#` 代表該月的哪個事件。 例如，若您將 `1#3`，則事件將於該月第三個星期日觸發。 請注意，若您 `X#5` 而該月中沒有第五次出現，該事件將 **not** 被觸發。 例如，若您將 `1#5`，而該月沒有第五個星期日，則活動會 **not** 被觸發。 |

### 範例

下表顯示cron運算式字串範例，並說明其含義。

| 運算式 | 解釋 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 每天下午1點會引發。 |
| `0 30 9 * * ? 2022` | 2022年每天早上9點30分開始。 |
| `0 * 18 * * ?` | 事件會每分鐘引發，從下午6點開始，到下午6:59結束，每天。 |
| `0 0/10 17 * * ?` | 每10分鐘引發一次，從下午5點開始，到下午6點結束。 |
| `0 13,38 5 ? 6 WED` | 該活動將於6月每週三早5時13分和早5時38分引發。 |
| `0 30 12 ? * 4#3` | 活動將於每月第三個星期三中午12點30分開始。 |
| `0 30 12 ? * 6L` | 事件將在每月最後一個星期五的中午12點30分引發。 |
| `0 45 11 ? * MON-THU` | 活動將於每週一、二、三、四的上午11:45引發。 |