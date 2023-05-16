---
description: 了解如何格式化API呼叫，以透過Adobe Experience Platform Destination SDK提交目的地發佈請求。
title: 建立目標發佈請求
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# 建立目標發佈請求

>[!IMPORTANT]
>
>如果您要提交要供其他Experience Platform客戶使用的已分產品化（公開）目的地，則只需使用此API端點。 如果您要建立私人目的地供自己使用，則不需使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試您的目的地後，您就可以將其提交至Adobe以進行審核和發佈。 閱讀 [提交以審核在Destination SDK中創作的目標](../guides/submit-destination.md) 在目標提交程式中，您必須執行的所有其他步驟。

符合下列情形時，請使用發佈目標API端點提交發佈請求：

* 作為Destination SDK合作夥伴，您希望讓所有Experience Platform組織都能提供產品化目的地，供所有Experience Platform客戶使用；
* 你讓 *任何更新* 設定。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 目的地發佈API作業快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 提交要發佈的目標配置 {#create}

您可以向提交POST請求，以提交要發佈的目標設定 `/authoring/destinations/publish` 端點。

**API格式**

```http
POST /authoring/destinations/publish
```

+++請求

下列要求會提交要發佈的目的地，涵蓋由裝載中提供的參數所設定的組織。 以下裝載包含接受的所有參數 `/authoring/destinations/publish` 端點。

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
| `destinationId` | 字串 | 您要提交以進行發佈的目的地設定的目的地ID。 使用 [檢索目標配置](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API呼叫。 |
| `destinationAccess` | 字串 | 使用 `ALL` 讓您的目的地出現在所有Experience Platform客戶的目錄中。 |

{style="table-layout:auto"}

+++回應

成功的回應會傳回HTTP狀態201，並包含目的地發佈請求的詳細資訊。

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何提交目的地的發佈請求。 Adobe Experience Platform團隊將檢閱您的發佈請求，並在5個工作天內回覆給您。