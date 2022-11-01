---
title: 配額API端點
description: 資料衛生API中的/quota端點可讓您根據組織對每種作業類型的每月配額限制來監控資料衛生使用量。
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# 配額終結點

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**.

此 `/quota` 資料衛生API中的端點可讓您根據組織對每個作業類型的配額限制來監控資料衛生使用情況。

對每個資料衛生作業類型執行配額的方式如下：

* 消費者每月的刪除和欄位更新僅限於特定數量的請求。
* 資料集有效期對同時作用中作業的數量有固定限制，無論有效期的執行時間為何。

## 快速入門

本指南中使用的端點是資料衛生API的一部分。 繼續之前，請檢閱 [概述](./overview.md) 以取得下列資訊：

* 相關檔案的連結
* 本檔案中讀取範例API呼叫的指南
* 成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊

## 清單配額 {#list}

您可以向 `/quota` 端點。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{QUOTA_TYPE}` | 一個可選查詢參數，它指定要檢索的配額類型。 若否 `quotaType` 參數時，API回應會傳回所有配額值。 接受的類型值包括：<ul><li>`expirationDatasetQuota`:資料集有效期</li><li>`deleteIdentityWorkOrderDatasetQuota`:消費者刪除</li><li>`fieldUpdateWorkOrderDatasetQuota`:欄位更新</li></ul> |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**回應**

成功的響應返回資料衛生配額的詳細資訊。

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `quotas` | 列出每個資料衛生作業類型的配額資訊。 每個配額對象包含以下屬性：<ul><li>`name`:資料衛生作業類型：<ul><li>`expirationDatasetQuota`:資料集有效期</li><li>`deleteIdentityWorkOrderDatasetQuota`:消費者刪除</li></ul></li><li>`description`:資料衛生作業類型的說明。</li><li>`consumed`:此類型的作業數在當前每月期間運行。</li><li>`quota`:此作業類型的配額限制。 對於消費者的刪除和欄位更新，這代表每月可執行的工作數量。 對於資料集過期時間，這代表可在任何指定時間同時作用的工作數量。</li></ul> |

{style=&quot;table-layout:auto&quot;}
