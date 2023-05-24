---
description: 本頁說明了用於通過Adobe Experience Platform Destination SDK刪除現有目標伺服器配置的API調用。
title: 刪除目標伺服器配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# 刪除目標伺服器配置

本頁說明了API請求和負載，您可以使用 `/authoring/destination-servers` API終結點。

有關可以通過此端點刪除的權能的詳細說明，請閱讀以下文章：

* [使用Destination SDK建立的目標的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立的目標的模板規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式配置](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標伺服器API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 刪除目標伺服器配置 {#delete}

可以刪除 [現有](create-destination-server.md) 通過建立目標伺服器配置 `DELETE` 請求 `/authoring/destination-servers` 端點 `{INSTANCE_ID}`要刪除的目標伺服器配置。

>[!TIP]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

獲取現有目標伺服器配置及其相應配置 `{INSTANCE_ID}`，請參閱有關 [檢索目標伺服器配置](retrieve-destination-server.md)。

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `ID` 目標伺服器配置。 |

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++回應

成功的響應返回HTTP狀態200以及空的HTTP響應。

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何通過Destination SDK刪除現有目標伺服器 `/authoring/destination-servers` API終結點。

要瞭解有關可以使用此端點執行什麼操作的詳細資訊，請參閱以下文章：

* [建立目標伺服器配置](create-destination-server.md)
* [檢索目標伺服器配置](retrieve-destination-server.md)
* [更新目標伺服器配置](update-destination-server.md)

