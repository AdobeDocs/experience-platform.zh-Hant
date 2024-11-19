---
title: 稽核事件匯出API端點
description: 瞭解如何使用稽核查詢API以Experience Platform匯出稽核事件。
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# 匯出稽核事件清單

您可以向`/audit/export`端點發出GET要求，指定您要在承載中擷取的事件，以擷取事件資料。

**API格式**

```http
GET /audit/export
```

| 參數 | 說明 |
| --------- | ----------- |
| `timestamp` | 依時間戳記進行篩選時，最佳做法是使用>和&lt;運運算元來使用範圍，而不是使用確切的值。 <br/>範例： `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`。 |
| `status` | 動作的狀態。 狀態可以是下列任一專案： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>範例： `?property=status==Deny`。 |
| `action` | 為事件記錄的動作型別。 動作可以是下列任一專案： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> 範例：`?property=action==Create`。 |
| `user` | 執行事件的使用者。 |
| `assetType` | 執行動作的Platform資源型別。 <br/>範例： `?property=assetType==<an asset type>`。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**回應**

結果會產生CSV檔案以供匯出。 成功的回應會傳回HTTP 307，但沒有回應內文。 `Location`回應標頭中提供匯出檔案的連結。
