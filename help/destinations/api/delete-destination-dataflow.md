---
keywords: Experience Platform；首頁；熱門主題；流程服務；API；API；刪除；刪除目的地資料流程
solution: Experience Platform
title: 使用流程服務API刪除目的地資料流
type: Tutorial
description: 瞭解如何使用資料流服務API將資料流刪除至批次和串流目的地。
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 14%

---

# 使用流程服務API刪除目的地資料流

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)刪除包含錯誤或已過時的資料流。

本教學課程涵蓋使用[!DNL Flow Service]將資料流刪除至批次和串流目的地的步驟。

## 快速入門 {#get-started}

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從[目的地目錄](../catalog/overview.md)中選取您選擇的目的地，並依照概述的步驟[連線至目的地](../ui/connect-destination.md)和[啟用資料](../ui/activation-overview.md)，然後再嘗試進行此教學課程。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [目的地](../home.md)： [!DNL Destinations]是預先建立的與目的地平台的整合，可順暢地從Adobe Experience Platform啟用資料。 您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功刪除資料流。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值 {#gather-values-for-required-headers}

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`標頭，則在`prod`沙箱下解析請求。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 刪除目的地資料流 {#delete-destination-dataflow}

使用現有的資料流識別碼，您可以透過對[!DNL Flow Service] API執行DELETE要求來刪除目的地資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 您要刪除之目的地資料流的唯一`id`值。 |

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

成功的回應會傳回HTTP狀態202 （無內容）和空白內文。 您可以嘗試對資料流進行查詢(GET)請求以確認刪除。 此API將傳回HTTP 404 （找不到）錯誤，這表示資料流已刪除。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 如需解譯錯誤回應的詳細資訊，請參閱Platform疑難排解指南中的[API狀態碼](/help/landing/troubleshooting.md#api-status-codes)和[要求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功使用[!DNL Flow Service] API刪除到目的地的現有資料流。

如需有關如何使用使用者介面執行這些操作的步驟，請參閱有關[在UI中刪除資料流](../ui/delete-destinations.md)的教學課程。

您現在可以使用[!DNL Flow Service] API繼續並[刪除目的地帳戶](/help/destinations/api/delete-destination-account.md)。
