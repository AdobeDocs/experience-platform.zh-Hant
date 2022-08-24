---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；調度；api;API;
solution: Experience Platform
title: 計畫API終結點
topic-legacy: developer guide
description: 計畫是一種工具，可用於每天自動運行一次批分段作業。
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 84026b447eea00955bc9e6482b81ae1aad3c312e
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 3%

---

# 計畫終結點

計畫是一種工具，可用於每天自動運行一次批分段作業。 您可以使用 `/config/schedules` 終結點：檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 檢索計劃清單 {#retrieve-list}

您可以通過向以下站點發出GET請求來檢索組織的所有計劃清單 `/config/schedules` 端點。

**API格式**

的 `/config/schedules` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們以幫助降低昂貴的開銷。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有計畫。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{START}` | 指定偏移將從哪個頁開始。 預設情況下，此值為0。 |
| `{LIMIT}` | 指定返回的計畫數。 預設情況下，此值為100。 |

**要求**

以下請求將檢索您組織中過帳的最後十個計畫。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中列出了指定IMS組織的調度清單(JSON)。

>[!NOTE]
>
>以下響應已被截斷，只顯示返回的第一個計畫。

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
| `_page.totalCount` | 返回的計畫總數。 |
| `_page.pageSize` | 計畫頁的大小。 |
| `children.name` | 調度的字串名稱。 |
| `children.type` | 作業的字串類型。 支援的兩種類型是&quot;batch_segmentation&quot;和&quot;export&quot;。 |
| `children.properties` | 包含與計畫相關的其他屬性的對象。 |
| `children.properties.segments` | 使用 `["*"]` 確保包括所有段。 |
| `children.schedule` | 包含作業計畫的字串。 作業只能計畫為每天運行一次，這意味著您不能計畫在24小時內運行多次作業。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](#appendix)。 在本示例中，「0 0 1 * *」表示此計畫將在每天上午1點運行。 |
| `children.state` | 包含調度狀態的字串。 支援的兩個狀態是「活動」和「非活動」。 預設情況下，狀態設定為「非活動」。 |

## 建立新計畫 {#create}

您可以通過向POST `/config/schedules` 端點。

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
| `name` | **必填。** 調度的字串名稱。 |
| `type` | **必填。** 作業的字串類型。 支援的兩種類型是&quot;batch_segmentation&quot;和&quot;export&quot;。 |
| `properties` | **必填。** 包含與計畫相關的其他屬性的對象。 |
| `properties.segments` | **在 `type` 等於&quot;batch_segmentation&quot;。** 使用 `["*"]` 確保包括所有段。 |
| `schedule` | *選填.* 包含作業計畫的字串。 作業只能計畫為每天運行一次，這意味著您不能計畫在24小時內運行多次作業。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](#appendix)。 在本示例中，「0 0 1 * *」表示此計畫將在每天上午1點運行。 <br><br>如果未提供此字串，則系統生成的調度將自動生成。 |
| `state` | *選填.* 包含調度狀態的字串。 支援的兩個狀態是「活動」和「非活動」。 預設情況下，狀態設定為「非活動」。 |

**回應**

成功的響應返回HTTP狀態200，其中包含您新建立的計畫的詳細資訊。

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

## 檢索特定計畫 {#get}

您可以通過向以下站點發出GET請求來檢索有關特定計畫的詳細資訊 `/config/schedules` 端點，並提供要在請求路徑中檢索的計畫的ID。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要檢索的計畫的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定計畫的詳細資訊。

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
| `name` | 調度的字串名稱。 |
| `type` | 作業的字串類型。 支援的兩種類型為 `batch_segmentation` 和 `export`。 |
| `properties` | 包含與計畫相關的其他屬性的對象。 |
| `properties.segments` | 使用 `["*"]` 確保包括所有段。 |
| `schedule` | 包含作業計畫的字串。 作業只能計畫為每天運行一次，這意味著您不能計畫在24小時內運行多次作業。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](#appendix)。 在本示例中，「0 0 1 * *」表示此計畫將在每天上午1點運行。 |
| `state` | 包含調度狀態的字串。 兩個支援的狀態是 `active` 和 `inactive`。 預設情況下，狀態設定為 `inactive`。 |

## 更新特定計畫的詳細資訊 {#update}

您可以通過向以下站點發出PATCH請求來更新特定計畫 `/config/schedules` 終結點，並提供您嘗試在請求路徑中更新的計畫的ID。

PATCH請求允許您更新 [狀態](#update-state) 或 [cron計畫](#update-schedule) 來確定。

### 更新計畫狀態 {#update-state}

可以使用JSON修補程式操作更新計畫的狀態。 要更新狀態，請聲明 `path` 屬性 `/state` 並設定 `value` 或 `active` 或 `inactive`。 有關JSON修補程式的詳細資訊，請閱讀 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 文檔。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要更新的計畫的值。 |

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
| `path` | 要修補的值的路徑。 在這種情況下，由於您正在更新計畫的狀態，因此需要設定 `path` 到「/state」。 |
| `value` | 計畫狀態的更新值。 此值可以設定為「活動」或「非活動」以激活或停用調度。 請注意 **不能** 如果IMS組織已啟用流式處理，則禁用調度。 |

**回應**

成功的響應返回HTTP狀態204（無內容）。

### 更新cron計畫 {#update-schedule}

可以使用JSON修補程式操作更新cron計畫。 要更新計畫，請聲明 `path` 屬性 `/schedule` 並設定 `value` 到有效的cron計畫。 有關JSON修補程式的詳細資訊，請閱讀 [JSON修補程式](https://datatracker.ietf.org/doc/html/rfc6902) 文檔。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](#appendix)。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要更新的計畫的值。 |

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
| `path` | 要更新的值的路徑。 在這種情況下，由於您正在更新cron計畫，因此需要設定 `path` 至 `/schedule`。 |
| `value` | cron計畫的更新值。 此值需要以cron計畫的形式出現。 在此示例中，計畫將在每月的第二天運行。 |

**回應**

成功的響應返回HTTP狀態204（無內容）。

## 刪除特定計畫

您可以請求刪除特定計畫，方法是向 `/config/schedules` 端點，並提供您希望在請求路徑中刪除的計畫的ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要刪除的計畫的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204（無內容）。

## 後續步驟

閱讀本指南後，您現在對時間表的工作原理有了更好的瞭解。

## 附錄 {#appendix}

下面的附錄說明了計畫中使用的cron表達式的格式。

### 格式

cron表達式是由6或7個欄位組成的字串。 表達式的外觀與以下內容類似：

`0 0 12 * * ?`

在cron表達式字串中，第一個欄位表示秒，第二個欄位表示分鐘，第三個欄位表示小時，第四個欄位表示月的日，第五個欄位表示月，第六個欄位表示周的日。 您還可以選擇包括表示年份的第七個欄位。

| 欄位名稱 | 必填 | 可能的值 | 允許的特殊字元 |
| ---------- | -------- | --------------- | -------------------------- |
| 秒 | 是 | 0-59 | `, - * /` |
| 分鐘 | 是 | 0-59 | `, - * /` |
| 小時 | 是 | 0-23 | `, - * /` |
| 當月日期 | 是 | 1-31 | `, - * ? / L W` |
| 月 | 是 | 1-12,1-12 | `, - * /` |
| 週中的日 | 是 | 1-7,SUN-SAT | `, - * ? / L #` |
| 年 | 無 | 空，1970-2099 | `, - * /` |

>[!NOTE]
>
>月份的名稱和星期的名稱 **不** 區分大小寫。 所以， `SUN` 等於使用 `sun`。

允許的特殊字元表示以下含義：

| 特殊字元 | 說明 |
| ----------------- | ----------- |
| `*` | 此值用於選擇 **全部** 欄位中的值。 比如說， `*` 在小時數字表示 **每** 小時。 |
| `?` | 此值表示不需要特定值。 這通常用於在允許字元的一個欄位中指定某個內容，但不能在另一個欄位中指定它。 例如，如果您希望每月3日觸發一個事件，但不關心該事件是星期幾，則將 `3` 在月的日欄位和 `?` 在「星期」欄位中。 |
| `-` | 此值用於指定 **包容** 欄位的範圍。 例如，如果 `9-15` 在「小時數」欄位中，這表示「小時數」將包括9、10、11、12、13、14和15。 |
| `,` | 此值用於指定附加值。 例如，如果 `MON, FRI, SAT` 在星期日欄位中，這表示星期日包括星期一、星期五和星期六。 |
| `/` | 此值用於指定增量。 放在 `/` 確定其從的增量位置，同時在 `/` 確定它的增量。 例如，如果 `1/7` 在「分鐘」欄位中，這表示分鐘將包括1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用於指定 `Last`，並且根據所使用的欄位具有不同的含義。 如果它與月的日欄位一起使用，則它表示月的最後一天。 如果它單獨與星期日欄位一起使用，則它表示星期末的星期六（星期六）`SAT`)。 如果它與星期欄位的日期一起使用，並與另一個值一起使用，則它表示該月的該類型的最後一天。 例如，如果 `5L` 在星期一的田裡 **僅** 包括本月最後一個星期五。 |
| `W` | 此值用於指定與給定日期最接近的工作日。 例如，如果 `18W` 在月日欄位中，當月18號是星期六，它將在17號星期五觸發，這是最接近的工作日。 如果當月18號是星期天，那麼將在19號星期一觸發，這是最接近的工作日。 請注意，如果 `1W` 在「月的日」欄位中，最近的工作日將位於上個月，但活動仍將在最近的工作日觸發 **當前** 月。</br></br>另外，您可以 `L` 和 `W` 要 `LW`，它將指定月的最後一個工作日。 |
| `#` | 此值用於指定一個月中一週的第n天。 放在 `#` 表示星期中的某一天，而放置在 `#` 表示該月中發生的事件。 例如，如果 `1#3`，該事件將在當月三號觸發。 請注意，如果 `X#5` 並且該月的該天沒有第五次發生，該事件將 **不** 觸發。 例如，如果 `1#5`，而那個月沒有第五個星期日，這個活動 **不** 觸發。 |

### 範例

下表顯示了cron表達式字串示例，並說明它們的含義。

| 運算式 | 解釋 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 活動將於每天下午1點開始。 |
| `0 30 9 * * ? 2022` | 該活動將於2022年每天上午9時30分開火。 |
| `0 * 18 * * ?` | 活動將每分鐘發射一次，從下午6點開始，到每天下午6點59分結束。 |
| `0 0/10 17 * * ?` | 該活動每10分鐘發一次火，從下午5點開始，到下午6點結束，每天。 |
| `0 13,38 5 ? 6 WED` | 活動將於6月每週三早5時13分和5時38分開火。 |
| `0 30 12 ? * 4#3` | 活動將在每月的第三個星期三下午12點30分開火。 |
| `0 30 12 ? * 6L` | 活動將在每月最後一個星期五的下午12點30分開火。 |
| `0 45 11 ? * MON-THU` | 活動將於每週一、二、三、四的上午11:45發射。 |