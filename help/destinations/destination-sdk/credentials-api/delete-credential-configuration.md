---
description: 本頁說明了用於刪除憑據配置Adobe Experience Platform Destination SDK的API調用。
title: 刪除憑據配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 刪除憑據配置

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/credentials`

本頁說明了API請求和負載，您可以使用 `/authoring/credentials` API終結點。

## 何時使用 `/credentials` API終結點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，你 ***不*** 需要使用 `/credentials` API終結點。 相反，您可以通過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。
> 
>閱讀 [客戶身份驗證配置](../functionality/destination-configuration/customer-authentication.md) 的子菜單。

僅當Adobe與目標平台之間存在全局身份驗證系統時，才使用此API終結點建立憑據配置， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 `/credentials` API終結點。

使用全局身份驗證系統時，必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 的 [目標傳遞](../functionality/destination-configuration/destination-delivery.md) 配置，當 [建立新目標配置](../authoring-api/destination-configuration/create-destination-configuration.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 憑據API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 刪除憑據配置 {#delete}

可以刪除 [現有](create-credential-configuration.md) 通過建立 `DELETE` 請求 `/authoring/credentials` 端點 `{INSTANCE_ID}`刪除的憑據配置。

獲取現有目標配置及其相應的 `{INSTANCE_ID}`，請參閱有關 [檢索憑據配置](retrieve-credential-configuration.md)。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `ID` 刪除的憑據配置。 |

以下請求刪除由 `{INSTANCE_ID}` 的下界。

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

閱讀此文檔後，您現在知道如何使用 `/authoring/credentials` API終結點。 閱讀 [如何使用Destination SDK配置目標](../guides/configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
