---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK刪除現有對象範本的API呼叫範例。
title: 刪除對象範本
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# 刪除對象範本

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

此頁面以範例說明可用來刪除對象範本的API請求和裝載，使用 `/authoring/audience-templates` api端點。

如需可透過此端點設定的功能的詳細說明，請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 對象範本API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需您成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除對象範本 {#delete}

您可以刪除 [現有](create-audience-template.md) 對象範本，做法是 `DELETE` 要求給 `/authoring/audience-templates` 端點與 `{INSTANCE_ID}`要刪除之對象範本的URL編號。

若要取得現有的對象範本及其對應的 `{INSTANCE_ID}`，請參閱「 」一文，瞭解 [擷取對象範本](retrieve-audience-template.md).

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除之對象範本的URL。 |

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

成功的回應會傳回HTTP狀態200以及空的HTTP回應。

+++

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/audience-templates` api端點。 讀取 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
