---
keywords: Experience Platform；首頁；熱門主題；流式服務；刪除目標帳戶；delete;api
solution: Experience Platform
title: 使用流服務API刪除目標帳戶
type: Tutorial
description: 瞭解如何使用流服務API刪除目標帳戶。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 使用流服務API刪除目標帳戶

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

在激活資料之前，您需要先設定目標帳戶以連接到目標。 本教程介紹使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

>[!NOTE]
>
>當前僅在流服務API中支援刪除目標帳戶。 無法使用Experience PlatformUI刪除目標帳戶。

## 快速入門 {#get-started}

本教程要求您具有有效的連接ID。 連接ID表示到目標的帳戶連接。 如果您沒有有效的連接ID，請從 [目標目錄](../catalog/overview.md) 並按照 [連接到目標](../ui/connect-destination.md) 在嘗試本教程之前。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [目標](../home.md): [!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 讀取示例API調用 {#reading-sample-api-calls}

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值 {#gather-values-for-required-headers}

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 未指定標頭，請求在 `prod` 沙盒。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* `Content-Type: application/json`

## 查找要刪除的目標帳戶的連接ID {#find-connection-id}

>[!NOTE]
>本教程使用 [飛艇目的地](../catalog/mobile-engagement/airship-attributes.md) 作為示例，但所概述的步驟適用於 [可用目標](../catalog/overview.md)。

刪除目標帳戶的第一步是找出與要刪除的目標帳戶對應的連接ID。

在Experience PlatformUI中，瀏覽到 **[!UICONTROL 目標]** > **[!UICONTROL 帳戶]** 並通過選擇 **[!UICONTROL 目標]** 的雙曲餘切值。

![選擇要刪除的目標帳戶](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

接下來，您可以從瀏覽器中的URL檢索目標帳戶的連接ID。

![從URL檢索連接ID](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## 刪除連接 {#delete-connection}

>[!IMPORTANT]
>
>在刪除目標帳戶之前，必須刪除目標帳戶的任何現有資料流。
>要刪除現有資料流，請參閱以下頁：
>* [使用Experience PlatformUI](../ui/delete-destinations.md) 刪除現有資料流；
>* [使用流服務API](delete-destination-dataflow.md) 刪除現有資料流。


一旦您擁有連接ID並確保目標帳戶不存在任何資料流，請向 [!DNL Flow Service] API。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 獨特 `id` 要刪除的連接的值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。 您可以通過嘗試查找(GET)連接請求來確認刪除。 API將返回HTTP 404（未找到）錯誤，表示目標帳戶已被刪除。

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

按照本教程，您已成功使用 [!DNL Flow Service] 用於刪除現有目標帳戶的API。 有關使用目標的詳細資訊，請參閱 [目標概述](/help/destinations/home.md)。