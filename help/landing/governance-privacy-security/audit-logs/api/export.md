---
title: 稽核事件匯出API端點
description: 了解如何使用稽核查詢API匯出Experience Platform中的稽核事件。
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# 匯出稽核事件清單

您可以向 `/audit/export` 端點，指定您要在裝載中擷取的事件。

**API格式**

```http
GET /audit/export
```

| 參數 | 說明 |
| --------- | ----------- |
| `timestamp` | 依時間戳記篩選時，最佳作法是使用>和&lt;運算子的範圍，而非確切值。 <br/>範例：?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48.610862Z。 |
| `status` | 動作的狀態。 狀態可以是下列任一項： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | 為事件記錄的動作類型。 動作可以是下列任一項： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | 執行事件的使用者。 |
| `assetType` | 執行動作的平台資源類型。 |

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

結果會產生為CSV檔案以供匯出。 成功的回應會傳回HTTP 307，但沒有回應內文。 匯出檔案的連結會提供於 `Location` 回應標題。
