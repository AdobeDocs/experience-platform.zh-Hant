---
title: 配額API終結點
description: 資料衛生API中的/quota終結點允許您根據組織針對每種作業類型的每月配額限制來監視資料衛生使用情況。
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 配額終結點

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買資料的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**。

的 `/quota` 資料衛生API中的終結點允許您根據組織針對每種作業類型的配額限制來監視資料衛生使用情況。

對每個資料衛生作業類型強制使用配額，方法如下：

* 記錄刪除和更新限制在每月的特定數量的請求。
* 資料集過期對併發活動作業的數量具有統一限制，而不管何時執行過期。

## 快速入門

本指南中使用的終結點是資料衛生API的一部分。 在繼續之前，請查看 [概述](./overview.md) 的子菜單。

* 指向相關文檔的連結
* 閱讀本文檔中示例API調用的指南
* 有關成功調用任何Experience PlatformAPI所需標頭的重要資訊

## 列出配額 {#list}

您可以通過向以下站點發出GET請求來查看組織的配額資訊 `/quota` 端點。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{QUOTA_TYPE}` | 指定要檢索的配額類型的可選查詢參數。 否 `quotaType` 提供參數，在API響應中返回所有配額值。 接受的類型值包括：<ul><li>`expirationDatasetQuota`:資料集過期</li><li>`deleteIdentityWorkOrderDatasetQuota`:記錄刪除</li><li>`fieldUpdateWorkOrderDatasetQuota`:記錄更新</li></ul> |

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

成功的響應將返回資料衛生配額的詳細資訊。

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
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `quotas` | 列出每個資料衛生作業類型的配額資訊。 每個配額對象都包含以下屬性：<ul><li>`name`:資料衛生作業類型：<ul><li>`expirationDatasetQuota`:資料集過期</li><li>`deleteIdentityWorkOrderDatasetQuota`:記錄刪除</li></ul></li><li>`description`:資料衛生作業類型的說明。</li><li>`consumed`:在當前每月期間運行的此類型作業數。</li><li>`quota`:此作業類型的配額限制。 對於記錄刪除和更新，這表示每個月期間可以運行的作業數。 對於資料集過期，這表示在任何給定時間可以同時處於活動狀態的作業數。</li></ul> |

{style="table-layout:auto"}
