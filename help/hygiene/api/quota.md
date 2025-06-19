---
title: 配額API端點
description: 資料衛生API中的/quota端點可讓您根據貴組織每個工作型別的每月配額限制，監控進階資料生命週期管理的使用情況。
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 配額端點

資料衛生API中的`/quota`端點可讓您根據貴組織每種工作型別的配額限制，監控進階資料生命週期管理的使用情況。

會追蹤每個資料生命週期工作型別的配額使用量。 您的實際配額限制取決於貴組織的權益，並可定期審查。 資料集過期時間受同時作用中工作數量的嚴格限制。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱[總覽](./overview.md)以取得下列資訊：

* 相關檔案的連結
* 閱讀本檔案中範例API呼叫的指南
* 關於呼叫任何Experience Platform API所需標題的重要資訊

## 配額與處理時間表 {#quotas}

記錄刪除請求受配額和服務層級預期的約束，這些預期取決於您的授權權利。 這些限制同時適用於UI和API型刪除請求。

>[!TIP]
> 
>本檔案說明如何根據軟體權利檔案限制查詢您的使用情況。 如需配額層、記錄刪除許可權和SLA行為的完整說明，請參閱[UI型記錄刪除](../ui/record-delete.md#quotas)或[API型記錄刪除](./workorder.md#quotas)檔案。

## 清單配額 {#list}

您可以透過向`/quota`端點發出GET要求來檢視您組織的配額資訊。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{QUOTA_TYPE}` | 選擇性查詢引數，指定要擷取的配額型別。 如果未提供`quotaType`引數，則API回應中會傳回所有配額值。 接受的型別值包括：<ul><li>`datasetExpirationQuota`：此物件顯示貴組織同時作用中的資料集到期數目，以及您的到期總允許。 </li><li>`dailyConsumerDeleteIdentitiesQuota`：此物件顯示貴組織今天提出的記錄刪除請求總數，以及您的每日津貼總額。<br>注意：僅計算已接受的請求。 如果工單因驗證失敗而被拒絕，這些身分刪除不會計入您的配額。</li><li>`monthlyConsumerDeleteIdentitiesQuota`：此物件顯示貴組織本月提出的記錄刪除請求總數，以及您的每月津貼總額。</li><li>`monthlyUpdatedFieldIdentitiesQuota`：此物件顯示貴組織本月提出的記錄更新要求總數，以及您的每月津貼總額。</li></ul> |

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

成功的回應會傳回資料生命週期配額的詳細資料。

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| 屬性 | 說明 |
| -------- | ------- |
| `quotas` | 列出每個資料生命週期工作型別的配額資訊。 每個配額物件都包含下列屬性：<ul><li>`name`：資料生命週期工作型別：<ul><li>`expirationDatasetQuota`：資料集有效期</li><li>`deleteIdentityWorkOrderDatasetQuota`：記錄刪除</li></ul></li><li>`description`：資料生命週期工作型別的說明。</li><li>`consumed`：此型別在目前期間執行的作業數目。 物件名稱表示配額期間。</li><li>`quota`：貴組織此工作型別的配額。 對於記錄刪除和更新，配額表示每個月期間可以執行的工作數量。 對於資料集有效期，配額代表可以在任何指定時間同時作用的工作數量。</li></ul> |
