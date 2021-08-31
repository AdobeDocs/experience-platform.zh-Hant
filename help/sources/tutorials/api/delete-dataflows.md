---
keywords: Experience Platform；首頁；熱門主題；流程服務；API;API；刪除；刪除資料流
solution: Experience Platform
title: 使用流服務API刪除資料流
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服務API刪除批處理資料流和流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用流服務API刪除資料流

您可以使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)刪除包含錯誤或已淘汰的批處理資料流和流資料流。

本教學課程涵蓋使用[!DNL Flow Service]刪除批次和串流來源所建立資料流的步驟。

## 快速入門

本教學課程需要您具備有效的流程ID。 如果您沒有有效的流ID，請從[sources overview](../../home.md)中選擇您選擇的連接器，並遵循在嘗試本教學課程之前概述的步驟。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供了您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功刪除資料流。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 刪除資料流

使用現有流ID，可以通過對[!DNL Flow Service] API執行DELETE請求來刪除資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 要刪除的資料流的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。 您可以嘗試對資料流執行查閱(GET)請求以確認刪除。 API會傳回HTTP 404（找不到）錯誤，指出資料流已刪除。

## 後續步驟

按照本教程，您已成功使用[!DNL Flow Service] API刪除現有資料流。

有關如何使用用戶介面執行這些操作的步驟，請參閱有關在UI](../../tutorials/ui/delete.md)中刪除資料流的[教程
