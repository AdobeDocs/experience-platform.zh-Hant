---
title: 審核事件導出API終結點
description: 瞭解如何使用審計查詢API導出Experience Platform中的審計事件。
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# 導出審計事件清單

可通過向Web站點發出GET請求來檢索事件資料 `/audit/export` 端點，指定要在負載中檢索的事件。

**API格式**

```http
GET /audit/export
```

| 參數 | 說明 |
| --------- | ----------- |
| `timestamp` | 按時間戳篩選時，最好使用>和&lt;運算子，而不是使用精確值。 <br/>範例: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | 操作的狀態。 狀態可以是以下任一狀態： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>範例: `?property=status==Deny`. |
| `action` | 為事件記錄的操作類型。 操作可以是下列任一操作： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> 範例：`?property=action==Create`。 |
| `user` | 執行該事件的用戶。 |
| `assetType` | 對執行操作的平台資源類型。 <br/>範例: `?property=assetType==<an asset type>`. |

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

結果將生成CSV檔案以供導出。 成功的響應返回沒有響應正文的HTTP 307。 中提供了指嚮導出檔案的連結 `Location` 響應標頭。
