---
keywords: Experience Platform；首頁；熱門主題；流程服務；API;API；刪除；刪除目標資料流
solution: Experience Platform
title: 使用流服務API刪除目標資料流
type: Tutorial
description: 了解如何使用流量服務API將資料流刪除到批處理和流目的地。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 使用流服務API刪除目標資料流

您可以刪除包含錯誤或已使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教學課程涵蓋使用將資料流同時刪除至批次和串流目的地的步驟 [!DNL Flow Service].

## 快速入門 {#get-started}

本教學課程需要您具備有效的流程ID。 如果您沒有有效的流ID，請從 [目的地目錄](../catalog/overview.md) 並依照 [連接到目標](../ui/connect-destination.md) 和 [啟動資料](../ui/activation-overview.md) ，再嘗試本教學課程。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [目的地](../home.md): [!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供了您需要了解的其他資訊，以便使用成功刪除資料流 [!DNL Flow Service] API。

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值 {#gather-values-for-required-headers}

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>若 `x-sandbox-name` 標題未指定，則會在 `prod` 沙箱。

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 刪除目標資料流 {#delete-destination-dataflow}

使用現有流ID，您可以通過執行DELETE請求來刪除目標資料流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 要刪除的目標資料流的值。 |

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

成功的回應會傳回HTTP狀態202（無內容）和空白內文。 您可以嘗試對資料流執行查閱(GET)請求以確認刪除。 API會傳回HTTP 404（找不到）錯誤，指出資料流已刪除。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](/help/landing/troubleshooting.md#request-header-errors) 以取得解譯錯誤回應的詳細資訊，請參閱Platform疑難排解指南。

## 後續步驟 {#next-steps}

依照本教學課程，您已成功使用 [!DNL Flow Service] 將現有資料流刪除到目標的API。

有關如何使用用戶介面執行這些操作的步驟，請參閱 [刪除UI中的資料流](../ui/delete-destinations.md).

你現在可以繼續 [刪除目標帳戶](/help/destinations/api/delete-destination-account.md) 使用 [!DNL Flow Service] API。
