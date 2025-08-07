---
title: 配額API端點
description: 資料衛生API中的/quota端點可讓您根據貴組織每個工作型別的每月配額限制，監控進階資料生命週期管理的使用情況。
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# 配額端點

使用資料衛生API中的`/quota`端點來檢查您組織目前的使用情況和限制。 配額依權利而異，例如Privacy and Security Shield或Healthcare Shield。

監視您目前的配額消耗，以確保符合每個工作型別的組織限制。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱[總覽](./overview.md)以取得下列資訊：

* 相關檔案連結
* 如何讀取範例API呼叫
* Experience Platform API呼叫的必要標頭

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

>[!NOTE]
>
>配額消耗會在每個月1日的00:00 GMT重設每日和每月。
>
>只有接受的請求才會計入您的配額。 拒絕的工作單不會減少您的配額。

| 參數 | 說明 |
| --- | --- |
| `{QUOTA_TYPE}` | 選擇性查詢引數，指定要擷取的配額型別。 如果未提供`quotaType`引數，則API回應中會傳回所有配額值。 接受的值包括：<ul><li>`datasetExpirationQuota`：使用中資料集到期日數目以及您的總允許。</li><li>`dailyConsumerDeleteIdentitiesQuota`：今天刪除的記錄數目以及您的每日配額。</li><li>`monthlyConsumerDeleteIdentitiesQuota`：本月刪除的記錄數與您的每月配額。</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| 屬性 | 說明 |
| -------- | ------- |
| `quotas` | 列出每個資料生命週期工作型別的配額資訊。 每個配額物件都包含下列屬性：<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | 配額型別識別碼。 |
| `description` | 此配額限制內容的說明。 |
| `consumed` | 目前使用的配額量。 使用量會在當月1日的00:00 GMT和00:00 GMT重設每日配額。 |
| `quota` | 貴組織此配額型別的最大配額。 |
