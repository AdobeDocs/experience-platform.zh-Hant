---
description: 本頁說明了用於通過Adobe Experience Platform Destination SDK刪除現有受眾模板的API調用。
title: 刪除受眾模板
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# 刪除受眾模板

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

本頁說明了API請求和負載，您可以使用 `/authoring/audience-templates` API終結點。

有關可以通過此終結點配置的功能的詳細說明，請參見 [受眾元資料管理](../functionality/audience-metadata-management.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 受眾模板API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 刪除受眾模板 {#delete}

可以刪除 [現有](create-audience-template.md) 通過建立 `DELETE` 請求 `/authoring/audience-templates` 端點 `{INSTANCE_ID}`的子菜單。

獲取現有受眾模板及其相應模板 `{INSTANCE_ID}`，請參閱有關 [檢索受眾模板](retrieve-audience-template.md)。

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `ID` 的子菜單。 |

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的響應返回HTTP狀態200以及空的HTTP響應。

+++

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何使用 `/authoring/audience-templates` API終結點。 閱讀 [如何使用Destination SDK配置目標](../guides/configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
