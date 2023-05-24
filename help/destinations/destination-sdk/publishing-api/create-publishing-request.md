---
description: 瞭解如何格式化API調用以通過Adobe Experience Platform Destination SDK提交目標發佈請求。
title: 建立目標發佈請求
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# 建立目標發佈請求

>[!IMPORTANT]
>
>只有在提交要供其他Experience Platform客戶使用的產品化（公共）目標時，才需要使用此API終結點。 如果您正在建立專用目標供自己使用，則無需使用發佈API正式提交目標。

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置和測試目標後，您可以將其提交給Adobe以進行審閱和發佈。 閱讀 [提交以審閱在Destination SDK中創作的目標](../guides/submit-destination.md) 對於作為目標提交流程的一部分必須執行的所有其他步驟。

在以下情況下，使用發佈目標API終結點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望使所有Experience Platform組織中的產品化目標都可用於所有Experience Platform客戶；
* 你 *任何更新* 配置。 配置更新僅在您提交新發佈請求後才反映在目標中，新發佈請求已獲得Experience Platform團隊的批准。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標發佈API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 提交要發佈的目標配置 {#create}

通過向發佈伺服器發出POST請求，可以提交要發佈的目標配置 `/authoring/destinations/publish` 端點。

**API格式**

```http
POST /authoring/destinations/publish
```

+++請求

以下請求將提交一個目標，以便跨由負載中提供的參數配置的組織發佈。 下面的負載包括接受的所有參數 `/authoring/destinations/publish` 端點。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 要提交以發佈的目標配置的目標ID。 使用 [檢索目標配置](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API調用。 |
| `destinationAccess` | 字串 | 使用 `ALL` 目標在所有Experience Platform客戶的目錄中。 |

{style="table-layout:auto"}

+++回應

成功的響應返回HTTP狀態201，其中包含目標發佈請求的詳細資訊。

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何提交目標的發佈請求。 Adobe Experience Platform團隊將審閱您的發佈請求，並在5個工作日後回復您。