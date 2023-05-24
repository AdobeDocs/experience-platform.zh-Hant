---
keywords: Experience Platform；首頁；熱門主題；流服務；API;api;delete;delete目標資料流
solution: Experience Platform
title: 使用流服務API刪除目標資料流
type: Tutorial
description: 瞭解如何使用流服務API將資料流刪除到批處理和流式處理目標。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 使用流服務API刪除目標資料流

您可以使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

本教程介紹使用以下步驟將資料流刪除到批處理和流式處理目標 [!DNL Flow Service]。

## 快速入門 {#get-started}

本教程要求您具有有效的流ID。 如果沒有有效的流ID，請從 [目標目錄](../catalog/overview.md) 並按照 [連接到目標](../ui/connect-destination.md) 和 [激活資料](../ui/activation-overview.md) 在嘗試本教程之前。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [目標](../home.md): [!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

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

## 刪除目標資料流 {#delete-destination-dataflow}

使用現有流ID，可以通過執行DELETE請求刪除目標資料流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 獨特 `id` 要刪除的目標資料流的值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態202（無內容）和空白正文。 您可以通過嘗試對資料流進行查找(GET)請求來確認刪除。 API將返回HTTP 404（未找到）錯誤，表示資料流已被刪除。

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) 有關解釋錯誤響應的詳細資訊，請參閱「Platform troubleshooting guide（平台故障排除指南）」。

## 後續步驟 {#next-steps}

按照本教程，您已成功使用 [!DNL Flow Service] 將現有資料流刪除到目標的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱上的教程 [刪除UI中的資料流](../ui/delete-destinations.md)。

你現在可以繼續 [刪除目標帳戶](/help/destinations/api/delete-destination-account.md) 使用 [!DNL Flow Service] API。
